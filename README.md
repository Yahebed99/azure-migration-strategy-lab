# azure-migration-strategy-lab
Comparing rehost, replat form, and containerize migration strategies for a small business scenario, with cost/effort/risk tradeoffs
## Scenario

A small business (25-30 users) has a customer database application running on an aging on-premises server. They want to move it to Azure, but need the most cost-effective and least disruptive path to get there.

## Recommendation: Rehost

I recommend **rehosting** the application rather than replatforming or containerizing it. Rehosting is the fastest and cheapest way to get off the physical on-prem server and into Azure.

**The tradeoff:** rehosting doesn't remove the ongoing maintenance burden — the company still owns patching, monitoring, and configuration of the application themselves. But for a small team without a dedicated DevOps setup, a smooth, low-cost transition to the cloud outweighs that tradeoff right now.

## Why Not the Other Options?

- **Replatform** would offload database maintenance to a managed Azure service, but requires more upfront rework and isn't necessary unless the company's maintenance burden becomes a real problem.
- **Containerize** is the most work upfront — the application would need to be repackaged to run in containers — and its main benefit (fast, automatic scaling) doesn't apply here, since this is a small, predictable internal workload, not a public app with unpredictable traffic spikes.
