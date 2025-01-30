---
title: "GitHub and SSH Keys"
date: 2025-01-30
layout: post
excerpt_separator: <!--more-->
---
GitHub provides mutliple methods for remote access, including HTTPS with a personal access token (PAT) or SSH.  Initially I used a PAT in the URL, but for now I prefer using SSH keys, which requires stricter file permissions on the client machine.
<!--more--> 

In the example just below, the PAT is the portion "ghp_...".
```
$ cat ~/local_git/shumphreys2.github.io/.git/config 
...
[remote "origin"]
	url = https://ghp_...@github.com/shumphreys2/shumphreys2.github.io
...
```
SSH access is handled with a public-private key pair.  The main steps are:
1. Generate a key pair with ```ssh-keygen -t ed255519 -C "comment"```, or use one that already exists.
2. Add the public key to your GitHub account under the user Settings, SSH and GPG Keys area.
3. Use the git@github.com URL instead of the https://<PAT>@github.com URL.

## Linux client
As I have more than one key pair for different client computers and servers, I wanted to store the new keys in a uniquely named set of files, not using the a default name.

```
$ ls -1 ~/.ssh/*github*
id_ed25519_shumphreys_github
id_ed25519_shumphreys_github.pub
```
The public key is added to my account on GitHub. The private key is kept on my Linux client machine.  
**Important**: In order for SSH to find this key file when using the default URL git@github.com, the ~/.ssh/config file must have *both* the Host and HostName fields set to **github.com**. The User is set to git.  (Initially, I tried to use GitHub as a simple alias in the Host field, as suggested generally for the .ssh/config file. This does not work with the default URL git@github.com, though it does work with the alias, e.g. ```ssh -T GitHub```.)

~/.ssh/config
```
Host github.com
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519_shumphreys_github
```
.git/config
```
...
[remote "origin"]
	url = git@github.com:shumphreys2/shumphreys2.github.io
...
```
Testing access:
```
$ ssh -T git@github.com 
Enter passphrase for key '/home/shumphreys/.ssh/id_ed25519_shumphreys_github': 
Hi shumphreys2! You've successfully authenticated, but GitHub does not provide shell access.
```
## Windows client
On a separate Windows machine I created a new SSH key pair. The steps are a little different.  
First, I installed the Git for Windows tools, which use MINGW64 for git-bash.
[Git Downloads for Windows](https://git-scm.com/downloads/win)  

The following steps work:  
1. ```ssh-keygen -t ed255519 -C "comment"```  
    1. I kept the default file names, id_ed25519 and id_ed25519.pub, as I only have these keys on this machine.
    2. The key files are placed automatically in ~/.ssh/ as usual.
2. Add a new SSH key in GitHub under the user Settings, SSH and GPG Keys area.
    1. Only copy the first two fields, and *not* the comment field., e.g.
       ```ssh-ed25519 <key text>```
3. As on Linux, remove all other permissions from the key files except for the user.
    1. On Windows this must be done through the File Properties, Security and Advanced dialogs.  
    2. See [SuperUser: windows-ssh-permissions-for-private-key-are-too-open](https://superuser.com/questions/1296024/windows-ssh-permissions-for-private-key-are-too-open)
5. Test access with: ```ssh -T git@github.com```  
    1. Additional options for debug: -v, -vvv, or to check the key itself: -i &lt;key file&gt;.

Git operations are performed through the git-bash tool, which also provides the git-gui.

## Other considerations
Note there are other considerations where HTTPS may be preferable, and there are additional PAT/credential storage mechanisms beyond the .git/config file. See the HappyWithR blog linked below for examples.  

## References
[GitHub SSH instructions](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)  
[Using the SSH config file, at Linuxize.com](https://linuxize.com/post/using-the-ssh-config-file/)  
[rmauro blog: Set up GitHub with SSH Config](https://rmauro.dev/github-ssh-key-authentication-and-ssh-config/)  
[HappyWithR blog: on PAT and HTTPS vs SSH](https://happygitwithr.com/https-pat)  
