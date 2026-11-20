# IT Support & Active Directory Administration Lab

## Project Overview

This project documents hands-on IT support and Windows administration practice in an isolated VMware home lab. It is intended to demonstrate foundational tasks relevant to Desktop Support, IT Support, Help Desk, Junior System Administrator, and Network Support roles.

## Lab Environment

| Component | Details |
|---|---|
| Virtualization | VMware Workstation |
| Domain Controller | Windows Server virtual machine |
| Client | Windows 10 virtual machine |
| Network | VMware NAT / isolated virtual lab |
| Domain | adlab.test |
| Domain Controller IP | 192.168.240.130 |
| Client IP | 192.168.240.131 |
| DNS | Domain Controller |
| Tools | Active Directory Users and Computers, DNS, Windows command line |

> These addresses are lab-only private addresses. Lab changes are performed inside the VMs.

## Verified Hands-on Tasks

- Installed/configured Active Directory Domain Services in the virtual server lab.
- Confirmed the AD DS service was running.
- Configured the domain controller's lab network settings.
- Verified DNS resolution for the lab domain.
- Joined the Windows client to `adlab.test`.
- Verified domain identity with `whoami`.
- Created a test Organizational Unit.
- Created a test user.
- Disabled and enabled the test account.
- Reset a test user's password.

## Skills Practiced

- Windows Server fundamentals
- Active Directory Domain Services
- Domain and user account administration
- Organizational Units
- DNS basics and domain name resolution
- Domain joining
- User account lifecycle
- Password reset and account status troubleshooting
- Windows command-line verification
- Virtual machine networking and isolation

## Troubleshooting Practice — Planned

These scenarios will be completed and documented with actual steps and evidence:

1. User cannot log in — check account status, password, domain, and connectivity.
2. Client cannot find the domain — verify DNS configuration and name resolution.
3. Domain join fails — verify DNS, network connectivity, domain name, and credentials.
4. Account is locked or disabled — identify status and follow an authorized unlock/enable workflow.
5. No internet connectivity in a VM — check IP, gateway, DNS, and connectivity in sequence.
6. Slow Windows system — check CPU, memory, disk, startup applications, and event logs.
7. Printer or peripheral issue — practice a structured support workflow.
8. Windows service issue — inspect service status and relevant event logs.

## Useful Verification Commands

```powershell
ipconfig /all
ping 192.168.240.130
nslookup adlab.test
whoami
hostname
systeminfo
Get-Service
```

## Evidence and Documentation

Add screenshots and concise notes for completed troubleshooting scenarios. Only mark tasks complete after the lab result is verified.

## Project Status

- [x] AD DS lab configured
- [x] Domain client joined
- [x] DNS resolution verified
- [x] Test user created
- [x] Account disable/enable practiced
- [x] Password reset practiced
- [ ] Troubleshooting scenarios documented with evidence
- [ ] Network troubleshooting exercises completed
- [ ] Final interview Q&A and ticket-style case notes added

## Safety

All work is performed in authorized virtual machines. The lab network is separate from production systems; verify VM networking before making changes.
