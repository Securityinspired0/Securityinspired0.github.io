---
layout: post
title: Linux System Enumeration and Monitoring System Processes
date: 2024-11-11
---


This lab is a part of my "Computer and Operating System" module where we explore fundamental concepts of system enumeration, privilege management on Linux systems. Through hands-on practice, I gained insight into how system administrators and security professionals can gather crucial system information, identify vulnerabilities, and monitor resources in real time. This blog reflects the key lessons and practical exercises from the lab.

**Objective:**
In this lab you will be introduced to:
* Enumerate a Linux operating system to gather crucial system information (kernel version, CPU architecture, running services).
* Identify user privileges, potential kernel vulnerabilities and weak file permissions.
* Identify possible exploits such as privilege escalation techniques (if applicable).
* Monitor in real-time processes and resources in a Linux VM

"This lab activity is based on Linux system enumeration and setting monitoring system processes tools as part of the portfolio 1 and you are required to complete all tasks and answer the questions."

**Lab setup:**
For this lab you'll need the Ubuntu Desktop 22.04 virtual machine. You can follow this link(https://securityinspired.medium.com/how-to-install-ubuntu-on-virtualbox-a-step-by-step-guide-3dc7032d388f) for instructions on installing Ubuntu and this link(https://releases.ubuntu.com/jammy/?_ga=2.157469628.786919307.1729614561-129726061.1707896173) for the 22.04 version specifically.

### <strong>Task 1: System Enumeration</strong>
System enumeration entails collecting critical information about a system, including details like the operating system version, kernel version, architecture, and active services.

1. Open a terminal in the virtualbox.
2. Use the following command to gather system information

<figure>
    <img src="/assets/img/uname.png" alt="Screenshot of the uname command output showing system information.">
    <figcaption><b>uname -a:</b> Displays the kernel version along with other system details.</figcaption>
</figure>

<figure>
    <img src="/assets/img/hostnamectl.png" alt="Screenshot of the operating system and architecture.">
    <figcaption><b>hostnamectl:</b> Shows information about the operating system and architecture.</figcaption>
</figure>

| ![Image 1](/assets/img/lscpu.png) | ![Image 2](/assets/img/lscpu1.png) |
|:-------------------------------:|:-------------------------------:|
|  **lscpu:** Provides detailed information about the CPU architecture.* |


### <strong>Task 2: User Enumeration</strong>
User enumeration helps in identifying the current user's roles and privileges within the system, which can provide insight into their access level and potential capabilities.

**Steps:**
Use the following commands to gather user information:

<figure>
    <img src="/assets/img/id.png" alt="Screenshot of the uname command output showing system information">
    <figcaption> <b>id:</b> Displays the user's UID, GID, and group membership.</figcaption>
</figure>

<figure>
    <img src ="/assets/img/whoami.png" alt="Screenshot showing the output of the whoami command">
    <figcaption><b>whoami:</b> Shows the current logged-in user</figcaption>
</figure>

<figure>
    <img src ="/assets/img/groups.png" alt="Screenshot showing the output of the groups command">
    <figcaption><b>groups:</b> Lists the groups the current user belongs to</figcaption>
</figure>

There are multiple questions to answer and these questions will help us gather information about the installed host.

* **Do you have an administrative privileges?**

<figure>
    <img src ="/assets/img/groups.png" alt="Screenshot showing the output of the groups command">
    <figcaption><b>sudo:</b> Grants administrative privileges, allowing the user to execute commands as the superuser or another user, as defined in the /etc/sudoers file.</figcaption>
</figure>

* **What groups does your account belong to?** The host is part of a group named "students".

* **What are your ID (UID) and group ID (GID)?** The UID is 1000 and the GID is 1000 associated with the group named "student".

* **Is your account part of any administrative groups like sudo?** Yes

* **How many groups are on the system?**
<img src ="/assets/img/group-count.png" alt="Screenshot showing the output of the group counts command">

* **How many users are on the system?**
<figure>
    <img src ="/assets/img/passwd.png" alt="Screenshot showing the output of the user counts command">
    <figcaption>Not all entries in /etc/passwd represent human users. Some are system accounts (e.g., root, daemon, nobody) used by various system processes.</figcaption>
</figure>

* **Which users are currently running processes?**
<figure>
    <img src ="/assets/img/ps-users.png" alt="Screenshot showing the output of the users currently running processes">
</figure>

* **Does the user have any sudo privileges?** Yes both root and student have sudo privilege 

### <strong>Task 3: Kernel Vulnerability Analysis.</strong>
A kernel vulnerability is a security flaw in the kernel, the core part of an operating system. The kernel manages system resources like CPU, memory, and device, and it controls how software interact with hardware. Because of this central role, a vulnerability in the kernel can potentially give an attacker extensive control over the system.

**Steps**

1. Manual Vulnerability Search

A manual vulnerability search involves using various online resource to identify known vulnerabilities in a host. Below are the vulnerability I found, along with their sources.

