# UPF Business Workspace

Static single-page UPF stock and order workspace.

## Included changes

- Customer accounts are loaded from Supabase and filtered by the signed-in user's row-level security policies.
- Customer master prices load from `public.customer_prices` when an account is selected.
- The order screen displays the saved before-discount price, discount percentage, and saved net price as read-only values.
- Salespeople can enter an **order-only net price override**. It applies only to the current in-memory order and never updates `customer_prices`.
- An item with no saved customer price is flagged. PDF preview/download is blocked until an order-only override is entered.
- Order totals and PDFs use the saved net price or the order-only override, and the PDF identifies overrides.

## Deploy with GitHub Pages

1. Create a new GitHub repository named `upf-live-stock` (or another name you prefer).
2. Upload the contents of this package to the repository root. Keep `index.html` at the root.
3. In GitHub, open **Settings → Pages** and select **GitHub Actions** as the build/deployment source if GitHub has not selected it automatically.
4. Push to the `main` branch. The included workflow publishes the site. The Pages URL appears under **Settings → Pages** and in the workflow deployment summary.

If your default branch is not `main`, update the branch name in `.github/workflows/deploy.yml`.

## Supabase security note

The page contains the Supabase project URL and publishable client key, which are intended for browser use. Do not add a `service_role` key or secret key to this file. Keep RLS enabled and maintain the existing policies that restrict salespeople to their own customers and allow only admins to modify customer prices.

The live app uses the existing Supabase project configured in `index.html`.
