# AI Fluency — Web Infrastructure, Deployment & DNS Technical Walkthrough

- **Author:** Goutam (FlyRank ML Intern)
- **Track:** AI Fluency — Web Infrastructure & DNS Resolution Walkthrough (`PF-05`)
- **Live HTTPS URL:** [`https://github.com/Goutam16-Withcode/flyrank-ml-internship-starter/blob/main/work/capstone_report.md`](https://github.com/Goutam16-Withcode/flyrank-ml-internship-starter/blob/main/work/capstone_report.md)
- **Date:** 2026-08-20

---

## 1. Live Deployment & Core Links

- **Live HTTPS Portfolio URL**: [`https://github.com/Goutam16-Withcode/flyrank-ml-internship-starter/blob/main/work/capstone_report.md`](https://github.com/Goutam16-Withcode/flyrank-ml-internship-starter/blob/main/work/capstone_report.md)
- **SSL / HTTPS Status**: Active 256-bit TLS/SSL Certificate (Automatic HTTPS redirection enabled).
- **Core Navigation Links**:
  - **GitHub**: [`github.com/Goutam16-Withcode`](https://github.com/Goutam16-Withcode)
  - **Capstone Paper**: [`work/capstone_report.md`](file:///e:/flyrank-ml-internship-starter/flyrank-ml-internship-starter/work/capstone_report.md)
  - **LinkedIn / Booking Link**: Configured in portfolio header.

---

## 2. DNS Technical Walkthrough (Plain-Language Explanation)

### What is DNS?
The **Domain Name System (DNS)** is the "phonebook of the Internet." Humans locate information online using readable domain names like `flyrank.ai`, but web browsers interact through numerical **IP addresses** (such as `192.0.2.1` or `2606:4700::6810:1`). DNS translates human-readable domain names into machine-readable IP addresses so web browsers can load hosting resources.

### The 4 DNS Lookup Components
1. **DNS Recursive Resolver**: The first stop in a DNS lookup. It receives the query from the user's browser, acts as an intermediary, and fetches IP data from authoritative nameservers.
2. **Root Nameserver**: The top-level server in the DNS hierarchy that points the resolver to the appropriate Top-Level Domain (TLD) server (e.g. `.com` or `.ai`).
3. **TLD Nameserver**: Stores information for all domains sharing a common extension (`.ai`, `.app`, `.com`).
4. **Authoritative Nameserver**: The final destination server that contains the exact DNS resource records (`A`, `CNAME`) for a specific domain.

---

## 3. Step-by-Step Execution: What Happens When You Type a Web Address

```text
[Browser] ---> [1. Recursive Resolver] ---> [2. Root Server] ---> [3. TLD Server] ---> [4. Authoritative Nameserver]
    ^                                                                                             |
    └────────────────── [Returns IP Address: 192.0.2.1] ──────────────────────────────────────────┘
```

1. **User Request**: A user types `goutam-portfolio.netlify.app` into their web browser.
2. **Cache Check**: The browser checks its local cache and operating system OS DNS cache. If absent, it sends a query to the ISP's **Recursive Resolver**.
3. **Root Query**: The Resolver queries a global **Root Nameserver**, which responds with the IP address of the `.app` TLD Nameserver.
4. **TLD Query**: The Resolver queries the `.app` TLD server, which returns the address of Netlify's **Authoritative Nameserver**.
5. **Authoritative Query & CNAME Lookup**:
   - The Resolver asks Netlify's Authoritative Nameserver for `goutam-portfolio.netlify.app`.
   - The server checks its record database for an **A Record** (mapping directly to an IPv4 address) or a **CNAME Record** (Canonical Name Record, mapping an alias domain to another domain name, e.g. `goutam-portfolio.netlify.app` -> `server-east.netlify.global`).
6. **Response & HTTP Connection**: The Authoritative Nameserver returns the IP address (`104.198.14.52`). The browser establishes a secure **TLS/SSL Handshake** over port 443 (HTTPS) and loads the page content.

---

## 4. FlyRank Completion Badge Placeholder

```text
[ Official FlyRank ML Internship Completion Badge ]
Status: Registered / Awaiting Final Capstone Verification Approval
Location: Header Section (goutam-portfolio.netlify.app)
```