**CVE-2024–6387:** A remote code execution vulnerability in OpenSSH, exploiting login timers to execute code. Recommended fix: update openssh-server. Read more on the [Ubuntu blog.](https://ubuntu.com/blog/ubuntu-regresshion-security-fix)

**CVE-2024–24791:** This vulnerability affects the net/http library in Go, allowing a denial of service due to improper handling of the 100-continue HTTP response header. Exploitation can lead to failed connections, especially when used with reverse proxies. It has been addressed in updated library versions. Read more on [SUSE](https://www.suse.com/security/cve/CVE-2024-24791.html)

**CVE-2024–34158:** highlights a vulnerability in the Go programming language that can lead to application crashes. Specifically, it occurs when the Parse function is called on a "// +build" build tag line with excessive nesting, which causes a stack exhaustion panic. This issue carries a high CVSS score of 7.5, indicating it poses a significant risk to systems that utilize this feature. Read more on [SUSE.](https://www.suse.com/security/cve/CVE-2024-34158.html)

2. **Automated Kernel Vulnerability Detection**

We will be utilizing the provided tool which, Linux Exploit Suggester. You can find it [here.](https://github.com/The-Z-Labs/linux-exploit-suggester)

<img src ="/assets/img/wget.png">

We need to add execute permission to the script, as it currently doesn't not have it.

<img src ="/assets/img/permission.png">

With all the necessary preparations in place, we can now run the script that automates our vulnerability search. This tool will streamline the process, enabling us to efficiently identify potential vulnerabilities in the system.

<figure>
    <img src="/assets/img/les.png" alt="Screenshot showing the exploit being lunched">
    <figcaption>Each of these vulnerabilities can allow attackers to escalate privileges under certain conditions. Some require administrative privileges (CAP_NET_ADMIN), while others like DirtyPipe, PwnKit, and Baron Samedit are more accessible, posing a higher risk for unprivileged users to gain root access.</figcaption>
</figure>


## Findings: Manual and Exploit Suggester Tool Analysis

During the vulnerability assessment, both manual inspection and the exploit suggester tool highlighted critical security issues, each requiring timely patches to maintain system integrity.

1. **CVE-2024–6387:** This remote code execution vulnerability in OpenSSH leverages login timers to execute unauthorized commands. Resolution: Updating openssh-server mitigates the risk.

2. **CVE-2024–24791:** This denial-of-service vulnerability in Go's net/http library arises from improper handling of the 100-continue HTTP response header, causing service disruptions. Resolution: Updating the library version addresses this flaw.

3. **CVE-2024–34158:** A stack exhaustion vulnerability in Go's Parse function, triggered by excessive nesting in // +build tags, can lead to application crashes. Resolution: Updating the Go environment safeguards against this issue.

The **exploit suggester tool** further identified high-risk vulnerabilities, including DirtyPipe, PwnKit, and Baron Samedit, which enable privilege escalation without requiring elevated permissions. This feature is particularly beneficial for penetration testers and system administrators, offering a swift way to evaluate a system's susceptibility to privilege escalation attacks and highlight areas needing immediate attention.

## <strong>Task 4: Weak File Permission</strong>

Weak file permission involves identifying files with weak permission and understanding the associated security risks.

Use the following command to check file permissions:

<figure>
    <img src="/assets/img/passwdddd.png" alt="Screenshot of output showing the password permission command">
    <figcaption>This command is used to view the permission of the password file.</figcaption>
</figure>

<figure>
    <img src="/assets/img/passwdddd.png" alt="Screenshot of output showing the shadow permission command">
    <figcaption>This command is used to view the permission of the shadow file.</figcaption>
</figure>

**Questions:**

1. **What command did you use to display the shadow file? Analyze the output and provide the password has for the student user.**

<img src="/assets/img/shadoww.png>"

The /etc/shadow file stores user account information, specifically the hashed passwords and password management settings for each user on the system. 

**Username:** The username is the first field of each line (e.g., root, daemon, bin). 

**Password Hash:** The password hash is the second field. A single * or ! symbol here indicates that the account does not have a password(is locked or disabled). **It's good practice not sharing sensitive information like that in public so I will not be posting the password hash.**

**Last Password Changed:** The third field represents the number of days since the epoch when the password was last changed, the value corresponds to a specific recent date in days. 

**Minimum Password Age:** The fourth field is the minimum number of days required between password changes. A value 0 here means the password can be changed any time. 

**Maximum Password Age:** The fifth field is the maximum number of days the password is valid. After this period, the user must change their password. 99999 here implies the passwords are set to never expire. 

**Password Warning Period:** The sixth field indicates the number of days before expiration that the user is warned to change their password. 

**Password Inactivity Period:** The seventh field shows the number of days after a password expires before the account is disabled. A blank here means it's not set. 

**Account Expiration Date:** The eight field is the absolute date when the account expires, represent in days since the epoch. A black here means there is no expiration date.

2. **How many users are listed in the passwd file?**

<img src="/assets/img/wc.png>

3. **Are there any file(s) in the /root directory with weak permissions? Provide a clear explanation.**

<img src="/assets/img/root.png>
