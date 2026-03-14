# OverTheWire-Bandit-WriteUp-Level-19---20
## Objectives:
Understand how special permissions work on Linux systems (specifically the SUID) and demonstrate how a misconfigured binary can be exploited to execute commands with elevated privileges and access restricted files.
The objective of this level is to find the password located in */etc/bandit* pass using the SUID.
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
-rw**s**r-x--- 1 bandit20 bandit19 14884 Oct 14 09:26 bandit20-do
```

