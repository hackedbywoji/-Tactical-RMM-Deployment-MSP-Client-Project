# -Tactical-RMM-Deployment-MSP-Client-Project
This is a remote monitoring and management setup I deployed for a client with 30 Windows laptops and high staff turnover. The company had no visibility into who was using which device at any given time, making it impossible to track equipment, update documentation, or investigate incidents like theft.
---

## 🎯 The Problem

The client had 30 Windows laptops constantly changing hands between employees without notifying the MSP. This created three real problems:

- Documentation was always outdated — no one knew which user had which device
- When laptops were stolen, it was impossible to know who had the device, which Microsoft 365 accounts were active on it, or what data was at risk
- With high staff turnover, accounts were frequently left active on devices assigned to different employees — creating security gaps and compliance issues

This last point became critical after a real incident: several laptops were stolen, and because there was no record of which accounts were logged in on each device, the company couldn't determine the scope of the breach or act quickly to revoke access.

There was no monitoring platform in place. Everything was managed manually, reactively, and with incomplete information.

---

## ⚙️ The Solution

Deployed Tactical RMM, an open-source remote monitoring and management platform for Windows, giving the MSP a centralised web dashboard showing in real time the logged-in user, hostname, and public IP of every device in the fleet.

**Server infrastructure**
Provisioned a Debian 12 VPS (4 vCPU, 8GB RAM, 200GB disk) and configured three DNS subdomains pointing to the server IP: `rmm`, `api`, and `mesh`. Opened the required firewall ports (22, 80, 443, 4222), created a non-root user, and ran the official Tactical RMM installation script. SSL certificates were handled automatically by the installer.

**Agent deployment**
Generated a silent PowerShell deployment script from the Tactical RMM web panel. Executed on each laptop as administrator — installation takes under one minute per device and requires no user interaction. Once installed, the device appears in the dashboard immediately.

**Office 365 account tracking** *(in progress)*
Currently implementing a PowerShell-based tracking system that cross-references each device with its associated Microsoft 365 accounts. This will allow the MSP to know not only who is physically using each laptop, but also which Office 365 accounts are active on it at any given time — closing the last gap in device accountability and making the solution complete for incident response and offboarding workflows.
---

## 🛠️ Tech Used

Tactical RMM, Debian 12 (Linux), VPS, DNS configuration, firewall (UFW), PowerShell, SSL/TLS (auto-managed), Remote Monitoring & Management.

---

## 📊 Result

Centralised web dashboard accessible from anywhere, showing all 30 client devices in real time with logged-in user, hostname, and public IP. The MSP now has full visibility over the fleet, can respond to incidents immediately, and always knows who has which device.

This was the first RMM service ever offered to this client. The deployment created a new billable service for the MSP — a recurring revenue stream that did not exist before. Deployed and configured in a single working day.

---

## 📝 Notes

Built and deployed while working full-time as an IT technician. Prior to this, the MSP had never offered remote monitoring as a service to this client. The project generated direct economic value for the company by opening a new billable service line, while solving a real operational problem for the client.
