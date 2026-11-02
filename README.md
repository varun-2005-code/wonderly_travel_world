# ✈ Wanderly – Book your next escape

Wanderly is a single-page travel booking web app built with plain HTML, CSS and JavaScript. No framework and no build step. Browse 25 handpicked destinations, see hotels on a map with driving routes, add a hotel, a car and food to your trip, pay (simulated) and manage your bookings. A built-in chat assistant, **Wanda**, answers trip questions.

> **Demo project.** There is no real backend and no real payment. Accounts, bookings and favourites are stored in your browser's `localStorage` through a simulated REST-style API layer.

## Features

- **Explore and search**: filter by destination, budget and category (Beach, Romance, Culture, Adventure, City), and sort by rating or price.
- **Trip details**: description, highlights, and a live price summary with 12% tax.
- **Interactive map** (Leaflet + OpenStreetMap): hotel pins, driving route, distance, travel time and turn-by-turn directions via the OSRM routing service. Falls back to a straight line if offline.
- **Add-ons**: three hotel tiers, car rental with driver, and local food orders.
- **Checkout**: UPI, card (Luhn check, expiry and CVV validation) and net banking, all simulated.
- **Accounts**: register, sign in and sign out. Passwords are hashed with SHA-256 (Web Crypto) before being stored locally.
- **My trips**: view and cancel bookings. Cancelled bookings are marked as refunded.
- **Payments dashboard**: KPIs, spend by month, and transaction history.
- **Favourites**: save destinations with a heart.
- **Wanda chat assistant**: rule-based, answers from the trip catalogue (budget, style, hotels, cars, food, payments, cancellations).
- **Dark and light theme**, responsive layout, keyboard-accessible, respects `prefers-reduced-motion`.

## Project structure

```
wanderly/
├── index.html   # page markup
├── style.css    # all styles (themes, layout, components)
├── script.js    # data, simulated API, UI logic, map, chat assistant
└── README.md
```

## Run locally

No installation needed.

1. Clone the repo:
   ```bash
   git clone https://github.com/<your-username>/wanderly.git
   cd wanderly
   ```
2. Open `index.html` in a browser, or serve it locally:
   ```bash
   python3 -m http.server 8000
   # then visit http://localhost:8000
   ```

An internet connection is needed for Google Fonts, Leaflet (cdnjs), map tiles and route lookups.

## Deploy with GitHub Pages

1. Push the files to a GitHub repository.
2. Go to **Settings → Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**, select `main` and `/ (root)`, then save.
4. Your site will be live at `https://<your-username>.github.io/wanderly/`.

## Try it

- Use the test card `4242 4242 4242 4242` with any future expiry (e.g. `12/30`) and any CVV.
- UPI example: `name@okbank`.
- Ask Wanda: *"beach trip under 60000"*, *"tell me about Kyoto"*, *"how do I book?"*.

## How it works

| Part | Description |
|------|-------------|
| `DEST`, `COORD`, `HT`, `CT`, `FD` | Destination catalogue, map coordinates, hotel, car and food data |
| `API(method, path, body)` | Fake REST layer with routes such as `/auth/login`, `/bookings` and `/favs`, persisted in `localStorage` |
| `openTrip()` / `initMap()` / `showRoute()` | Trip dialog, Leaflet map and OSRM routing |
| `openTrips()` / `openDash()` | My trips and payments dashboard |
| `bot` | Chat assistant logic |

## Tech stack

- HTML5 (`<dialog>`), CSS3 (custom properties, grid, `color-mix`), vanilla JavaScript (ES2020)
- [Leaflet](https://leafletjs.com/) and [OpenStreetMap](https://www.openstreetmap.org/) tiles
- [OSRM](https://project-osrm.org/) public demo server for routing
- Google Fonts: Bricolage Grotesque and DM Sans

## Limitations

- Client-side only: data is per-browser and can be edited by the user, so this is not secure for real use.
- The OSRM demo server is for light use only. Use your own routing service in production.
- Hotel pin positions are illustrative, generated from each hotel's listed distance.

## Ideas for next steps

- Real backend (Node/Express or similar) with a database and proper authentication
- Real payment gateway (Razorpay or Stripe)
- Real hotel and flight data, photos and reviews
- Move the catalogue into a `data.json` file

## License

MIT. Add a `LICENSE` file to your repository if you want to publish under this license.
