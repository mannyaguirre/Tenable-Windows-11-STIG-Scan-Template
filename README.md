# Advanced Network Scan - DISA STIG: Windows 11 VM

<img width="702" height="342" alt="TenableStigs" src="https://github.com/user-attachments/assets/bac62962-146e-4394-9de2-c13c3d1a794b" />

---

## Overview

The purpose of this lab was to create an ***Advanced Network Scan with a DISA STIG Template***. The benefit of using a DISA STIG template is to measure an organization's security posture against the DISA STIG's security standards. ***DISA ( Defense Information Systems Agency)*** is an agency under the U.S Department of Defense. DISA publishes ***STIGs (Security Technical Implementation Guide)***. Organizations working under DoD environments, systems or contracts are expected to follow DISA STIGs security requirements to help ensure compliance with DoD's security standards. Other organizations not working within DoD environments may use DISA STIGs as a strong security baseline.

In this lab I provisioned a Windows 11 VM. I created vulnerabilities inside the virtual machine to measure those vulnerabilities against DISA STIG standards. Created an Advanced Network Scan with a DISA STIG template for Windows 11. Launched the scan. Reviewed the results. Performed a clean up of the environment.

This lab was performed in a controlled environment using an intentionally misconfigured Windows 11 VM.

> **Security Note:**  
> The vulnerabilities created in this lab, such as disabling the firewall, enabling insecure accounts and using blank passwords, should never be used in a production environment. These were configured only for educational testing inside a temporary lab environment.

---

## Lab Objectives

By the end of this lab I was able to:

- Provision a Windows 11 VM.
- Create vulnerabilities inside of the VM.
- Create an Advanced Network Scan.
- Check compliance using DISA STIG.
- Review results of scan.
- Measure the vulnerabilities against DISA STIGs.
- Perform environment clean up.

---

## Tools Used

- Tenable Vulnerability Management
- Microsoft Azure
- Windows 11 Virtual Machine
- DISA STIG
- Remote Desktop Connection (RDC)
- Advanced Network Scan

---

## Lab Environment

| Component | Description |
|---|---|
| Endpoint | Windows 11 Virtual Machine |
| Scanner Type | User Defined |
| Scan Type | Advanced Network Scan DISA STIG Windows 11 |
| Platform | Tenable Vulnerability Management |
| Platform | Microsoft Azure |

---

## Lab Steps

### Step 1: Provision Windows 11 Virtual Machine

The first step in this lab was to configure a Windows 11 Virtual Machine using Microsoft Azure shown in ***Exhibit 1***.

### Why This Matters?

The virtual machine will serve as our endpoint for the Advanced Network Scan.

### Exhibit 1

<img width="1918" height="918" alt="Lab1" src="https://github.com/user-attachments/assets/be50c01f-304a-4a9e-820b-1bdac23db168" />

---

### Step 2: Create Vulnerabilities Inside Virtual Machine

The second step was to create vulnerabilities inside the virtual machine ***Exhibits 2, 3, 4 and 5***.

### Why This Matters?

The vulnerabilities needed to be created so that the Advanced Network Scan could detect the vulnerabilities and measure them against DISA STIG standard. 

The vulnerabilities created are outlined below:

- Disabled firewall.
- Created new administrator account with blank password.
- New adminstrator password was set to never expire.
- Added administrator account to administrator group.
- Enabled Guest account.
- Set Guest account password to blank.
- Guest account password was set to never expire.
- Added Guest account to admistrator group.

### Exhibit 2

<img width="1582" height="950" alt="Lab2" src="https://github.com/user-attachments/assets/05accee2-3067-420b-87f7-cf9214b7f3dd" />

### Exhibit 3

<img width="1580" height="936" alt="Lab3" src="https://github.com/user-attachments/assets/7e33112b-525a-4bc7-be2a-ff8fe7db5a23" />

### Exhibit 4

<img width="1587" height="943" alt="Lab4" src="https://github.com/user-attachments/assets/a9c067f4-b7cb-4186-a0f5-fd1f6d9e8592" />

### Exhibit 5

<img width="1327" height="872" alt="Lab3 1" src="https://github.com/user-attachments/assets/c3ea2a5e-40b2-4337-9fe3-4b5f1fc91a4f" />

---

### Step 3: Create Advanced Network Scan with DISA STIG Template

The third step was to create the Advanced Network Scan with DISA STIG Compliance ***Exhibits 6, 7, 8, 9, 10 and 11***. The Advanced Network Scan was launched by using an Advanced Network Scan template. 

