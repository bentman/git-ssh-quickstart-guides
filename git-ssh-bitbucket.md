# Setting Up SSH Keys for Bitbucket

## 1. Check for Existing SSH Keys
Open a terminal and check for existing keys by running the following command:
```bash
ls -al ~/.ssh
```
Look for files named `id_ed25519` and `id_ed25519.pub`.

## 2. Generate a New SSH Key Pair
If you don't have an existing key, generate a new one by running the following command:
```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```
Make sure to replace `your_email@example.com` with your actual email address.

## 3. Add Your SSH Public Key to Bitbucket
- Display and copy your public key by running the following command:
```bash
cat ~/.ssh/id_ed25519.pub
```
- Log into your Bitbucket account.
- Go to: Avatar (bottom left) > **Personal settings** > **SSH keys**.
- Click on the "Add key" button and paste your public key.

## 4. Test the Connection
Test the connection by running the following command:
```bash
ssh -T git@bitbucket.org
```
If you see a welcome message, it means that the connection was successful.

## 5. Configure Git to Use SSH (if needed)
In your repository directory, run the following command to configure Git to use SSH:
```bash
git remote set-url origin git@bitbucket.org:username/reponame.git
```
Make sure to replace `username` and `reponame` with your actual username and repository name.

## 6. Troubleshooting
If you encounter any issues, ensure that the SSH agent has the right key by running the following commands:
```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

That's it! You can now enjoy password-less Git operations with Bitbucket. 😊