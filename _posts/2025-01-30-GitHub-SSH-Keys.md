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
1. Generate a key pair, or use one that already exists.
2. Add the public key to your GitHub account under the user Settings, SSH and GPG Keys area.
3. Use the git@github.com URL instead of the https://<PAT>@github.com URL.

As I have more than one key pair for different client computers and servers, I wanted to store the new keys in a uniquely named set of files, not using the a default name.
```
$ ls -1 ~/.ssh/*github*
id_ed25519_shumphreys_github
id_ed25519_shumphreys_github.pub
```
The public key is added to my account on GitHub. The private key is kept on my Linux client machine. 
In order for SSH to find this key file when using the URL git@github.com, the ~/.ssh/config file must have **github.com** for *both* the Host and HostName. The User is set to git.
Initially, I used a different, simpler alias in the Host field, as suggested generally for the .ssh/config file.
This does not work with the expected git@github.com URL, though it does work with the alias, e.g. ```ssh -T GitHub```.

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
Note there are other considerations where HTTPS may be preferable, and there are additional PAT/credential storage mechanisms beyond the .git/config file. See the HappyWithR blog linked below for examples.
## References
[GitHub SSH instructions](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)  
[Using the SSH config file, at Linuxize.com](https://linuxize.com/post/using-the-ssh-config-file/)  
[rmauro blog: Set up GitHub with SSH Config](https://rmauro.dev/github-ssh-key-authentication-and-ssh-config/)  
[HappyWithR blog: on PAT and HTTPS vs SSH](https://happygitwithr.com/https-pat)  
