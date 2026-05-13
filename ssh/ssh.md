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
