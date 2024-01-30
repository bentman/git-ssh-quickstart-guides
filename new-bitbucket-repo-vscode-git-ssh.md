# Creating a New Bitbucket Repository from VS Code with Git Bash SSH Integration

## 1. Open VS Code and Git Bash
- Open VS Code and press `Ctrl + Shift + P` to open the command palette.
- Type and select "Terminal: Select Default Profile".
- Choose "Git Bash" from the list of available profiles.

## 2. Create a New Local Repository
- In the terminal, navigate to the directory where you want to create your new repository.
- Run the following command to initialize a new Git repository:
```bash
git init
```

## 3. Add Files and Make Changes
- Add files to your repository and make changes as needed.
- Stage and commit your changes using the Source Control panel in VS Code.

## 4. Create a New Repository on Bitbucket
- Log into your Bitbucket account.
- Click on the "+" icon (top left) > **Repository**.
- Fill in the repository details and click "Create repository".

## 5. Add Remote and Push Changes to Bitbucket
- In the terminal, navigate to your repository's directory.
- Add the remote by running the following command:
```bash
git remote add origin git@bitbucket.org:username/reponame.git
```
Make sure to replace `username` and `reponame` with your actual username and repository name.
- Push your changes to Bitbucket by running the following command:
```bash
git push -u origin main
```

That's it! You have successfully created a new local repository, added files, and pushed it up to a new remote repository on Bitbucket from VS Code with Git Bash SSH integration. 😊