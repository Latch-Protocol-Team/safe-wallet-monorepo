# Latch Safe — a re-skinned Safe{Wallet} fork

This is the Safe{Wallet} web app (GPL-3.0, <https://github.com/safe-global/safe-wallet-monorepo>),
re-skinned to serve the self-hosted Safe stack for the chains Latch Protocol runs on (Robinhood
Chain first), where app.safe.global does not index. Built on Safe{Core}; not affiliated with or
endorsed by Safe. The smart-account contracts are NOT modified — this fork deploys and talks to the
canonical Safe v1.4.1 bytecode only.

## Branches

- `dev` — tracks upstream, untouched.
- `latch/web-vX.Y.Z` — upstream release tag `web-vX.Y.Z` plus the commits below. A new upstream
  release is adopted by rebasing these commits onto the new tag.

## The whole diff (keep it this small)

1. **Marks** — `apps/web/public/images/{logo,logo-no-text,logo-round,safe-wallet-lockup}.svg`,
   `safe-logo-green.png` and every favicon under `apps/web/public/favicons/` + `public/favicon.ico`
   replaced by Latch's own marks, same filenames, so no component changes.
2. **Manifest** — `apps/web/public/safe.webmanifest` name/description.
3. **Palette** — Safe's green (`#12FF80`, `#0cb259`, `#B0FFC9`, `#1B2A22`) replaced by Latch blue
   (`#6B8DFF`, `#2F5FE0`, `#C7D3FF`, `#1A2238`) in `packages/theme/src/palettes/*` and the generated
   `apps/web/src/styles/{vars,shadcn}.css`, plus the promo banner that hard-codes the tint.
4. **Name** — the two components that hard-code "Safe" (`SafeLogo` alt text, `LaunchScreen`
   captions) read `BRAND_NAME` (build arg `NEXT_PUBLIC_BRAND_NAME`, "Latch Safe").

Planned next: the in-app Swap page uses Latch's `SwapWidget` (Latch pools only, 25 bps integrator
fee to the governance Safe, shown in the quote) in place of the third-party swap and bridge widgets.

## Build

The image is built by `ops/safe/ui/Dockerfile` in the Latch monorepo: upstream's release image
(same tag, so its `node_modules` match) + this branch's changed files + `yarn build` → static export
served by nginx.