The steps to create the template and launch the scan are outlined below:

1. cloud.tenable.com
2. Scans
3. Vulnerability Management Scans
4. Create Scan Template ***Exhibit 6***
5. Advanced Network Scan ***Exhibit 7***
6. Under Compliance choose **DISA Microsoft Windows 11 STIG v2r7** ***Exhibit 8***
7. Scans
8. Vulnerability Management Scans
9. Create Scan
10. User Define ***Exhibit 9***
11. Advanced Network Scan - DISA STIG: Windows 11 VM ***Exhibit 10***
12. Private IP set to ```10.1.0.116``` and launch ***Exhibit 11***

### Why This Matters?

The scan was created so that Tenable could detect the vulnerabilities created inside the VM and measure them against DISA STIG.

### Exhibit 6

<img width="1918" height="925" alt="Lab5" src="https://github.com/user-attachments/assets/688df4dd-aed6-4bc3-a0dd-110e8dd17ec6" />

### Exhibit 7

<img width="1918" height="922" alt="Lab6" src="https://github.com/user-attachments/assets/bf276f8f-9532-42d0-90bf-40c440e3c8fa" />

### Exhibit 8

<img width="1918" height="920" alt="Lab7" src="https://github.com/user-attachments/assets/2401a560-f18c-46c1-b65b-43667f0dfd53" />

### Exhibit 9

<img width="786" height="678" alt="Lab8" src="https://github.com/user-attachments/assets/ab13bbd3-ab35-495b-a9e6-1f50bb9c152a" />

### Exhibit 10

<img width="1918" height="912" alt="Lab9" src="https://github.com/user-attachments/assets/b8554211-fe21-48b0-af3d-66e665a2104e" />

### Exbibit 11

<img width="1918" height="912" alt="Lab9" src="https://github.com/user-attachments/assets/b69ff7af-2d95-4044-9b83-34ff9148ea88" />


---

### Step 4: Review Scan Results

The fourth step was to review the results of the scan and observe the vulnerabilities. The scan took approximately 34 minutes and yielded the following results:

| Severity | Vulnerabilities |
|---|---|
| High | 5 |
| Medium | 3 |
| Low | 2 |

The results showed the vulnerabilities that were found, the description for each vulnerability, the affected assets, the risk information such as CVSS scores, the solution to remediate the vulnerability and an optional executive PDF summary.

### Why This Matters?

It is important to review the results of scans to learn about any possible vulnerabilities an organization may have and take the necessary steps to implement the organization's **Playbook** if necessary.

### Exbibit 12

<img width="1918" height="918" alt="Lab10" src="https://github.com/user-attachments/assets/372e6528-4970-4267-8cd6-7548fecd3c85" />

### Exbibit 13

<img width="1918" height="917" alt="Lab11" src="https://github.com/user-attachments/assets/a7b78f39-682e-4167-84bd-eaf4abf070b2" />

### Exbibit 14

<img width="1918" height="916" alt="Lab12" src="https://github.com/user-attachments/assets/9b6aeb6c-1b81-4c57-b3a0-5a1dfd201c67" />

### Exbibit 15

<img width="1918" height="915" alt="Lab13" src="https://github.com/user-attachments/assets/e898d45e-004d-4e49-ad41-55db482a26e9" />

### Exbibit 16

<img width="846" height="585" alt="Lab14" src="https://github.com/user-attachments/assets/88665074-6380-43eb-8ce0-fd51d44b87bc" />



### Step 5: Clean Up

The final step was to perform cleanup by deleting the virtual machine to prevent unnecessary resource usage and wipe the vulnerabilities created in the lab.

---

## Key Takeaways

- DISA STIGs measure an organization's security posture against the DISA STIG's security standards.
- Organizations working under DoD environments are expected to follow DISA STIGs security requirements.
- The vulnerabilities created in this lab are not to be replicated in live production.
- User is able to reuse DISA STIG template for future scans. 
---

## Conclusion

In this lab I successfully created and launched an Advanced Network Scan with a DISA STIG Template. I was able to measure the failed audits of the scan against DISA STIGs security measurements and observe how the vulnerabilities created inside the lab affected our virtual machine. This lab was only for creation and observation. Remediation is completed in others labs.

```
Author        : Manuel Aguirre
LinkedIn      : linkedin.com/in/mannyaguirre/
GitHub        : github.com/mannyaguirre
Date Created  : May 1, 2026
Last Modified : May 13, 2026
Version       : 1.0
