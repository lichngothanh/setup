# SSH Multi Account Setup 

## SSH Keys

SSH will contain the following keys:

| Purpose           | File Name                         | Description                  |
|-------------------|-----------------------------------|------------------------------|
| GitHub Personal   | `id_ed25519_github_personal`      | Personal GitHub account      |
| GitHub Company    | `id_ed25519_github_work`          | Company GitHub account       |
| Azure Repo Company| `id_ed25519_azure_work`           | Company Azure DevOps repos   |

## Step 1. Create a folder to store .ssh.

```bash
mkdir ~/.ssh
```

## Step 2. Generate SSH Keys

Run:

```bash
ssh-keygen -t ed25519 -C "personal@email.com"
```

When asked:

```text
Enter file in which to save the key:
```

Input:

```text
~/.ssh/id_ed25519_github_personal
```

> [!NOTE]
> If you get a No such file or directory error, enter the full path instead.
>
> **Passphrase:** is a password used to encrypt and protect an SSH private key; Git push/pull operations require the passphrase to unlock the key before authentication.

Result:

```text
id_ed25519_github_personal
id_ed25519_github_personal.pub
```

Repeat the same setup for the project or company account.

Final result:
```text
id_ed25519_github_personal
id_ed25519_github_personal.pub

id_ed25519_github_company
id_ed25519_github_company.pub

id_ed25519_azure_company
id_ed25519_azure_company.pub
```

## Step 3. Start ssh-agent service
```bash
Get-Service ssh-agent | Set-Service -StartupType Automatic
Start-Service ssh-agent
```
Check: 
```bash
Get-Service ssh-agent
```
Result:
Status   |Name               |DisplayName
------   |----               |-----------
Running  |ssh-agent          |OpenSSH Authentication Agent

## Step 4. Add keys
```bash
ssh-add ~/.shh/id_ed25519_github_personnal
```

check keys:
```bash
ssh-add -1
```

## Step 5. Add config file

Add config file to ~/.ssh

```bash
# GitHub Personal
	Host github-personal
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519_github_personal

# GitHub Work
	Host github-company
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519_github_company

# Azure DevOps
	Host azure-company
    HostName vs-ssh.visualstudio.com
    User git
    IdentityFile ~/.ssh/id_ed25519_azure_company
```

## Step 6. Copy keys and create in Git Store
Cat key:
```bash
cat ~/.ssh/id_ed25519_github_personal.pub
```

[Git Hub SSH](https://github.com/settings/keys)
