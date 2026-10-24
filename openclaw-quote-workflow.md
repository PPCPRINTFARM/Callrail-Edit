# OpenClaw: Send a Shopify Quote via Gmail

Use this workflow when a call summary includes a quote request. You need:
- Customer name, company, city/state
- Product SKU(s) requested
- Pricing override (e.g. "GP20NLA at GP20NL price")
- Any discount (e.g. "$180 free shipping")
- Customer email

---

## Step 1 — Look up the product and pricing

Search Shopify for the requested SKU to get the variant ID and list price:

```graphql
# Tool: mcp__Shopify__search_products
# search_query: "GP20NLA"  (or whatever SKU was requested)
```

Then search for the pricing-reference SKU (e.g. GP20NL) to get the target price:

```graphql
# search_query: "GP20NL sku:GP20NL"
```

Note both:
- `variantId` of the product being sold (e.g. GP20NLA)
- `price` of the pricing reference (e.g. GP20NL = $2,663.00)

---

## Step 2 — Create the draft order

```graphql
mutation draftOrderCreate($input: DraftOrderInput!) {
  draftOrderCreate(input: $input) {
    draftOrder {
      id
      name
      invoiceUrl
      subtotalPrice
      totalPrice
    }
    userErrors { field message }
  }
}
```

Variables:
```json
{
  "input": {
    "lineItems": [{
      "variantId": "gid://shopify/ProductVariant/VARIANT_ID",
      "quantity": QTY
    }],
    "shippingAddress": {
      "firstName": "FIRST", "lastName": "LAST",
      "company": "COMPANY",
      "city": "CITY", "provinceCode": "STATE", "countryCode": "US"
    },
    "note": "Quote: Nx PRODUCT at PRICING_SKU pricing. Free shipping to CITY, STATE.",
    "tags": ["quote"]
  }
}
```

Save the returned `id` (e.g. `gid://shopify/DraftOrder/XXXXXXXXX`) and `name` (e.g. `#D3776`).

> **Note:** Do NOT try to set `originalUnitPrice` in the create step — Shopify ignores it and keeps the list price. Fix it in Step 3.

---

## Step 3 — Fix unit price + apply shipping discount

Shopify does not let you override unit price directly. Use a **line-item `appliedDiscount`** to bring each unit down to the target price, plus an **order-level `appliedDiscount`** for the shipping promotion.

Calculate: `lineItemDiscount = listPrice - targetPrice`  
Example: $3,195.00 − $2,663.00 = **$532.00**

```graphql
mutation draftOrderUpdate($id: ID!, $input: DraftOrderInput!) {
  draftOrderUpdate(id: $id, input: $input) {
    draftOrder {
      name
      invoiceUrl
      subtotalPrice
      totalPrice
    }
    userErrors { field message }
  }
}
```

Variables:
```json
{
  "id": "gid://shopify/DraftOrder/XXXXXXXXX",
  "input": {
    "lineItems": [{
      "variantId": "gid://shopify/ProductVariant/VARIANT_ID",
      "quantity": QTY,
      "appliedDiscount": {
        "value": LINE_ITEM_DISCOUNT,
        "valueType": "FIXED_AMOUNT",
        "title": "GP20NL Pricing"
      }
    }],
    "shippingLine": {
      "price": "0.00",
      "title": "Free Shipping to CITY, STATE"
    },
    "appliedDiscount": {
      "value": 180.0,
      "valueType": "FIXED_AMOUNT",
      "title": "Free Shipping Promotion",
      "description": "Free shipping included"
    }
  }
}
```

Verify the response shows:
- `discountedUnitPrice` = target price (e.g. $2,663.00)
- `totalPrice` = expected total (e.g. $5,146.00)

---

## Step 4 — Send the quote email via Gmail

```
Tool: mcp__Gmail__send_message
to: [customer email]
cc: [glen@phoenixphaseconverters.com]
subject: Your [PRODUCT] Quote — Phoenix Phase Converters (#D3776)
```

Email body should include:
- Greeting by first name
- Reference to their call today
- Quote table: Item | Qty | Unit Price | Total
- Shipping line: FREE
- Discount line: −$180.00
- **Total: $X,XXX.00**
- Invoice button linking to `invoiceUrl` from the draft order
- Phone number: 800-417-6568
- Signed: Glen / Phoenix Phase Converters

The `invoiceUrl` from the draft order IS the payment link — customers can pay directly from it.

---

## Quick reference — common variant IDs

| SKU | Variant ID | List Price |
|-----|-----------|------------|
| GP20NL | `gid://shopify/ProductVariant/53793...` | $2,663.00 |
| GP20NLA | `gid://shopify/ProductVariant/54849561264500` | $3,195.00 |

> Always re-query prices before quoting — do not use cached values.

---

## Pricing rule

- **GP20NLA quoted at GP20NL price** = $2,663.00/unit (line-item discount: $532.00)
- Shipping discount: $180.00 (standard for free-shipping offers)
- Total for 2x GP20NLA with free shipping: **$5,146.00**
