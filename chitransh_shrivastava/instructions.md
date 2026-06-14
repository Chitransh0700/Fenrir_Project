# chitransh_shrivastava: National Social Gaming

## Full-Stack Online Gaming Platform

|                    |                                                                                                                |
| ------------------ | -------------------------------------------------------------------------------------------------------------- |
| **Category**       | Web Development                                                                                                |
| **Client context** | Online gaming platform with game discovery, authentication, social features, reviews, favourites, and rewards. |
| **Primary tools**  | React.js or Next.js (frontend), Node.js + Express (backend), MongoDB or equivalent database                    |
| **Language**       | English                                                                                                        |

---

## Context

National Social Gaming (NSG) is a browser-based gaming platform. This task covers the **full stack**: a backend API server with a database, and a frontend that consumes that API to render the homepage, game detail pages, and footer **exactly as shown in the five reference images**.

> **No hardcoded game data is permitted in the frontend.** All game, category, review, trending, and user data must come from the backend API.

---

## Reference Files

Five reference images are provided:

| File                                 | Purpose                                                                   |
| ------------------------------------ | ------------------------------------------------------------------------- |
| `logo.png`                           | NSG logo. Use in navbar, sidebar, footer.                                 |
| `Front_page.png`                     | Homepage layout reference.                                                |
| `Image_of_next_game_when_opened.png` | Desktop (1440px) game detail page reference.                              |
| `afterOpeningAnyGame.png`            | Responsive (768px) game detail page reference.                            |
| `footer.png`                         | Footer reference with link columns, newsletter, stats bar, and legal bar. |

Study all five images and `NSG_UI_Design_System.pdf` **before writing any code**. Every element visible in the reference images must appear in the final deliverable.

---

## Tech Stack

- **Frontend:** React.js (CRA) or Next.js 14, Tailwind CSS or CSS custom properties, React Router (if CRA) or Next routing.
- **Backend:** Node.js + Express.
- **Database:** MongoDB with Mongoose (or an equivalent database — document the choice in `README.md`).
- **Authentication:** JWT. Passwords hashed with bcrypt.
- **Icons:** Lucide React or React Icons.

> No UI libraries that override the custom colour palette (no Material UI, no Ant Design, no Bootstrap).

---

## Project Structure

```text
nsg-platform/
├── backend/
│   ├── src/
│   │   ├── models/
│   │   │   ├── Game.js
│   │   │   ├── Review.js
│   │   │   ├── User.js
│   │   │   ├── Category.js
│   │   │   └── NewsletterSubscriber.js
│   │   ├── routes/
│   │   │   ├── games.js
│   │   │   ├── categories.js
│   │   │   ├── reviews.js
│   │   │   ├── auth.js
│   │   │   ├── users.js
│   │   │   └── newsletter.js
│   │   ├── middleware/
│   │   │   └── auth.js
│   │   ├── seed/
│   │   │   └── seed.js
│   │   ├── app.js
│   │   └── server.js
│   ├── .env.example
│   └── package.json
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   │   ├── Navbar.jsx
│   │   │   ├── Sidebar.jsx
│   │   │   ├── Footer.jsx
│   │   │   ├── GameCard.jsx
│   │   │   ├── CategoryCard.jsx
│   │   │   ├── HeroBanner.jsx
│   │   │   ├── ReviewCard.jsx
│   │   │   ├── PlayPanel.jsx
│   │   │   ├── GameInfoPanel.jsx
│   │   │   ├── ThumbnailStrip.jsx
│   │   │   └── SectionRow.jsx
│   │   ├── pages/
│   │   │   ├── HomePage.jsx
│   │   │   ├── GameDetailPage.jsx
│   │   │   ├── LoginPage.jsx
│   │   │   └── SignUpPage.jsx
│   │   ├── services/
│   │   │   └── api.js
│   │   ├── context/
│   │   │   └── AuthContext.jsx
│   │   ├── styles/
│   │   │   └── globals.css
│   │   ├── App.jsx
│   │   └── index.jsx
│   ├── public/
│   │   └── logo.png
│   └── package.json
└── README.md
```

---

## Colour Palette

Define all colours as CSS custom properties in `:root` (frontend) or a Tailwind config extension. Apply the **70 / 20 / 10** visual balance rule from the design system:

- **70%** dark backgrounds — `#060816`, `#0C1023`, `#090D1A`
- **20%** neon green — `#A3FF12`
- **10%** purple / cyan — `#8B5CF6`, `#00D4FF`

