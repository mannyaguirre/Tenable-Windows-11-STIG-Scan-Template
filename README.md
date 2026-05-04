# Using a Scan Template to Scan a Windows 11 VM

<img width="698" height="333" alt="Screenshot 2026-05-04 141200" src="https://github.com/user-attachments/assets/528b7299-bb9f-41c5-9b93-4cbbbc3322a7" />


## Overview

In this lab, I created a Windows 11 virtual machine and used a custom Tenable scan template to perform a vulnerability and compliance scan. The goal was to practice configuring scan templates, using credentialed scanning, observing vulnerability results, reviewing compliance audit findings, and identifying remediation recommendations.

This lab was performed in a controlled environment using an intentionally misconfigured Windows 11 VM.

> **Security Note:**  
> The vulnerable settings used in this lab, such as disabling the firewall, enabling insecure accounts, using blank passwords, and opening inbound network access, should never be used in a production environment. These were configured only for educational testing inside a temporary lab environment.

---

## Lab Objective

The objective of this lab was to:

- Create a Windows 11 VM
- Intentionally weaken the VM security posture for testing
- Configure a Tenable Advanced Network Scan template
- Add DISA Windows 11 STIG compliance auditing
- Launch a credentialed vulnerability and compliance scan
- Review vulnerabilities, audit results, and remediation guidance
- Remove the lab environment after testing

---

## Tools Used

- Microsoft Azure
- Windows 11 Virtual Machine
- Tenable
- Advanced Network Scan Template
- DISA Microsoft Windows 11 STIG Compliance Audit
- Network Security Group, or NSG
- Windows Administrator Account
- Ping/ICMP testing

---

## Lab Environment

| Component | Description |
|---|---|
| Target System | Windows 11 Virtual Machine |
| Scanner | Tenable |
| Scan Type | Advanced Network Scan |
| Compliance Framework | DISA Microsoft Windows 11 STIG |
| Authentication | Credentialed scan using local administrator credentials |
| Network Configuration | NSG opened for inbound testing |

---

## High-Level Lab Steps

1. Create a Windows 11 Virtual Machine.
2. Disable the Windows Firewall.
3. Create intentional vulnerabilities for Tenable to detect.
4. Enable insecure local accounts.
5. Open the Azure NSG to allow inbound traffic.
6. Test connectivity from a personal computer using ping.
7. Create a Tenable scan template.
8. Configure scan discovery, assessment, credentials, compliance, and plugins.
9. Save the scan template.
10. Create a new scan using the template.
11. Launch the scan against the Windows 11 VM.
12. Review vulnerabilities, compliance audits, and remediation results.
13. Delete the Windows 11 VM after completing the lab.

---

## Step 1: Create a Windows 11 Virtual Machine

I started by creating a Windows 11 virtual machine in Microsoft Azure.

The VM was used as the target system for the Tenable scan.

<img width="1897" height="971" alt="Lab1" src="https://github.com/user-attachments/assets/6816f55d-f5f7-4e5f-ad21-7fc197a5dc21" />

## Step 2: Disable Windows Firewall

After logging into the Windows 11 VM, I disabled the Windows Firewall to allow the scanner to communicate more freely with the target system.

This helped confirm that network restrictions would not prevent Tenable from discovering and scanning the host.

> **Note:** In a real production environment, the Windows Firewall should remain enabled and properly configured. This was done only for lab testing.

<img width="1560" height="982" alt="Lab2" src="https://github.com/user-attachments/assets/cf2c9cb1-9af0-4370-bcd6-b54b42076703" />

## Step 3: Create Intentional Vulnerabilities

To give Tenable something meaningful to detect, I intentionally weakened the Windows 11 VM’s security configuration.

The purpose of this step was to create insecure account settings that could be identified during the vulnerability and compliance scan.

The following insecure configurations were created:

| Configuration | Purpose in Lab |
|---|---|
| Enabled the local `administrator` account | Created a privileged local account for credentialed scanning |
| Set a blank password with no expiration | Created an intentionally weak authentication condition |
| Added the `administrator` account to the local `administrators` group | Ensured the account had administrative privileges |
| Enabled the local `guest` account | Created an additional insecure account |
| Added the `guest` account to the local `administrators` group | Created a high-risk privilege misconfiguration |
| Configured the guest account with no password | Created another weak authentication condition |

These settings are intentionally insecure and were configured only for this temporary lab environment.

> **Security Warning:**  
> Blank passwords, enabled guest accounts, and unnecessary administrative privileges create serious security risks. These settings should never be used in a production environment.

