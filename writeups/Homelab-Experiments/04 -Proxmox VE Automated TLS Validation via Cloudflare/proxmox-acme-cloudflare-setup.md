1\. Objective

Design and implement an automated Public Key Infrastructure (PKI) TLS/SSL certificate issuance and renewal pipeline for the Proxmox Virtual Environment (PVE) management plane. Mitigate inbound attack surface exposure by enforcing Let's Encrypt DNS-01 validation via Cloudflare API, eliminate browser trust degradation, secure Infrastructure-as-Code (Terraform) API endpoints against TLS tampering, and implement deterministic split-horizon DNS resolution across private subnets and VPN tunnels.



🛠2. Environment \& Tools

Virtualization Host: Proxmox VE 8.x (192.168.10.10:8006)



Security Gateway / Edge Resolver: OPNsense Firewall (192.168.10.1)



Authoritative DNS Infrastructure: Cloudflare Nameservers (ridge.ns.cloudflare.com, stephane.ns.cloudflare.com)



Domain Registrar: OVH (NS Delegation to Cloudflare)



PKI / Certificate Authority: Let's Encrypt ACME Engine



IaC \& Orchestration Engine: HashiCorp Terraform (Proxmox Telmate/bpg Provider)



Authentication Vector: Scoped Cloudflare REST API Bearer Token



3\. Methodology \& Execution

Phase 1: Delegation Diagnostics \& Zone Sanitation

Diagnosed persistent ACME validation timeouts and handshake failures using the legacy OVH DNS plugin.



Verified authoritative delegation: Zone marwane-eljaafari.fr registrar records at OVH delegate authoritative control to Cloudflare nameservers. Validation records populated in the OVH DNS console were orphaned and undetectable by Let's Encrypt authoritative resolvers.



Purged stale, unreferenced \_acme-challenge TXT records across the active zone.



Phase 2: Least-Privilege API Token Provisioning

Provisioned a scoped Cloudflare API access token adhering strictly to RBAC:



Permissions: Zone.DNS:Edit



Resource Scope: Restricted solely to the marwane-eljaafari.fr zone boundary.



Integrated the ACME DNS plugin (cf-dns) into Proxmox VE utilizing parameters CF\_Token, CF\_Account\_ID, and CF\_Zone\_ID.



Phase 3: Headless DNS-01 Validation \& Certificate Delivery

Initialized the automated DNS-01 challenge cycle directly via Proxmox ACME client.



Challenge successfully validated out-of-band via Let's Encrypt authoritative validation servers (TASK OK achieved in \~15 seconds).



Installed signed X.509 server certificate binding to the PVE proxy daemon (pveproxy).



Phase 4: Name Resolution Architecture (Split-Horizon / RFC 1918 Direct)

Realigned local PVE upstream DNS resolver to point directly to OPNsense (192.168.10.1).



Configured an authoritative public A record (DNS Only / Gray Cloud) mapping pve.marwane-eljaafari.fr to internal IP 192.168.10.10.



Enforced end-to-end hostname resolution across local VLANs, administrative workstations, and WireGuard remote access peers.



4\. Results \& Artifacts

Zero WAN Attack Surface: Complete elimination of inbound port openings (ports 80/443 remain sealed at the perimeter edge).



High-Assurance Cryptographic Validation: Native browser trust established at \[https://pve.marwane-eljaafari.fr:8006](https://pve.marwane-eljaafari.fr:8006) with full certificate path validation and zero browser exceptions.



Hardened IaC Pipeline: Proxmox API accepts Terraform execution without setting pm\_tls\_insecure = true or insecure = true, preventing machine-in-the-middle (MITM) vulnerabilities.



Autonomous Certificate Lifecycle: Zero-touch bi-monthly renewal automated via background cron/systemd timers interfacing with the Cloudflare API.



5\. Lessons Learned \& Troubleshooting

Pre-Flight DNS Trace: Execute an authoritative trace (dig +trace NS domain.tld) before configuring ACME challenge automation to confirm active authoritative resolvers and prevent registrar/nameserver mismatch.



Credential Hygiene: Avoid global Cloudflare API keys; restrict automation tokens to discrete zone IDs and specific read/write verbs.



Split-DNS vs. Information Disclosure: Publishing RFC 1918 private IP addresses to public authoritative DNS leaks internal IP addressing schemes to passive OSINT reconnaissance. For hardened environments, implement DNS overrides on internal resolvers (OPNsense Unbound DNS) while keeping public DNS zones unpopulated with private addresses.

EOF

