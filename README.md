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
## Hands-On: Rehosting in Practice

I built this out in Azure to validate the recommendation above

### What I did
- Created a resource group (`rg-rehost-lab`) to contain the project
- Provisioned an Ubuntu 22.04 VM (`vm-rehost-demo`, Standard_B1s) using Azure CLI
- Connected to the VM via SSH
- Installed and started nginx to simulate hosting the migrated application
- Hit a real issue: nginx was running, but the site was unreachable from the browser
- <img width="2560" height="1392" alt="Screenshot 2026-10-02 174423" src="https://github.com/user-attachments/assets/bff5e727-6d65-42db-b466-9afe3cac5771" />

- 

### The problem and the fix
When I provisioned the VM, Azure automatically created a Network Security Group (NSG) acting as a firewall in front of it. By default, that NSG only allowed inbound traffic on port 22 (SSH), which is what let me connect to the VM to manage it. It did not allow port 80 (HTTP), so even though nginx was installed and running correctly inside the VM, the website was unreachable from a browser — the request never got past the firewall. I fixed this by running az vm open-port to add a new inbound rule to the NSG allowing traffic on port 80. After that, the site loaded successfully from an outside browser.



### Result
A live web server reachable at a public IP, built and troubleshot entirely through Azure CLI.
<img width="1920" height="1032" alt="Screenshot 2026-10-02 175115" src="https://github.com/user-attachments/assets/864ad6c3-4540-42de-aa54-2a98857bc06d" />