<img width="1232" height="872" alt="Lab3" src="https://github.com/user-attachments/assets/d9a05505-ffc0-4e6a-8f08-c7fac1dc3481" />

## Step 4: Open the Network Security Group

Next, I configured the Azure Network Security Group, also known as the NSG, to allow inbound traffic to the Windows 11 VM.

The purpose of this step was to make sure Tenable could reach the target system during the vulnerability and compliance scan.

| Configuration | Purpose in Lab |
|---|---|
| Opened inbound traffic on the NSG | Allowed the scanner to communicate with the VM |
| Allowed network access to the VM’s public IP address | Made the target reachable from outside the Azure environment |
| Prepared the VM for connectivity testing | Confirmed that network traffic was not being blocked before scanning |

> **Security Warning:**  
> Opening inbound traffic to a virtual machine is dangerous in a real environment. This should only be done in a controlled lab environment and should be removed immediately after testing.

<img width="1918" height="954" alt="Lab4" src="https://github.com/user-attachments/assets/b59b69ae-0bf0-4df1-8c73-0e6ef6b3f747" />

## Step 5: Test Connectivity

From my personal computer, I tested connectivity to the Windows 11 VM by pinging the VM’s public IP address.

The purpose of this step was to confirm that the VM was reachable before launching the Tenable scan.

<img width="698" height="302" alt="Lab5" src="https://github.com/user-attachments/assets/80214522-6de8-48d9-a3e6-e95fccfebf89" />

## Step 6: Create a Tenable Scan Template

After confirming that the Windows 11 VM was reachable, I logged into Tenable and created a new scan template.

For this lab, I used the **Advanced Network Scan** template.

The purpose of this step was to create a reusable scan configuration that could be used to assess the Windows 11 VM for vulnerabilities and compliance issues.

| Template Setting | Purpose in Lab |
|---|---|
| Advanced Network Scan | Provided detailed scan configuration options |
| Custom scan name | Helped identify the scan template later |
| Credentialed scan options | Allowed Tenable to perform deeper checks |
| Compliance audit options | Allowed Tenable to compare the VM against STIG requirements |
| Plugin configuration | Controlled which vulnerability and compliance checks were enabled |

---

### Basic Settings

In the **Basic** section, I configured the scan name and enabled options that allowed Tenable to start important Windows services during the scan.

| Setting | Status |
|---|---|
| Name | `Win-11-STIG-test` |
| Start the Remote Registry service during the scan | Enabled |
| Enable administrative shares during the scan | Enabled |
| Start the Server service during the scan | Enabled |

These settings helped Tenable perform a more complete authenticated scan of the Windows 11 VM.

<img width="1915" height="905" alt="Lab6" src="https://github.com/user-attachments/assets/b3e744d9-b11c-4d55-9ebd-2638ad91e788" />

### Discovery Settings

In the **Discovery** section, I enabled host discovery and TCP scanning options.

The purpose of this section was to help Tenable identify the Windows 11 VM, confirm that the host was reachable, and determine which network services could be scanned.

| Discovery Setting | Status | Purpose |
|---|---|---|
| Ping the remote host | Enabled | Confirms the target host is reachable before scanning |
| Use fast network discovery | Enabled | Speeds up the host discovery process |
| Network Port Scanners: TCP | Enabled | Allows Tenable to scan TCP ports and identify reachable services |

These settings helped confirm that Tenable could communicate with the Windows 11 VM before performing deeper vulnerability and compliance checks.

<img width="1918" height="925" alt="Lab7" src="https://github.com/user-attachments/assets/e82ab237-2413-49e0-a5f9-4babfaa7b3f9" />

### Assessment Settings

In the **Assessment** section, I enabled the settings needed for a deeper vulnerability scan of the Windows 11 VM.

The purpose of this section was to allow Tenable to perform more detailed checks against the target system instead of only running a basic scan.

| Assessment Setting | Status | Purpose |
|---|---|---|
| Perform thorough tests | Enabled | Allows Tenable to run more detailed vulnerability checks |
| Only use credentials provided by the user | Unchecked | Allows Tenable to use additional scan methods beyond only the provided credentials |

Enabling **Perform thorough tests** helped Tenable perform a more complete assessment of the Windows 11 VM.

Leaving **Only use credentials provided by the user** unchecked allowed the scanner to perform additional checks when applicable.

<img width="1917" height="937" alt="Lab8" src="https://github.com/user-attachments/assets/91fc17cd-e3a6-4aa7-9549-a0b61bbdbb3d" />

### Credential Settings

