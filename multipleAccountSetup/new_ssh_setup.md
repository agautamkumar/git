---

# **🔐 Setting Up a New SSH Key for a New Git Account**

This guide walks you through **creating a new SSH key**, adding it to your Git account, and configuring multiple SSH keys in Linux.

---

## **1️⃣ Generate a New SSH Key**
Run the following command to create a new SSH key, replacing `"your_email@example.com"` with your actual email:

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

When prompted for a filename, use a custom name to differentiate from existing SSH keys, e.g.:

```
Enter file in which to save the key (/home/user/.ssh/id_ed25519): ~/.ssh/id_ed25519_newaccount
```

This will generate:
- A **private key**: `~/.ssh/id_ed25519_newaccount`
- A **public key**: `~/.ssh/id_ed25519_newaccount.pub`

---

## **2️⃣ Add the New SSH Key to the SSH Agent**
Start the SSH agent:
```bash
eval "$(ssh-agent -s)"
```

Then, add the newly created key:
```bash
ssh-add ~/.ssh/id_ed25519_newaccount
```

Verify that the key was added successfully:
```bash
ssh-add -l
```

---

## **3️⃣ Add the SSH Key to Your Git Account**
To use this key for authentication, **add the public key to your Git provider**.

1. Display the public key:
   ```bash
   cat ~/.ssh/id_ed25519_newaccount.pub
   ```
2. Copy the output and add it to your Git account:
   - **GitHub**: [Settings → SSH and GPG Keys](https://github.com/settings/keys)
   - **GitLab**: [Preferences → SSH Keys](https://gitlab.com/-/profile/keys)
   - **Bitbucket**: [Personal Settings → SSH Keys](https://bitbucket.org/account/settings/)

---

## **4️⃣ Configure SSH for Multiple Accounts (Optional)**
If you are using **multiple Git accounts**, create a `~/.ssh/config` file:

```bash
nano ~/.ssh/config
```

Add the following configuration:

```
Host github-new
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519_newaccount
```

Save and exit (`CTRL + X`, then `Y`, then `Enter`).

Now, when using this Git account, use `github-new` instead of `github.com`:

```bash
git clone git@github-new:your-username/repository.git
```

---

## **5️⃣ Test Your SSH Connection**
To confirm that your new SSH key is working, run:

```bash
ssh -T git@github-new
```

If successful, you should see a message like:

```
Hi your-username! You've successfully authenticated, but GitHub does not provide shell access.
```

---

## **6️⃣ Use the New SSH Key for a Repository**
If you already have a Git repository and want to use the new SSH key, update the remote URL:

```bash
git remote set-url origin git@github-new:your-username/repository.git
```

Verify the change:

```bash
git remote -v
```

---

## **🛠 Quick Commands Reference**
| Command | Purpose |
|---------|---------|
| `ssh-keygen -t ed25519 -C "your_email@example.com"` | Generate a new SSH key |
| `ssh-add ~/.ssh/id_ed25519_newaccount` | Add the key to SSH agent |
| `cat ~/.ssh/id_ed25519_newaccount.pub` | Copy the public key |
| `nano ~/.ssh/config` | Configure multiple SSH keys |
| `ssh -T git@github-new` | Test the SSH connection |
| `git remote set-url origin git@github-new:your-username/repository.git` | Use new SSH key for repo |

---

Now your new SSH key is created, attached to your new Git account, and ready to use! 🚀😊