Project: Secure Linux Workstation Remote Access

Date: 2026-06-07 | Category: Network Architecture & Remote Access | MITRE Tactic: TA0001 (Initial Access) / T1133 (External Remote Services)
1. Objective

Establish secure remote desktop access to a local Linux workstation (Wayland) from external networks. The architecture must bypass internal VLAN routing restrictions without compromising the perimeter security posture or exposing raw TCP ports (specifically RDP/3389) to the WAN.
🛠 2. Environment & Tools

    Target OS: Linux (Wayland display server)

    Service: Native Remote Desktop Protocol (RDP) Server

    Network Infrastructure: OPNsense Firewall, Managed VLANs

    Virtualization/Hosting: Proxmox VE, Docker

    Secure Tunneling: Tailscale (Overlay Network / Zero Trust Access)

3. Methodology & Execution

    Local Service Provisioning: Activated the native RDP server within the Linux system settings under Wayland. Created a dedicated user group and account for remote authentication on local port 3389.

    Network Constraint Analysis: Identified that existing strict VLAN rules (designed to prevent lateral movement) blocked routing from the Proxmox environment to the workstation subnet.

    Threat Modeling (MITRE T1133): Evaluated direct Internet exposure via Cloudflare. Determined that proxying raw RDP traffic over the WAN introduces critical vulnerabilities. Public exposure strategy was formally abandoned.

    Secure Overlay Deployment: Deployed Tailscale to establish an encrypted mesh VPN tunnel directly to the workstation. This securely authenticates the external client and bridges the connection without altering OPNsense firewall perimeter rules or modifying internal VLAN isolation policies.

4. Results & Artifacts

    Secure Access: Remote desktop connection successfully established via the Tailscale overlay network.

    Network Segmentation Maintained: OPNsense and VLAN isolation rules remain intact; lateral movement from Proxmox to the workstation remains restricted by design.

    Perimeter Security: Port 3389 is completely invisible to the WAN, mitigating the risk of brute-force and remote code execution attacks.

5. Lessons Learned & Troubleshooting

    VLAN Efficacy: The inability to route from Proxmox to the desktop validates the effectiveness of the current network segmentation strategy.

    Zero Trust over Perimeter Exposure: Relying on overlay networks (Tailscale) or dedicated perimeter VPNs (OPNsense WireGuard/OpenVPN) is functionally superior and infinitely more secure than attempting to expose local services via standard reverse proxies for raw TCP traffic.
    EOF