Use the full palette table from the assets document. **No colour outside this palette in any primary UI element.**

| Token                     | Hex                               | Usage                        |
| ------------------------- | --------------------------------- | ---------------------------- |
| Main Background           | `#060816`                         | Page base                    |
| Secondary Background      | `#0C1023`                         | Panels, footer               |
| Navbar Background         | `#0A0E1E`                         | Top navbar                   |
| Sidebar Background        | `#090D1A`                         | Left sidebar                 |
| Search Bar                | `#11172B`                         | Inputs, search               |
| Card Background           | `#12172B`                         | Game/category cards          |
| Card Hover                | `#1A203A`                         | Card hover                   |
| Card Border               | `#242B4A`                         | Card/section borders         |
| Information Panel         | `#101629`                         | Play / info panels           |
| Active Menu Background    | `#16231A`                         | Active sidebar item          |
| Neon Green (CTA / Active) | `#A3FF12`                         | CTAs, active state, progress |
| Electric Purple           | `#8B5CF6`                         | Secondary buttons, glow      |
| Neon Cyan                 | `#00D4FF`                         | Accents, glow                |
| Rating Star               | `#FACC15`                         | Stars                        |
| Primary Text              | `#FFFFFF`                         | Headings                     |
| Secondary Text            | `#B6BDD7`                         | Body                         |
| Muted Text                | `#6E7694`                         | Meta, breadcrumb             |
| Success / Error / Info    | `#22C55E` / `#EF4444` / `#38BDF8` | Status                       |

---

## Typography

Load from Google Fonts:

- **Inter** (400, 500, 600, 700) — body and UI.
- **Rajdhani** or **Orbitron** (600, 700) — hero headlines and major section titles.

---

## Backend — API Endpoints

Implement all endpoints below. All list endpoints return JSON **arrays**. All single-resource endpoints return JSON **objects**. Protected endpoints require a valid `Authorization: Bearer <token>` header and return **401** if missing or invalid.

### Games

```http
GET /api/games
```

- Query params: `category`, `trending` (boolean), `featured` (boolean), `search` (string, matches title)
- Returns array of game **summary** objects (no full screenshots/reviews)

```http
GET /api/games/:id
```

- Returns full game object including `screenshots` array, embedded or referenced reviews, and a `relatedGames` array (3 games from the same category)

```http
GET /api/games/trending
```

- Returns games where `trendingRank` is not null, sorted ascending by `trendingRank`, **max 6**

```http
GET /api/games/recommended
```

- Returns a curated/random set of games for the homepage _Recommended For You_ row, **minimum 6**

### Categories

```http
GET /api/categories
```

- Returns array of `{ name, icon, gameCount }` — `gameCount` computed **live** from the games collection

### Reviews

```http
GET /api/games/:id/reviews
```

- Returns array of review objects for the given game

```http
POST /api/games/:id/reviews          [PROTECTED]
```

- Body: `{ rating: Number, text: String }`
- Creates a review attributed to the authenticated user; returns the created review

### Auth

```http
POST /api/auth/register
```

- Body: `{ username, email, password }`
- Hashes password with bcrypt, creates user with `coins: 0`, returns `{ token, user }`

```http
POST /api/auth/login
```

- Body: `{ email, password }`
- Validates credentials, returns `{ token, user }`

```http
GET /api/auth/me                      [PROTECTED]
```

- Returns the authenticated user's profile (excluding password hash)

### Favourites

```http
GET    /api/users/favourites          [PROTECTED]
POST   /api/users/favourites/:gameId  [PROTECTED]
DELETE /api/users/favourites/:gameId  [PROTECTED]
```

- `GET` returns array of full game objects in the user's favourites list
- `POST` adds `gameId` to the favourites array, returns updated array
- `DELETE` removes `gameId` from the favourites array, returns updated array

### Recently Played

```http
GET  /api/users/recently-played          [PROTECTED]
POST /api/users/recently-played/:gameId  [PROTECTED]
```

- `GET` returns games the user has played, most recent first, **max 10**
- `POST` records a play event with the current timestamp, deduplicates by `gameId` (updates timestamp if already present)

### Rewards

```http
GET  /api/users/rewards         [PROTECTED]
POST /api/users/rewards/claim   [PROTECTED]
```

