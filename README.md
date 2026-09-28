# # Active Directory Home Lab

Built a virtual Windows domain environment to practice the account management, networking, and troubleshooting tasks handled by IT help desk and system administration teams.

**Tools:** Windows Server 2022 (or 2019) · Windows 10/11 Pro · Active Directory Domain Services · DNS · DHCP · RAS/NAT · PowerShell · Oracle VirtualBox

---

## Network Diagram

![Network diagram](images/network-diagram.png)

<!-- Make this in draw.io (free). Show: Internet → DC01 (NIC 1: NAT) → DC01 (NIC 2: Internal, 172.16.0.1) → CLIENT1 (DHCP address) -->

| Machine | Role | Network | IP |
|---|---|---|---|
| DC01 | Domain controller, DNS, DHCP, NAT router | NAT + Internal | 172.16.0.1 (internal, static) |
| CLIENT1 | Domain-joined workstation | Internal only | Assigned by DHCP |

**Domain:** `mydomain.com`

---

## What I Built

1. **Created two virtual machines** in VirtualBox: a server with two network adapters (internet-facing NAT and a private internal network) and a client on the internal network only.
2. **Installed Windows Server**, assigned a static IP to the internal adapter, and renamed the machine.
3. **Installed Active Directory Domain Services** and promoted the server to a domain controller for a new forest.
4. **Created a domain admin account** and organized accounts into Organizational Units (OUs).
5. **Configured RAS/NAT** so internal clients reach the internet through the domain controller.
6. **Configured DHCP** with a scope for the internal network so clients receive addresses automatically.
7. **Bulk-created 1,000+ users** with a PowerShell script (see [`scripts/`](scripts/)).
8. **Joined the Windows client to the domain** and logged in as a created domain user.

![Screenshot: Server Manager with AD DS installed](images/01-adds-installed.png)
![Screenshot: Users in Active Directory Users and Computers](images/02-users-created.png)
![Screenshot: DHCP scope and leased addresses](images/03-dhcp-leases.png)
![Screenshot: Client joined to domain](images/04-domain-join.png)
![Screenshot: Logged in as domain user](images/05-domain-login.png)

---

## Help Desk Scenarios Practiced

<!-- Fill this in after the video. This section is what makes your lab stand out. Delete any you didn't do. -->

| Ticket | What I did |
|---|---|
| User forgot password | Reset the password in ADUC and required a change at next logon |
| Account locked out | Unlocked the account and reviewed the lockout policy |
| Employee left the company | Disabled the account and moved it to a "Disabled Users" OU |
| User can't access shared folder | Created a security group, added the user, and set NTFS/share permissions |
| Client can't reach the internet | Diagnosed with `ipconfig`, `ping`, and `nslookup`; found and fixed the misconfiguration |

### Group Policy

- Enforced a domain password policy (length, complexity, lockout threshold)
- Mapped a network drive for all users in an OU
- Restricted Control Panel access for standard users

---

## Problems I Ran Into

<!-- The most valuable section. Write real issues in this format. -->

**Problem:** _e.g., Client received a 169.254.x.x address and couldn't join the domain._
**Cause:** _e.g., DHCP scope wasn't activated / client adapter was on the wrong VirtualBox network._
**Fix:** _What you changed and how you confirmed it worked._

---

## What I Learned

- How Active Directory, DNS, and DHCP depend on each other in a domain environment
- How domain join and authentication work between a client and a domain controller
- Using PowerShell to automate repetitive administration tasks
- <!-- Add your own -->

---

## Next Steps

- [ ] Add a ticketing system (osTicket) and log lab tickets against it
- [ ] Add a second domain controller for redundancy
- [ ] Explore AD security basics (auditing logons, reviewing event logs)

---

## Credit

Initial build based on [Josh Madakor's Active Directory home lab tutorial](https://www.youtube.com/watch?v=MHsI8hJmggI). Help desk scenarios, Group Policy configuration, and troubleshooting were added independently.
