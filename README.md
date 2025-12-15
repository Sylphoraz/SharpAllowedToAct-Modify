# Introduction

This project is a fork of [SharpAllowedToAct]. Sometimes, an attacker may obtain credentials for a privileged user but lack access to the user's machine. To exploit this scenario—where the attacker aims to perform resource-based constrained delegation attacks using the acquired privileged account (e.g., a domain-joined account)—`SharpAllowedToAct` only leverages the current user's privileges for attacks. Therefore, I made the following modifications:

1. The operation for adding machine accounts has been removed. You can use the original `SharpAllowedToAct` to add accounts, or use `addcomputer.py` to add machine accounts.

2. Added custom LDAP account and password parameters.

3. Added the specified machine account parameter

# Instructions for Use

The default `msds-allowedtoactonbehalfofotheridentity` is not specified, so the ticket request failed:

<img width="649" height="195" alt="wecom-temp-57fce9cf5f6a8385299c7d8199d6ef29" src="https://github.com/user-attachments/assets/975df16b-b685-41e5-a4ea-4917665c124c" />

Use the tools provided by this project to modify the victim's `msds-allowedtoactonbehalfofotheridentity` attribute:

<img width="1321" height="363" alt="image-20211215223552267" src="https://github.com/user-attachments/assets/f56dd573-db29-4e6e-9dc5-b6df8d70ffae" />

The -m parameter specifies the machine account you added, -u is the LDAP username, -p is the LDAP password, -t is the target machine name, -a is the domain controller address, and -d is the domain name. For example:

```
SharpAllowedToAct.exe -m machine -u ldapuser -p ldappass -t victim -a dcserver.domian.com -d domain.com
```

The bill application was successful at this time:

<img width="804" height="213" alt="image-20211215213032275" src="https://github.com/user-attachments/assets/95fdfc3d-5c1d-4084-a1aa-0f779e77ee0f" />

RBCD successfully connected to the victim machine:

<img width="1327" height="446" alt="image-20211215212349621" src="https://github.com/user-attachments/assets/7e04c3a8-6c07-4dd9-9fdd-4214ec8566b5" />
