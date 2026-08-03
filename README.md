
---

```markdown
# Cloud Governance Gone Rogue – Azure Policy Lab

**Course:** CST8919 – DevOps Security and Compliance  
**Repository:** `25S_CST8919_Lab_3`  
**Video Demo:** (https://youtu.be/k9xfjK2MX5c)

---

## 1. Scenario & Lab Overview

At **MapleTech Solutions**, rapid growth led to uncontrolled cloud resource provisioning. Developers were deploying resources across unauthorized global regions, omitting required operational tags, and creating publicly exposed IP addresses.

As a Cloud Security Engineer, 
---

## 2. Policy Definitions

Three custom Azure Policies were authored in JSON with a `deny` effect to enforce security guardrails:

1. **`Only-CanadaCentral`**: Restricts resource deployments exclusively to the Canada Central region.
2. **`Require-ProjectName-Tag`**: Denies deployment of any resource that lacks the mandatory ProjectName tag.
3. **`Deny-Public-IP`**: Prevents the creation of public-facing network interfaces 

These three policies were grouped into an Initiative named **`MapleTech Secure Foundation`** and assigned to the target resource group with enforcement enabled.

---

## 3. Test Cases & Enforcement Summary

| Test Case | Scenario | Expected Outcome | Actual Result | Evidence |
| :--- | :--- | :--- | :--- | :--- |
| **Test Case 1** | Deploy VM in `East US` |  Denied | Denied by `Only-CanadaCentral` | `screenshots/test1-vm-eastus-denied.png` |
| **Test Case 2** | Deploy Storage Account without `ProjectName` tag | Denied | Denied by `Require-ProjectName-Tag` | `screenshots/test2-storage-notag-denied.png` |
| **Test Case 3** | Create a Public IP Address in `Canada Central` |  Denied | Denied by `Deny-Public-IP` | `screenshots/test3-publicip-denied.png` |
| **Test Case 4** | Deploy VM in `Canada Central` with `ProjectName` tag & no Public IP |  Allowed | Passed pre-flight validation & provisioned | `screenshots/test4-vm-compliant-allowed.png` |

---


---

## 5. Challenges & Lessons Learned

* **Policy Assignment Propagation:** Azure Policy  initiative assignment take 15 to 30 minutes to fully replicate across the Azure control plane. Testing quickly after assignment can result in false positive crration
* **Indexed vs. All Policy Modes:** Selecting the correct evaluation mode (`Indexed for tagged/located resources vs. All for resource types without location tags like public IP) is essential for proper rule evaluatio


```

```
