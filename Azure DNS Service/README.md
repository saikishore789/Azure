Azure DNS is a **high-performance, reliable, and scalable domain name system (DNS) hosting service** provided by Microsoft. It allows you to host your domain names and manage DNS records using the same credentials, APIs, and tools as other Azure services.

---

## 🌐 What Is Azure DNS?

Azure DNS lets you:
- Host your DNS domains in Azure
- Manage DNS records using Azure Portal, CLI, PowerShell, or SDKs
- Integrate with other Azure services like App Service, CDN, and Traffic Manager
- Use **Azure Private DNS** for internal name resolution within virtual networks

Azure DNS does **not** support domain registration—you must purchase domains from a registrar like GoDaddy or Namecheap and then delegate them to Azure DNS.

---

## 🧱 Key Concepts

### 1. **DNS Zone**
A DNS zone is a container for DNS records for a specific domain. For example, a zone for `contoso.com` might contain records for:
- `www.contoso.com`
- `mail.contoso.com`
- `api.contoso.com`

### 2. **DNS Records**
DNS records define how domain names are resolved. Azure DNS supports all standard record types.

---

## 📋 Common DNS Record Types with Examples

| Record Type | Purpose | Example |
|-------------|---------|---------|
| **A** | Maps domain to IPv4 address | `www.contoso.com → 52.183.88.22` |
| **AAAA** | Maps domain to IPv6 address | `api.contoso.com → 2001:0db8:85a3::8a2e:0370:7334` |
| **CNAME** | Aliases one domain to another | `shop.contoso.com → contoso.azurewebsites.net` |
| **MX** | Directs email to mail servers | `contoso.com → mail.contoso.com (priority 10)` |
| **NS** | Specifies authoritative name servers | `contoso.com → ns1-01.azure-dns.com` |
| **TXT** | Stores text info (e.g., verification) | `asuid.contoso.com → "abc123xyz"` |
| **SRV** | Specifies service location | `_sip._tcp.contoso.com → sipserver.contoso.com:5060` |
| **SOA** | Contains zone metadata | Includes primary name server, admin email, TTL |
| **PTR** | Reverse DNS lookup | `52.183.88.22 → www.contoso.com` |
| **CAA** | Restricts certificate authorities | `contoso.com → only lets Let's Encrypt issue certs` |

Sources: 

---

## 🛠️ Example: Hosting a Domain in Azure DNS

Let’s say you own `contoso.com` and want to host it in Azure DNS:

### Step 1: Create DNS Zone
- Go to Azure Portal → Create Resource → DNS Zone
- Name: `contoso.com`

### Step 2: Add Records
- A Record: `www.contoso.com → 52.183.88.22`
- CNAME: `blog.contoso.com → contoso.azurewebsites.net`
- MX: `contoso.com → mail.contoso.com`

### Step 3: Delegate Domain
- At your registrar, update name servers to:
  - `ns1-01.azure-dns.com`
  - `ns2-01.azure-dns.net`
  - `ns3-01.azure-dns.org`
  - `ns4-01.azure-dns.info`

---

## 🔒 Azure Private DNS

Use **Azure Private DNS** for internal name resolution:
- No public exposure
- Ideal for VMs, containers, and services within a VNet
- Example: `internal.contoso.local → 10.0.0.4`

---