In the **Credentials** section, I entered the local administrator credentials that were configured earlier in the lab.

The purpose of this section was to allow Tenable to authenticate into the Windows 11 VM and perform a deeper credentialed scan.

| Credential Setting | Purpose |
|---|---|
| Windows credentials | Allowed Tenable to authenticate to the target VM |
| Local administrator account | Provided the permissions needed for deeper system checks |
| Credentialed scan access | Allowed Tenable to inspect local configuration, registry settings, security policies, and compliance settings |

Credentialed scanning provides more detailed results than an unauthenticated scan because Tenable can inspect the system from the inside instead of only scanning exposed network services.

<img width="1918" height="803" alt="Lab9" src="https://github.com/user-attachments/assets/f16ed30b-6f89-4c52-a107-23cc5ae4309f" />

### Compliance Settings

In the **Compliance** section, I added a Windows 11 DISA STIG audit file.

The purpose of this section was to allow Tenable to compare the Windows 11 VM’s configuration against a recognized security baseline.

<img width="1907" height="842" alt="Lab10" src="https://github.com/user-attachments/assets/00c3a6a0-db35-47f8-9fff-58001e094291" />

### Plugin Settings

In the **Plugins** section, I enabled the plugin families needed for Windows vulnerability and compliance scanning.

The purpose of this section was to control which types of checks Tenable would run against the Windows 11 VM.

| Plugin Family | Status | Purpose |
|---|---|---|
| General | Enabled | Runs general vulnerability and system checks |
| Policy Compliance | Enabled | Supports compliance audit checks |
| Windows Compliance Checks | Enabled | Checks Windows-specific compliance settings |
| Settings | Enabled | Reviews system and scan-related configuration issues |
| Windows | Enabled | Runs Windows-specific vulnerability checks |
| Windows: Microsoft Bulletins | Enabled | Checks for Microsoft security bulletin-related vulnerabilities |
| Windows: User Management | Enabled | Reviews Windows user account and group configuration issues |

These plugin families helped Tenable identify Windows vulnerabilities, user management issues, security misconfigurations, missing security controls, and compliance findings.

<img width="1918" height="682" alt="Lab11" src="https://github.com/user-attachments/assets/39d4c33a-48af-479c-89b7-9a64fdf61562" />

## Step 7: Save the Scan Template

After configuring the scan template settings, I saved the Tenable scan template.

The purpose of this step was to create a reusable scan configuration that could be used later for similar Windows 11 vulnerability and compliance scans.

| Action | Purpose |
|---|---|
| Reviewed the scan template settings | Confirmed the scan was configured correctly before saving |
| Saved the scan template | Created a reusable scanning configuration |
| Reused the template for a new scan | Reduced the need to manually configure the same settings again |

Saving the template helps standardize the scanning process and keeps the scan configuration consistent across future assessments.

## Step 8: Create a New Scan from the Template

After saving the scan template, I created a new scan using the template I configured earlier.

The purpose of this step was to apply the saved scan configuration to the Windows 11 VM target.

| Action | Purpose |
|---|---|
| Selected the saved scan template | Reused the scan settings configured earlier |
| Created a new scan | Prepared a scan job for the Windows 11 VM |
| Entered the VM IP address | Set the Windows 11 VM as the scan target |
| Verified credentials | Confirmed Tenable could attempt a credentialed scan |
| Reviewed scan settings | Checked the configuration before launching the scan |

Using a saved template made the scan setup faster and helped keep the configuration consistent.

<img width="1918" height="872" alt="Lab12" src="https://github.com/user-attachments/assets/e13badc7-46f1-4f79-bd4d-e6938bad0b23" />

## Step 9: Launch the Scan

After creating the new scan from the saved template, I launched the scan against the Windows 11 VM.

The purpose of this step was to allow Tenable to assess the target system using the configured discovery, assessment, credential, compliance, and plugin settings.

| Action | Purpose |
|---|---|
| Launched the scan | Started the vulnerability and compliance assessment |
| Targeted the Windows 11 VM IP address | Directed Tenable to scan the correct system |
| Used the saved scan template | Applied the previously configured scan settings |
| Allowed the scan to complete | Gave Tenable time to perform discovery, authentication, vulnerability checks, and compliance checks |

During the scan, Tenable attempted to communicate with the VM, authenticate using the provided credentials, identify vulnerabilities, and evaluate the system against the selected DISA STIG compliance audit.

<img width="1918" height="975" alt="Lab13" src="https://github.com/user-attachments/assets/0516454d-24ae-4d4c-b4b4-8c3a4f54b839" />

