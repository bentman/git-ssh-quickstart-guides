# Setting Up Git SSH on VS Code-Server (Fedora & Zsh) for Bitbucket

## 1. Check for Existing SSH Keys in Zsh
Open a terminal in VS Code-Server and check for existing keys by running the following command:
```zsh
ls -al ~/.ssh
```
Look for files named `id_ed25519` and `id_ed25519.pub`.

## 2. Generate a New SSH Key Pair
If you don't have an existing key, generate a new one by running the following command:
```zsh
ssh-keygen -t ed25519 -C "your_email@example.com"
```
Make sure to replace `your_email@example.com` with your actual email address.

## 3. Add Your SSH Public Key to Bitbucket
- Display and copy your public key by running the following command:
```zsh
cat ~/.ssh/id_ed25519.pub
```
- Log into your Bitbucket account.
- Go to: Avatar (bottom left) > **Personal settings** > **SSH keys**.
- Click on the "Add key" button and paste your public key.

## 4. Test the Connection
Test the connection by running the following command:
```zsh
ssh -T git@bitbucket.org
```
If you see a welcome message, it means that the connection was successful.

## 5. Configure Git to Use SSH (if needed)
- In the VS Code-Server terminal, navigate to your repository's directory.
- Set the remote to use SSH by running the following command:
```zsh
git remote set-url origin git@bitbucket.org:username/reponame.git
```
Make sure to replace `username` and `reponame` with your actual username and repository name.

## 6. Troubleshooting
Ensure that Zsh is aware of the SSH agent. You might want to add these lines to your `.zshrc` file to auto-start the agent:
```zsh
if [ ! -S ~/.ssh/ssh_auth_sock ]; then
  eval `ssh-agent`
  ln -sf "$SSH_AUTH_SOCK" ~/.ssh/ssh_auth_sock
fi
export SSH_AUTH_SOCK=~/.ssh/ssh_auth_sock
ssh-add -l > /dev/null || ssh-add ~/.ssh/id_ed25519
```

That's it! You can now enjoy password-less Git operations with Bitbucket on VS Code-Server running Zsh. 😊