- `GET` returns `{ coins: Number, canClaimDaily: Boolean }`. `canClaimDaily` is `true` if `lastDailyRewardClaim` is null or more than 24 hours ago.
- `POST` — if `canClaimDaily` is `true`, add a fixed amount (e.g. **50 coins**), set `lastDailyRewardClaim` to now, return updated coins. If `false`, return **400** with an error message.

### Newsletter

```http
POST /api/newsletter/subscribe
```

- Body: `{ email }`
- Validates email format, stores in the `NewsletterSubscriber` collection (dedupe by email), returns a success message

---

## Backend — Seed Script

Create `backend/src/seed/seed.js` that:

- Connects to the database using the connection string from `.env`
- Clears existing **Games, Reviews, Categories, Users** collections
- Inserts all **6 categories** from the assets document
- Inserts **minimum 15 games** from the assets document seed list, each with **minimum 4 screenshots** (placeholder image URLs) and **minimum 3 reviews** (review documents referencing the game)
- Inserts **City Car Racer** with the complete data specified in the assets document, including all **5 reference reviews** matching the rating distribution percentages as closely as integer review counts allow
- Inserts **1 demo user**: email `demo@nsg.com`, password `Demo1234!` (hashed), with `coins: 250` to match the reference image coin display

Run via `npm run seed` from the backend directory. Document this command in `README.md`.

---

## Frontend — Page 1: Homepage

Build to match `Front_page.png` exactly.

### Top Navigation Bar

- Fixed, height **60px**, background `#0A0E1E`.
- **Left:** NSG logo from `logo.png`.
- **Centre:** search bar, placeholder `Search games, categories...`, background `#11172B`, border-radius 24px. On submit, navigates to a search results view or filters the games list via `GET /api/games?search=`.
- **Right:** Rewards button (links to rewards section/modal showing data from `GET /api/users/rewards` if authenticated), coin display showing current balance (from `/api/users/rewards` if authenticated, otherwise a static placeholder), Login/Sign Up button (navigates to `/login` if not authenticated, shows user avatar/menu if authenticated).

### Left Sidebar

- Fixed, width **200px**, background `#090D1A`.
- NSG logo + tagline at top.
- Nav items: **Home, All Games, Categories, Trending, New Games, Top Rated, Multiplayer, Favorites, Recently Played**.
- Favorites and Recently Played routes call the corresponding protected API endpoints when authenticated; if not authenticated, prompt to log in.
- **Active item:** background `#16231A`, left border 3px `#A3FF12`, icon/text `#A3FF12`. **Inactive:** text `#D0D5E6`.
- Promotional card: trophy icon, "Play More" / "Earn More" (green), description text, "View Challenges" button (`#8B5CF6`).
- Bottom: Settings, Help & Support, Login/Sign Up links, Dark Mode toggle (default on).

### Hero Banner

- Height ~**320px**, background `#140B38`.
- Headline **"PLAY TOGETHER"** (white) / **"WIN TOGETHER"** (`#A3FF12`), display font, bold.
- Subtext paragraph.
- Buttons: **"Explore Games >"** (green outline, scrolls to Recommended section), **"Join Now"** (dark, navigates to `/signup`).
- Character illustration with purple/blue glow effects (CSS radial gradients or box-shadow).
- Right side: 3 stacked quick-access cards — **Daily Rewards** (Claim Now! — calls rewards claim endpoint if authenticated), **Leaderboards** (Top Players), **Play Together** (Invite Friends).
- Dot pagination indicators below.

### Recommended For You

- Fetches `GET /api/games/recommended` on mount.
- Heading with controller icon, "View All >" link in `#A3FF12`.
- Horizontal scroll row of game cards (**minimum 6**), scroll arrow button.
- **Game card:** thumbnail, title (bold white), rating (`#FACC15` star + value), player count (icon + value), featured badge (lightning icon) if `isFeatured`. Background `#12172B`, hover `#1A203A`, border `#242B4A`, radius 12px, width ~180px.

### Browse by Categories

- Fetches `GET /api/categories` on mount.
- Heading with grid icon.
- **7 cards:** the 6 categories plus a View All card. The 6 categories are `Action` (124 games), `Adventure` (98 games), `Racing` (76 games), `Puzzle` (110 games), `Sports` (85 games), and `Strategy` (63 games). Each card shows icon, name, and game count from the API. Background `#12172B`, border `#242B4A`, radius 12px.

### Trending Now

