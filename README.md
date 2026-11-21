# QC-shop: Corner Dash

The customer shop for a quick-commerce dark store. Mobile-first, and works on phone, tablet and desktop. It sells only what the warehouse has in stock and sends every order to the warehouse in [Quick-Commerce-optimization](https://github.com/Sahilrathour007/Quick-Commerce-optimization).

| File | What it is |
|---|---|
| `index.html` | The shop: search, categories, bestsellers, cart, checkout (pay on delivery), order tracking, and My orders. |
| `core.js` | Demo data and stock maths. The same file is in Quick-Commerce-optimization; keep the two copies identical. |

## Run it
- **Demo:** open `index.html`. Stock and bestsellers come from the demo warehouse.
- **With GitHub Pages:** turn on Pages for this repo and for Quick-Commerce-optimization (Settings → Pages → Deploy from branch → `main`, root). In demo mode, an order placed here appears in the warehouse Orders tab in the same browser, and the tracking page updates as the warehouse picks and packs it.
- **Live:**
  1. Run the warehouse's `supabase/schema.sql` in your Supabase project.
  2. Put the Project URL and the anon public key in `SHOP_SUPABASE_URL` and `SHOP_SUPABASE_ANON_KEY` at the top of the script in `index.html`. The anon key is public by design; the database only lets customers read the catalogue and place or track orders.
  3. Set `price_inr` (and optionally `mrp_inr`, `pack`, `image_url`) on each SKU. SKUs without a price are not shown.

## How ordering works
- What a customer can buy = book stock − units on orders already placed. The cart never allows more.
- `place_order` re-checks stock under a lock, so two customers cannot buy the last unit, and it takes prices from the database, so nobody can change a price in the browser.
- Delivery is free over ₹199, otherwise ₹25. Change `FREE_OVER` and `DELIVERY_FEE` in `index.html`; the same rule is in `place_order`.

## Product photos
The shop draws an original illustration for each product. For real photos, use pack shots your distributors or brands supply, upload them to Supabase Storage, and set `skus.image_url`. Don't copy product photos from other websites; they are the brands' copyright.

## Not built yet
- Online payment (UPI or card). Needs a payment provider.
- Customer accounts. "My orders" lives on the customer's device.
