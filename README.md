# TryHackMe Documentation: Cyber Defense 

## 1. Introduction
- **Purpose**: Document my experience and share knowledge on the Cyber Defense challenge.
- **Scope**:  Learn the fundamental components of detecting and responding to threats in a corporate environment.

## 2. Setup
- **Environment**: Kali Linux via VirtualBox
- **Accounts and Access**: Created a TryHackMe account and accessed the room via OpenVPN

## 3. Challenge Walkthrough

### 3.1 Room Name: Network Services
- **Objective**: Learn about, then enumerate, and exploit a variety of network services and misconfigurations

### 3.2 Enumeration
- **Initial Scanning**:
  - **Tools and Commands**: 
	- `Enum4linux `
	- `enum4linux -U 10.10.242.131`
	- `enum4linux -a 10.10.242.131`
  - **Findings**:
	- Users are: administrator, guest, krbtgt, domain admins, root, bin, none
	- No password 
	- Workgroup name is WORKGROUP
	- Name of machine is polosmb
	- OS running on version 6.1
	- ***Ports that are open***:
		- 22/tcp  open  ssh
		- 139/tcp open  netbios-ssn
		- 445/tcp open  microsoft-ds
	- Users profiles is shared in the SMB with the sharename 'profiles'

### 3.3 Exploitation
- **Vulnerability Identification**: [CVE-2017-7494 (https://nvd.nist.gov/vuln/detail/CVE-2017-7494)]
  - **Techniques Used**:  exploiting anonymous SMB share access- a common misconfiguration that can allow us to gain information that will lead to a shell.

- **Exploitation Process**:
  - **Commands and Payloads**: 
  - **Screenshots**: ![Exploitation Step]
	- Enter to access smb smbclient //10.10.242.131/ Anonymous -U profiles
	- Press Enter on Password
	- Enter ls -a to show files and hidden files

- Type get “Working From Home Information” to download to your download           folder
- Enter ‘cat Working From Home Information.txt’ to view the text file in your 












- Type open .ssh to access directory
- To download type get id_rsa

	- Type chmod 600 id_rsa to change the permissions

	







- Type ssh cactus@10.10.242.131 -i id_rsa to access the server

	- Type ls  to show files then cat smb.txt to view text file


## 4. Analysis and Reflection
- **Challenges Faced**: Difficulty in identifying the exact version of Apache.
- **Learnings**: Importance of thorough enumeration.
- **Improvements**: Try alternative enumeration techniques earlier.

## 5. Conclusion
- **Summary**: Successfully gained root access and captured the flag

## 6. References
- [TryHackMe](https://tryhackme.com)
- [Nmap Documentation](https://nmap.org/book/man.html)

