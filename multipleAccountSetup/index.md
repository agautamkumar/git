
---

### **Check Added Git SSH Keys in Linux**

This guide helps you verify how many SSH keys are added and used in your Linux system for Git authentication.

---

## **1️⃣ Check SSH Keys Loaded in SSH Agent**
To see the currently **loaded SSH keys**, run:

```bash
ssh-add -l
```

- If it lists multiple keys, those are the ones currently **loaded**.
- If it says **"The agent has no identities."**, no SSH keys are added.

---

## **2️⃣ List All Available SSH Keys**
To check how many SSH keys exist on your system, list the contents of your SSH directory:

```bash
ls -l ~/.ssh/id_*
```

This will display available SSH keys, such as:

```
-rw------- 1 user user  2602 Feb 16 15:20 id_rsa
-rw-r--r-- 1 user user   574 Feb 16 15:20 id_rsa.pub
-rw------- 1 user user  2602 Feb 16 15:22 id_ed25519
-rw-r--r-- 1 user user   574 Feb 16 15:22 id_ed25519.pub
```

Each key usually comes in a pair:
- **Private Key (`id_ed25519`, `id_rsa`)** → Keep it secret!
- **Public Key (`id_ed25519.pub`, `id_rsa.pub`)** → Used to authenticate with Git servers.

---

## **3️⃣ Check If SSH Keys Are Being Used for Git**
To confirm that SSH authentication works with Git, test it with:

```bash
ssh -T git@github.com
```

If a key is recognized, you’ll see:

```
Hi your-username! You've successfully authenticated, but GitHub does not provide shell access.
```

For GitLab:

```bash
ssh -T git@gitlab.com
```

For Bitbucket:

```bash
ssh -T git@bitbucket.org
```

---

## **4️⃣ Check Which SSH Key is Used by Git**
To check which SSH key Git is using:

```bash
ssh -vT git@github.com
```

Look for a line that shows which identity file is being used:

```
debug1: Offering public key: /home/user/.ssh/id_ed25519
```

This tells you which key is being sent to GitHub for authentication.

---

## **5️⃣ Manage Multiple SSH Keys for Different Accounts**
If you have multiple Git accounts, configure `~/.ssh/config`:

```bash
nano ~/.ssh/config
```

Add entries like:

```
Host github-personal
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519_personal

Host github-work
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519_work
```

Then, use:

```bash
git remote set-url origin git@github-personal:your-username/repo.git
```

---

### **🛠 Summary**
| Command | Purpose |
|---------|---------|
| `ssh-add -l` | Show loaded SSH keys |
| `ls -l ~/.ssh/id_*` | List all stored SSH keys |
| `ssh -T git@github.com` | Test GitHub SSH connection |
| `ssh -vT git@github.com` | Debug which SSH key is used |
| `nano ~/.ssh/config` | Configure multiple SSH keys |

---

Now you can **check, manage, and use multiple SSH keys** in Linux for Git authentication! 🚀🔑

