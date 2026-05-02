# Lumiere Finds

A single-page curated product showcase for external marketplace products. The site renders product cards from a separate JavaScript data file, so product updates can be made without editing the page layout.

## Project Files

- `index.html` - Main website, styles, product rendering, filters, gift guide shortcuts, modal, and newsletter demo.
- `products.js` - Product data configuration exposed as `window.PRODUCTS`.

## Preview

Open `index.html` directly in a browser. No build step is required.

If your browser blocks local scripts, run a simple static server from this folder and open the printed local URL:

```bash
python -m http.server 8000
```

## Add A Product

Add a new object to the `window.PRODUCTS` array in `products.js`.

Use only information that is visible in the product screenshot or supplied by the product page data. If a value is unknown, use `null`, `"Unknown"`, or add a note under `details.unknown`.

```js
{
  id: "temu-example-product-010",
  title: "Product title",
  category: "Custom Mugs",
  price: 9.99,
  originalPrice: null,
  rating: null,
  reviews: null,
  badge: "Almost Sold Out",
  tags: ["20oz", "Gift", "Home Decor"],
  description: "Short product description based only on known information.",
  image: "https://example.com/product-image.jpg",
  hoverImage: "",
  marketplace: "Temu",
  productUrl: "https://share.temu.com/example",
  cta: "Buy on Temu",
  featured: 10,
  details: {
    seller: "Unknown",
    sold: null,
    color: "White",
    size: null,
    capacity: null,
    shipping: "Unknown",
    unknown: [
      "Original price is not shown.",
      "Product rating and review count are not shown."
    ]
  }
}
```

## Supported Categories

The current UI includes filters for:

- `Jewelry`
- `Custom Mugs`
- `Pillow Covers`
- `Gifts`
- `Personalized`
- `Holiday Picks`

Use one of these categories when possible. If a new category is needed, add a matching filter button in `index.html`.

## Gift Guide Rules

The Gift Guide cards use rule-based filtering in `index.html`:

- `For Her` shows jewelry and products tagged for women.
- `For Mom` shows products mentioning mom, mother, grandma, or Mother's Day.
- `For Couples` shows mug and coffee-related products.
- `For Home` shows pillow covers and home decor products.
- `Under $20` shows products with `price < 20`.
- `Thoughtful Gifts` shows products related to gifts, birthdays, mom, or Mother's Day.

## Data Guidelines

- Keep all file text ASCII-only to avoid encoding issues.
- Do not invent product details. Use `details.unknown` for anything not shown.
- Keep `featured` unique so sorting is predictable.
- Use direct image URLs in `image`.
- Use marketplace share links in `productUrl`.
- Use `null` for unknown numeric fields such as `originalPrice`, `rating`, `reviews`, or `sold`.

## Validation

Check JavaScript syntax after editing:

```bash
node --check products.js
```

To confirm there are no non-ASCII characters:

```bash
rg -n "[^\\x00-\\x7F]" index.html products.js README.md
```
