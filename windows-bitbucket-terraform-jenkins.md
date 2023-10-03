# Windows Client Setup Guide

This guide covers setting up Bitbucket, Git, Terraform, and VS Code on Windows for infrastructure as code using SSH keys for authentication.

## Generate SSH Keys

From the VS Code terminal, generate an ed25519 SSH key pair:

```powershell
ssh-keygen -t ed25519 -C "your_email@example.com"
```

## Add Public Key to Bitbucket  

Copy your public key and add it to your Bitbucket account:

```powershell
Get-Content -Path ~/.ssh/id_ed25519.pub
# Copy output and add to Bitbucket SSH keys 
```
- [Bitbucket SSH Key Setup Guide](https://support.atlassian.com/bitbucket-cloud/docs/set-up-an-ssh-key/)

## Clone Bitbucket Repos

Clone your Bitbucket repos in the terminal using the SSH URL:

```powershell
git clone git@bitbucket.org:user/repo.git
```

## Configure Git in VS Code

Set your Git username and email:

```powershell
git config --global user.name "Your Name"
git config --global user.email "your_email@example.com"
```
- [GitHub SSH Key Setup Guide](https://docs.github.com/en/authentication/connecting-to-github-with-ssh)

## Install Terraform Extension

Install the Terraform extension for VS Code. In the extension settings, configure the `terraform.cli` path to point to your Terraform binary.

- [HashiCorp Terraform VSCode extension - GitHub](https://github.com/hashicorp/vscode-terraform)
- [Enabling VS Code Terraform extension code completion on Windows and ...](https://dev.to/wholroyd/enabling-vs-code-terraform-extension-code-completion-on-windows-and-macos-2d0c)

## Configure Terraform Backend  

In your Terraform files, set the `backend` config to point to your remote state storage in Bitbucket:

```hcl
terraform {
  backend "s3" {
    endpoint   = "https://bitbucket.org/account/repo" 
    bucket     = "terraform-state"
    key        = "env/myterraform.tfstate"
    region     = "us-east-1" 
  }
}
```
- [Using SSH Keys for Cloning Modules - HashiCorp Developer](https://developer.hashicorp.com/collections/terraform/ssh-keys)
- [How to use Project wide ssh keys with terraform - StackOverflow](https://stackoverflow.com/questions/38919811/how-to-use-project-wide-ssh-keys-with-terraform)
- [Terraform GitHub Actions](https://www.terraform.io/docs/github-actions/setup-credentials.html)

## Connect to Jenkins Pipeline

Install the Jenkins and Pipeline extensions. Add your private key to Jenkins credentials for SSH access. Configure a webhook in your Bitbucket repo to trigger the Jenkins pipeline on changes.

- [Using Jenkins agents](https://www.jenkins.io/doc/book/using/using-agents)
- [Step-By-Step Guide to Setting Up SSH Keys for Jenkins | Jhooq](https://jhooq.com/setting-up-ssh-keys-for-jenkins)
- [Jenkins and GIT Integration using SSH Key - GeeksforGeeks](https://www.geeksforgeeks.org/jenkins-and-git-integration-using-ssh-key)

## Manage Repos in VS Code

Use VS Code to commit changes and push to Bitbucket to trigger deployments.

## More Resources

1. **Azure CLI Installation and Configuration**:
   - [Get started with Azure CLI](https://docs.microsoft.com/en-us/cli/azure/get-started-with-azure-cli)
   
2. **Azure Provider Configuration in Terraform**:
   - [Azure Provider: Authenticating using the Azure CLI](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/guides/azure_cli)

3. **Azure VM Management with Terraform**:
   - [AzureRM Provider Documentation](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs)

4. **Azure Extensions in Visual Studio Code**:
   - [Azure Extensions for Visual Studio Code](https://marketplace.visualstudio.com/azure)

5. **Azure DevOps Integration**:
   - [Azure DevOps Documentation](https://learn.microsoft.com/en-us/azure/devops/?view=azure-devops)

6. **Jenkins on Azure**:
   - [Jenkins solutions in Azure](https://docs.microsoft.com/en-us/azure/developer/jenkins/)

7. **Azure VM Monitoring and Management**:
   - [Management and Monitoring of VMs in Azure](https://docs.microsoft.com/en-us/azure/virtual-machines/manage-monitor)

8. **Security Best Practices**:
   - [Azure Security Best Practices](https://docs.microsoft.com/en-us/azure/security/fundamentals/best-practices-and-patterns)

9. **Collaboration and Version Control**:
   - [Bitbucket Cloud Documentation](https://support.atlassian.com/bitbucket-cloud/)

10. **Automated Testing and Deployment**:
    - [Automating Jenkins with REST, Pipeline, and more](https://www.jenkins.io/doc/book/automating/)

Here is a markdown section on security best practices for SSH keys:

## SSH Security Best Practices

When working with SSH keys, follow these security best practices:

#### Use SSH agent forwarding

- Start the SSH agent in the background:

```powershell
# Start SSH agent
ssh-agent -s 

# Add key 
ssh-add ~\.ssh\id_ed25519
```

- Enable agent forwarding when connecting:

```powershell
ssh -A user@host
```

- This allows you to access remote hosts without copying keys.

#### Avoid copying keys

- Avoid copying private keys between machines.

- Copy public key instead and generate keys on each host.

#### Use passphrase for keys

- Secure keys with a passphrase.

- Prevents use of keys if compromised.

#### Revoke compromised keys 

- If a key is compromised, revoke it immediately.

- Remove from remote hosts and regenerate.

Following these best practices prevents your SSH keys from being misused if compromised.