- Fetches `GET /api/games/trending` on mount.
- Same structure as Recommended For You, with a **rank number badge (1–6)** overlaid top-left of each card thumbnail.

---

## Frontend — Page 2: Game Detail (Desktop, ≥1024px)

Build to match `Image_of_next_game_when_opened.png` at 1440px. Fetches `GET /api/games/:id` on mount based on the route param. Same navbar/sidebar as homepage with appropriate active states.

- **Breadcrumb:** `Home > {category} > {title}`. Home link navigates to `/`, current page in white, others muted `#6E7694`.
- **Game header:** title (H1 white bold), verified badge, rating, player count, category tag, tag chips (from `game.tags`).
- **Favorite button:** heart icon + "Favorite" label. If authenticated, clicking calls `POST`/`DELETE /api/users/favourites/:gameId` and toggles filled/outline state based on whether the game is in the user's favourites (checked via `GET /api/users/favourites`). If not authenticated, prompt login.
- **Share button:** share icon (Web Share API or copy link).
- **Video player container** (`#12172B`, radius 12px, 16:9): play button overlay; static overlay data positioned to match the reference image. `POS 2/8` overlay top left. `LAP 2/3` with timer `01:45.67` overlay top right. Speedometer reading `238 KM/H` overlay bottom right. Video itself can be a placeholder image or looping muted video.
- **Screenshot strip:** vertical column to the right of the video at desktop width, showing `game.screenshots` (**minimum 4**); last tile shows "+N Screenshots" if more than 4 exist.
- **About This Game:** heading + description, "Read more" toggle (expands/collapses if long).
- **Key Features:** heading + checkmark list from game data (hardcode the 5 City Car Racer features from assets for that game; other games may have generic feature lists in seed data).
- **Player Reviews:** fetches `GET /api/games/:id/reviews`. Aggregate rating (large number), 5-star visual, "Out of 5" label, distribution bars (5★ to 1★) using `game.ratingDistribution`, colour `#A3FF12`. For City Car Racer the aggregate rating is `4.6`, the review count is `128`, and the distribution is `5★ 73%`, `4★ 17%`, `3★ 6%`, `2★ 2%`, `1★ 2%`. Review cards below: avatar, username, timestamp, star rating, text. If authenticated, show a review submission form (rating + text) that POSTs to the reviews endpoint and prepends the new review on success.
- **Right panel:**
  - **Play card** (`#101629`, radius 16px): "Play {title}", "Free To Play" (`#A3FF12`) or price, in-game purchases note, support icons/labels, **"Play Now"** button (full width, `#A3FF12`, black bold text, height 48px — clicking calls `POST /api/users/recently-played/:id` if authenticated), **"Invite Friends"** button (full width, transparent, border `#8B5CF6`, text `#8B5CF6`).
  - **Game Information panel:** heading with info icon, rows for Developer, Release Date, Last Update, Platform, Language, Game Mode.

---

## Frontend — Page 3: Game Detail (Responsive, ≤768px)

Match `afterOpeningAnyGame.png`. Verify the layout at the `768px` tablet breakpoint and at the `375px` mobile breakpoint.

- Screenshot strip moves **below** the video as a horizontal scroll row with arrow navigation.
- Right-panel sections reflow below the main content.
- **"You May Also Like"** replaces Key Features in the right-panel flow, showing `relatedGames` from the API response (3 games: thumbnail, name, rating, player count, category tag).

---

## Frontend — Footer

Match `footer.png`. **Present on all pages.**

- **Logo block:** NSG logo + description text.
- **App store badges:** static images, links can be `#`.
- **Social icons:** Discord, Instagram, YouTube, Twitter, Facebook (links `#`).
- **Four columns** with exact links from the assets document: **EXPLORE, COMMUNITY, SUPPORT, COMPANY**.
- **Newsletter box "STAY IN THE GAME":** email input + "Subscribe Now" button (`#A3FF12`). On submit, calls `POST /api/newsletter/subscribe` and shows a success/error message.
- **Stats bar:** 2M+ Active Players, 1500+ Games, 500K+ Communities, 250+ Tournaments, 24/7 Live Events, 99.9% Uptime — may be static values matching the reference image (not required to be live-computed).
- **Bottom bar:** Safe & Secure Gaming (shield icon), copyright text with heart icon, Secured Payments (lock icon).

---

## Frontend — Auth Pages

### Login (`/login`)

