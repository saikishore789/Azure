Great question! Let's break this down clearly:

---

## 🌐 What is an **Availability Set** in Azure?

An **Availability Set** is a logical grouping of Virtual Machines (VMs) in Azure that helps ensure your application remains available during:

- **Planned maintenance** (like OS updates)
- **Unplanned hardware failures**

When you place VMs in an availability set, Azure distributes them across multiple **fault domains** and **update domains** to reduce the risk of downtime.

---

## 🧱 What is a **Fault Domain (FD)?**

A **Fault Domain** represents a group of hardware that shares:

- A common power source
- A common network switch

If a physical failure (like a power outage or switch failure) occurs, **only the VMs in that fault domain are affected**.

### Example:
If you have 3 fault domains and 3 VMs, Azure will place each VM in a different fault domain. So, even if one domain fails, the other two VMs continue running.

---

## 🔄 What is an **Update Domain (UD)?**

An **Update Domain** is a group of VMs that are **updated or rebooted together** during planned maintenance.

Azure updates **one update domain at a time**, ensuring that not all VMs go down simultaneously.

### Example:
If you have 5 update domains and 5 VMs, each VM is placed in a different update domain. During maintenance, Azure updates one domain at a time, keeping the rest running.

---

## ✅ Summary of Maximums:

| Feature           | Maximum |
|------------------|---------|
| Fault Domains     | **3**   |
| Update Domains    | **20**  |

