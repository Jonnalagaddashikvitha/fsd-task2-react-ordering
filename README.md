
Ember & Thyme
A table-side digital ordering app for a wood-fired Italian restaurant. Guests scan a QR code at their table, browse and filter the menu, build a cart with automatic 5% GST, and follow their order through the kitchen in real time.

Built for 21CSE354T – Full Stack Web Development, Task 2: Interactive JavaScript and ReactJS Application Development at SRM Institute of Science and Technology, Trichy Campus.

Features
QR table binding (Tables #1–#12): opening the page with ?table=N selects that table. Guests can also switch tables from the floor-plan strip.
Multi-criteria menu filtering: filter by course, dietary tag (VEG, NON-VEG, VEGAN, gluten-free) and a case-insensitive search across dish names and descriptions. All three filters combine.
Slide-over cart: add, increase and decrease items, and attach chef notes such as "medium-rare". Lines with the same dish and the same note merge into one.
GST billing: subtotal, 5% GST and grand total update instantly, with GST rounded to two decimals.
Live order tracker: after dispatch, the order moves through four stages: Order Received, Wood-Fired Prep, Plating & Ready, Served at Table.
Light and dark themes: follows the device setting.
Responsive: works from phone width upward.
Tech stack
React 18 (functional components and hooks)
useState for UI state, useEffect for QR parsing and the tracker timer, useMemo for filtered dishes and cart totals
htm for JSX-style templates without a build step
Plain CSS with design tokens (no framework)
React and htm load from a CDN, so the page needs an internet connection the first time it opens.

Run it
No install needed. Download or clone the repo, then either:

Option A: open the file

Open index.html in any modern browser.

Option B: serve it locally (recommended for testing QR links)



bash
python -m http.server 8000
Then visit:

http://localhost:8000/ for the default table
http://localhost:8000/?table=4 to simulate scanning the QR code at Table 4
How it works
State lives in the top-level App component and flows down to child components through props and callbacks (unidirectional data flow):

Component	Responsibility
QRTableModal	Table selection for Tables #1–#12
MenuFilterBar	Course, dietary and search controls
DishCard	One menu item with its add button
CartDrawer	Cart lines, notes, GST breakdown, dispatch
LiveOrderTracker	Four-stage order progress
Cart totals:



js
const subtotal = cart.reduce((sum, i) => sum + i.dish.price * i.qty, 0);
const gstAmount = Math.round(subtotal * 0.05 * 100) / 100;
const grandTotal = Math.round((subtotal + gstAmount) * 100) / 100;
Order stages advance automatically every 4 seconds to simulate the kitchen. In a production system this would come from a backend.

Project structure


.
├── index.html   # the whole app: markup, styles and React code
└── README.md
Notes
Menu items and prices are sample data.
No backend: orders are not stored, and refreshing the page clears the cart and tracker.
Possible next steps
Move the app into a Vite + TypeScript project with one file per component
Add a backend (Node and Express) to receive orders
Add a kitchen screen that updates the real order status
Persist the cart across refreshes
Author
J. Shikvitha, B.Tech Computer Science and Engineering, SRM IST Trichy Campus
