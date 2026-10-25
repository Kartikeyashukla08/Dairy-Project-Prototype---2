# DairyDesk — Dairy Operations Prototype

This is a deliberately lightweight front-end prototype for exploring the workflow. It includes:
- Demo multi-role login (owner, collection staff, accountant)
- Farmer records and per-farmer payment cycles
- Milk collection with quantity, fat, optional SNF, owner-controlled rate and computed amount
- Daily electricity meter readings and estimated charges
- B2B bulk milk sales
- Milk transfers to pouch-packing outlet
- Outlet cash collection and expenses
- Farmer ledger, advances/payments, balance estimate, printable statement with signature lines
- Incentive targets and farmer progress based on litres or points (fat × quantity)
- Outstanding debt estimate, raw material purchase entries
- Weekly milk/points report, audit log, JSON backup and restore

## Run locally
1. Unzip the folder.
2. Open `index.html` in a modern browser.
3. Sign in using one of the demo accounts:
   - `owner` / `owner123`
   - `staff` / `staff123`
   - `accountant` / `acct123`

The prototype stores data in the current browser's `localStorage`. The demo passwords and role checks are visible in the JavaScript. This is **not secure for real customer/business data**.

## Deploy the prototype on GitHub + Render (static site)
1. Create a GitHub repository, e.g. `dairy-desk-prototype`.
2. Upload `index.html` and this `README.md` to the repository root and commit.
3. Sign in to Render and choose **New + → Static Site**.
4. Connect the GitHub repository.
5. Set Build Command to blank (or use `echo "Static prototype"` if the UI requires a command).
6. Set Publish Directory to `.` (repository root).
7. Deploy. Render will provide a public URL.
8. For future changes, push commits to GitHub; Render can redeploy automatically.

## Important: what “local data” means here
`localStorage` is local to each browser profile/device. If staff enter milk on one phone, the owner will **not** see that entry on another computer. Clearing browser data can erase the records. Deploying this static app to Render does not turn browser storage into a shared database, and GitHub is source-code hosting—not a database.

For a real client delivery, keep the prototype UI if useful but replace the demo authentication and browser storage with:
- A backend API (for example, Node.js/Express)
- A shared database (for example, PostgreSQL on a managed host)
- Real password hashing and session management
- Server-side role/permission enforcement and audit logging
- Automated backups, HTTPS, and a tested restore procedure

A practical low-cost architecture is: GitHub (source) → Render Static Site (frontend) + Render Web Service (backend) → managed PostgreSQL. Another option is a hosted backend/database such as Supabase, with strict Row Level Security policies. Choose based on budget, data ownership, support and backup needs.

## Business logic caveats to validate with the client
- The current ledger is a basic estimate: milk value minus recorded payments/advances. Production accounting should define how advances, deductions, rejected milk, bonuses, penalties, carry-forward balances and payment periods work.
- The “litres needed to clear debt” card currently uses debt ÷ expected selling price. That is gross revenue, not profit. A production version should use contribution margin after procurement, packaging, electricity, transport, wastage and other costs.
- The weekly report is based on calendar weeks (Monday–Sunday) and all entries currently entered in the browser.
- Automated SMS/WhatsApp reminders are not sent by this prototype. They require an approved provider, message templates, consent and delivery/error handling.
- Milk entry editing/deletion, stock decrement/expiry, multi-branch support, tax invoices, export to Excel, payment-cycle due alerts and reconciliation are future improvements.

Do not use the prototype's demo login or localStorage for real business operations.
