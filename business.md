# Tessera (working name)

Rough skeleton. Its job is to give us shared guidance, not to be a business plan. Change anything.

## What it is
An online marketplace for puzzles and digital art. Indie creators sell on it, and buyers find them in one place instead of hunting across dozens of small shops.

## Who it's for
- **Buyers:** puzzle and art fans who are tired of big-box puzzle sites and don't know where the good indie sellers are.
- **Sellers:** independent artists and small puzzle makers who want a storefront without building one.

## How it makes money
1. **Commission** on sales made through the marketplace.
2. **Referral commission** when a seller keeps their own shop and we send the buyer to it (we earn for being the path they took).

## Product, in thin slices (built in this order)
1. A static storefront page: a catalogue of items with images. (Gets us something to containerize.)
2. Seller profiles and item listings.
3. Checkout (payment provider in test mode only, no real money).
4. Referral link-outs with click tracking.

## Teams (mock, so the platform has customers)
| Team | Owns |
|---|---|
| Platform / DevOps | CI/CD templates, release rings, Terraform, Kubernetes, tooling. A handful of people serving everyone else. |
| Storefront | Buyer-facing site |
| Marketplace | Seller onboarding, listings, commission logic |
| Payments | Checkout, payouts |

The point: a small platform team supports many product teams and many repos, so everything has to scale through automation and templates, not copy and paste.

## Platform principles
- Golden templates, versioned with tags and released in rings (canary, then early adopters, then everyone). No floating refs.
- Every Terraform apply passes through a real approval gate with access control.
- Pre-commit checks on every repo, enforced again in CI.
- Environments: `dev` and `prd`. Azure first. Kubernetes for the workloads.
- Run containers locally on the desktop first. Use the cloud in short, budgeted bursts with teardown.

## Engineering principles
- **Trunk-based development.** Short-lived branches, small PRs, merge to `main` often. The goal is startup speed, not gitflow ceremony. Incomplete work ships behind feature flags.
- **Two tiers: `dev` and `prd`.** Every change shows a visible progression from one to the other.
- **Build once, promote.** One artifact (a container image, tagged by release version) is built a single time and promoted from `dev` to `prd`, never rebuilt per environment.
- **Tagged releases.** Semantic versioning, automated changelogs, conventional commits.
- **Progressive delivery.** Canary and/or blue/green releases, with automated rollback on failed health checks.
- **Best practices on purpose.** Each practice gets a real, working example here, so it can be demonstrated, not just claimed.

## Not goals (for now)
- Real customers, real payments, or real sales.
- A polished brand or an HR-style org chart.
- Anything beyond what a pipeline or repo needs.

## Open questions
- Final name.
- Whether any real artwork is used publicly, and under what terms (see notes in chat).
- Public GitHub org name.
