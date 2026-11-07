# GRACELLE: site files (front end)

Two websites, plain HTML/CSS/JavaScript. No build step, no installs.

| File | What it is |
|---|---|
| `index.html` + `styles.css` + `app.js` | The customer storefront |
| `portal.html` + `portal.css` + `portal.js` | The staff portal (all 10 departments, CEO/GM) |
| `config.js` | **The only file you edit to link to the server** |
| `logo.png` | GRACELLE logo (transparent background) |

## How to link the two parts (3 steps)

1. Deploy the server from `2-server-files` (see its README) and note its address, e.g. `https://api.yourdomain.com`.
2. Open `config.js` and set `window.GRACELLE_API = 'https://api.yourdomain.com';`
3. Upload this whole folder to any static host (Netlify, Vercel, Cloudflare Pages, cPanel, GitHub Pages...).
   - Storefront: `https://yourdomain.com/index.html`
   - Staff portal: `https://yourdomain.com/portal.html` (you can rename it or put it on a subdomain)
4. In the server's `.env`, set `CORS_ORIGIN` to the website address(es) from step 3, so the server accepts them.

For quick local testing: start the server (`node server.js`), then open `http://localhost:3000/` after setting `STATIC_DIR=../1-site-files` in the server `.env`. The server then serves these files itself and everything works from one address.

## What comes from the server (nothing is typed into the code)

Storefront shows, live from the server: published products (photo, colours, sizes, description), prices and approved discounts, Sold Out status, banners (and where each "Shop now" opens), the top autoplay video banner, Flash Sale countdown, announcements, promo sections, FAQs, testimonials, bank/payment details at checkout, delivery fees and "we do not deliver here" rules, support contact details.
Customers: sign up, log in, reset password by emailed code, place orders with a receipt upload, track order status, rate and review, chat with an agent, see vouchers.

Staff portal: login with email + access code (officials) or ID number (regular staff), auto logout after 10 minutes of inactivity, every department's tools, dashboards, attendance QR (scan with camera), tasks, projects, group chat, announcements, My Account.

## Who controls what on the public site

| Storefront item | Department that controls it |
|---|---|
| Products, descriptions | Sales proposes, **Finance approves price** before it goes public |
| Discounts, bundles | Sales proposes, Finance approves |
| Flash Sale / Black Friday, payment methods, bank details | Finance |
| Homepage banners, top video banner, promo sections, announcements | PR & Media |
| Stock / "Sold Out" | Inventory (automatic when the last unit sells) |
| Delivery fees, shipping availability and timelines | Logistics (fee changes approved by Finance) |
| FAQs, support announcements | Customer Care |
| Support phone/email/address, return policy | Customer Care requests, CEO/GM approves |

## Notes

- Banner images and the video are uploaded from the portal (PR & Media). Images up to 5 MB, video up to 40 MB.
- The staff portal needs the camera for attendance. Browsers only allow the camera on `https://` (or localhost).
- "Continue with Apple" shows a message until Apple credentials are added; email + password works fully.