Email and password fields, "Login" button. On submit, calls `POST /api/auth/login`, stores the returned JWT (localStorage or context), redirects to homepage. Link to `/signup`. Styled with the dark NSG theme: card on `#0C1023` background, inputs background `#11172B`, primary button `#A3FF12`.

### Sign Up (`/signup`)

Username, email, password fields, "Sign Up" button. On submit, calls `POST /api/auth/register`, stores JWT, redirects to homepage. Link to `/login`. Same styling as Login.

### Auth Context

A React context provides the current user, token, `login()`, `logout()`, and `register()` functions to the whole app. Navbar shows Login/Sign Up button when unauthenticated and a user avatar/menu when authenticated. Avatar menu includes **Logout**, which clears the token and redirects to homepage.

---

## Navigation and Routing

| Route       | Page                                                                    |
| ----------- | ----------------------------------------------------------------------- |
| `/`         | Homepage                                                                |
| `/game/:id` | Game Detail Page (desktop or responsive layout based on viewport width) |
| `/login`    | Login Page                                                              |
| `/signup`   | Sign Up Page                                                            |

Clicking any game card navigates to `/game/:id` using the game's database `_id`.

---

## Interactions and States

- **Hover:** game cards lift with box-shadow, background `#12172B → #1A203A`. Category cards show `#A3FF12` border glow. Nav links show `#A3FF12` on hover. CTA buttons show 0.9 opacity on hover.
- **Search bar:** focus state border 1px `#A3FF12`.
- **Dark mode:** default on. Toggle in sidebar controls a class on the `html` element (light-mode implementation optional, but the toggle must be present and functional in some form).
- **Horizontal scroll rows:** smooth scroll via arrow button click, scroll by one card width. Arrow hidden at scroll start/end.
- **Favourite toggle:** heart icon fills (`#EF4444` or `#A3FF12`, developer's choice within palette) when favourited, outline when not, reflecting live state from the backend.

---

## Environment Variables — `.env.example` (backend)

```env
PORT=5000
MONGODB_URI=mongodb://localhost:27017/nsg
JWT_SECRET=your_jwt_secret_here
JWT_EXPIRES_IN=7d
```

---

## README.md Requirements

1. Project title and one-line description
2. Architecture overview (frontend + backend, tech stack used)
3. Prerequisites (Node.js version, database requirement)
4. Backend setup: install, configure `.env`, run seed script, start server
5. Frontend setup: install, configure API base URL, run dev server
6. Demo account credentials (`demo@nsg.com` / `Demo1234!`)
7. Full API endpoint list with method, path, and auth requirement
8. Folder structure overview
9. Colour palette source reference
10. Known limitations or placeholder content notes

---

## Deliverables

Every item below must be present for the submission to be accepted.

1. **Frontend source code** — a React or Next.js application styled with Tailwind CSS or CSS custom properties. Implements 5 screens: the homepage, the desktop game detail page, the responsive game detail page, the `/login` page, and the `/signup` page. Responsive at the 1440px, 768px, and 375px breakpoints. Dark mode is the default and only theme.

2. **Backend source code** — a Node.js and Express REST API served under the `/api` base path on port `5000`. Implements all 15 endpoints defined in the API Endpoints section, using MongoDB with Mongoose. Authentication is JWT based; passwords are hashed with bcrypt; protected routes return `401` without a valid `Authorization: Bearer <token>` header.

3. **Database seed script** — `backend/src/seed/seed.js`, runnable with `npm run seed`. Seeds a minimum of 15 games across the 6 categories (Action, Adventure, Racing, Puzzle, Sports, Strategy), a minimum of 4 screenshots per game, a minimum of 3 reviews per game, the 6 category records, and 1 demo user (`demo@nsg.com` / `Demo1234!` / `coins: 250`). Includes City Car Racer with rating `4.6`, review count `128`, and distribution `5★ 73%`, `4★ 17%`, `3★ 6%`, `2★ 2%`, `1★ 2%`.

4. **`backend/.env.example`** — an environment template documenting `PORT`, `MONGODB_URI`, and `JWT_SECRET`. No real secrets are committed.

5. **`README.md`** — a root readme containing the 10 sections listed in the README.md Requirements section, including separate frontend and backend setup steps, the seed script command, and the demo account credentials.

6. **Public GitHub repository** — a publicly accessible repository containing a `frontend/` folder and a `backend/` folder.

7. **Running application** — the app runs locally end to end: the backend serves the API, the frontend consumes it from the API only (no hardcoded game data), every page renders, and there are no console errors in Chrome on final delivery.

## Scope Boundaries

The following are explicitly OUT of scope for this engagement:

- Real multiplayer netcode or a playable game engine. Launching a game shows a placeholder; no actual gameplay is built.
- Real payment processing or real money in-app purchases. The coin balance and daily rewards are simulated only.
- Native iOS or Android applications. Delivery is responsive web only at 1440px, 768px, and 375px.
- Real email delivery for the newsletter. The `POST /api/newsletter/subscribe` endpoint stores the email only; no SMTP or transactional email is sent.
- OAuth or social login. Authentication is email and password with JWT only.
- Backend features for Community, Friends, Leaderboards, Tournaments, Events, Clans, Forums, and Live Streams. These appear as navigation and footer links only, with no functional endpoints.
- An admin or content-management dashboard. Game data is loaded by the seed script only.
- Production hosting, CI/CD, or domain setup. A local end-to-end run is the delivery target.

---

## Acceptance Checklist

- [ ] Backend server runs and connects to the database
- [ ] Seed script populates minimum 15 games, 6 categories, reviews, and a demo user
- [ ] All listed API endpoints implemented and return correct data shapes
- [ ] Protected endpoints reject requests without a valid JWT
- [ ] Homepage matches `Front_page.png` layout at 1440px
- [ ] Sidebar present with all nav items and correct active/inactive states
- [ ] Navbar present with logo, search, rewards, coins, auth button
- [ ] Hero banner matches reference with all text, buttons, and quick-access cards
- [ ] Recommended For You shows minimum 6 cards fetched from API
- [ ] Browse by Categories shows all 6 categories with live game counts plus View All
- [ ] Trending Now shows rank-badged cards fetched from API
- [ ] Game detail (desktop) matches `Image_of_next_game_when_opened.png` at 1440px
- [ ] Breadcrumb present and Home link navigates correctly
- [ ] Video player container with all overlays present
- [ ] Screenshot strip on right at desktop width
- [ ] Play Now and Invite Friends buttons styled and present
- [ ] Game Information panel shows all 6 fields
- [ ] Player Reviews section shows aggregate rating, distribution bars, and review list from API
- [ ] Authenticated users can submit a review that appears in the list
- [ ] Game detail (responsive) matches `afterOpeningAnyGame.png` at 768px
- [ ] Screenshot strip moves below video at 768px
- [ ] You May Also Like shows 3 related games at responsive width
- [ ] Favourite button toggles and persists via backend
- [ ] Footer matches `footer.png` with all 4 link columns, newsletter box, stats bar, and bottom bar
- [ ] Newsletter form submits to backend and shows success/error
- [ ] Login page functional, issues JWT, redirects on success
- [ ] Sign Up page functional, creates user, issues JWT
- [ ] Navbar reflects authenticated state with user menu and logout
- [ ] Recently played and favourites pages show data for the authenticated user
- [ ] Daily reward claim endpoint and UI element function correctly
- [ ] All colours match the NSG design system palette
- [ ] NSG logo appears correctly in navbar, sidebar, and footer
- [ ] No console errors in Chrome on homepage, game detail, login, and signup pages
- [ ] README.md present with all 10 required sections
- [ ] Repository is public with `frontend/` and `backend/` folders and `.env.example` present

---

## Final Self-Check Before Submission

- Start the backend, run the seed script, confirm 15+ games exist in the database.
- Start the frontend and confirm the homepage loads data from the API with no console errors.
- Open the City Car Racer detail page and compare against `Image_of_next_game_when_opened.png` at 1440px.
- Resize to 768px and compare against `afterOpeningAnyGame.png`.
- Scroll to the footer and compare against `footer.png` — confirm all 4 columns, newsletter, stats bar, and bottom bar are present.
- Register a new account, confirm the JWT is issued and the navbar updates.
- Log in as the demo account (`demo@nsg.com` / `Demo1234!`), favourite a game, refresh the page, confirm the favourite persists.
- Submit a review on a game detail page while authenticated, confirm it appears in the review list.
- Subscribe to the newsletter from the footer, confirm a success message appears and the email is stored in the database.
- Claim the daily reward, confirm coins increase and the button becomes unavailable until 24 hours pass.
- Confirm all colours match the design system palette throughout.
- Confirm `README.md` covers both frontend and backend setup completely.