## Step 10: Review Scan Results

After the scan completed, I reviewed the results in Tenable.

The purpose of this step was to analyze what Tenable discovered during the vulnerability and compliance scan.

| Result Section | Purpose |
|---|---|
| Vulnerabilities | Shows security issues detected on the Windows 11 VM |
| Vulns by Plugin | Groups findings by the Tenable plugin that detected them |
| Audits | Shows compliance results from the DISA Windows 11 STIG audit |
| Remediations | Provides recommended actions to fix the detected issues |

Reviewing the results helped me understand the security posture of the Windows 11 VM and identify which issues needed remediation.

<img width="1918" height="973" alt="Lab14" src="https://github.com/user-attachments/assets/e3ca32d4-e911-4747-8052-509a1430dce4" />

<img width="1918" height="977" alt="Lab15" src="https://github.com/user-attachments/assets/b1c54531-7d8a-4603-90cd-340c3702827a" />

<img width="1918" height="980" alt="Lab16" src="https://github.com/user-attachments/assets/3a041774-f55a-4d9e-8f0c-cc7d962b9763" />

## Key Takeaways

This lab demonstrated how Tenable can be used to perform both vulnerability scanning and compliance auditing against a Windows 11 virtual machine.

The main lesson from this lab was that credentialed scans provide deeper visibility than unauthenticated scans because Tenable can inspect the system configuration directly.

| Takeaway | Explanation |
|---|---|
| Credentialed scans provide better visibility | Tenable can review local settings, registry values, user accounts, services, and compliance controls |
| Scan templates improve consistency | A saved template allows the same scan settings to be reused for similar systems |
| Compliance audits help identify configuration weaknesses | DISA STIG audits compare the system against a defined security baseline |
| Weak account settings create serious risk | Blank passwords, enabled guest accounts, and excessive administrator privileges increase exposure |
| NSG rules affect scan success | If traffic is blocked, Tenable may not detect the host or complete the scan properly |
| Plugin selection matters | Enabled plugins determine what Tenable checks during the scan |
| Remediation review is important | Scan results are only useful if the findings are reviewed and acted on |
| Cleanup is part of the lab process | Removing vulnerable cloud resources helps reduce risk and avoid unnecessary costs |

### Skills Practiced

This lab helped me practice:

- Creating a Windows 11 VM in Azure
- Configuring a Tenable scan template
- Performing credentialed vulnerability scanning
- Adding DISA Windows 11 STIG compliance audits
- Reviewing vulnerabilities by plugin
- Reviewing compliance audit results
- Understanding remediation recommendations
- Cleaning up intentionally vulnerable cloud resources

---

## Cleanup

After reviewing the scan results, I deleted the Windows 11 virtual machine from Azure.

The purpose of this step was to remove the intentionally vulnerable system from the environment and prevent unnecessary cloud charges.

| Cleanup Action | Purpose |
|---|---|
| Deleted the Windows 11 VM | Removed the vulnerable target system |
| Removed exposed resources | Reduced the risk of unwanted access |
| Stopped ongoing Azure costs | Prevented unnecessary charges |
| Closed the lab environment | Completed the testing process safely |

Because this VM was intentionally misconfigured, it was important to remove it after the lab was complete.

The VM had insecure settings such as:

- Disabled Windows Firewall
- Open inbound NSG rules
- Enabled local administrator account
- Blank password configuration
- Enabled guest account
- Guest account added to the administrators group

These settings should not remain active after testing.

> **Security Note:**  
> Any intentionally vulnerable lab system should be deleted, isolated, or restored to a secure state after testing is complete.

---

## Conclusion

In this lab, I created a Windows 11 virtual machine, intentionally configured insecure settings, built a Tenable Advanced Network Scan template, added a DISA Windows 11 STIG compliance audit, launched a credentialed scan, and reviewed the scan results.

This lab gave me hands-on practice with vulnerability management and compliance scanning.

The scan helped show how Tenable can identify:

- Vulnerabilities
- Weak user account settings
- Windows misconfigurations
- Compliance failures
- Remediation recommendations

The most important takeaway was understanding the value of credentialed scanning. By providing valid credentials, Tenable was able to perform deeper checks than it would during an unauthenticated scan.

This lab also reinforced the importance of safely cleaning up cloud resources after testing, especially when those resources were intentionally configured to be insecure.

Overall, this project helped strengthen my understanding of scan templates, credentialed scanning, Windows security configuration, DISA STIG compliance checks, and vulnerability remediation workflows.
