> Copyright (C) 2022 Sandesh Regmi
### The permission to modify, delete, copy, merge, publish and use is herbly allowed to any users but they should mention the above copyright line

---
---
# OPENSSH Quick Guide 
### By *__Sandesh Regmi__*
___
---
## What is OPENSSH?
Well, if we dive directly dive into the topic, we can define openssh as the utility used to execute or run command in a remote machine via ssh. It comes installed by default in almost every linux distro. However, you will need to install it manually in some linux distrubution such as arch. Openssh comes pre installed with ssh client in Mac OS while in windows, you can install wsl, install any linux distrubution and install openssh. Still, if you can't install openssh, then go and take the help of google. After you have ssh installed, you can write `which ssh` in your terminal in order to see the binaries of openssh and if you are not able to see it, means that you have not it installed. SSHD is the daemon of ssh client.

Openssh use port number `22` by default
---
#
___

## Connecting to the remote computer via openssh
---
## Use the reference of the following command

> *__ssh {username given to the target machine}@{ip address}__*
### For example:
``` BASH
ssh -v sandesh@192.168.1.2
```

In the above option, it is not mandatory to use `-v` flag that stands for verbose and for getting more information while connecting, that flag was used. You can use `-p {port number}` as well. However, you can use `-p` command only if change the default port of ssh.

Use `Ctrl+D` in order to disconnect yourself from ssh shell that you had connected to.
Once you are connected to a machine via ssh, all of your caches that contains files like previously connected devices list and many more are going to be stored in .ssh directory which is present inside your home directory`(Or in root directory if you are logging it as root)`.

But when you need to connect to a machine time and again, it might not be a good task for you to write the username and ip address time and again which is even a bit harder to remember at all. So, you can do some configuration inside the .ssh directory located inside your home user directory. The followings are the thing mentioned in steps that you can do :
``` BASH
echo "You are completely legal to copy all the command"
cd ~/.ssh/ #Heading over to the home directory
vim config #Creating a configuration file and instead of vim, you can use any code editor
```

Now, just see what I have done and I will explain everything once you are done with looking the following block:

``` BASH
Host {machine name that you will remember with following features}
    User {username and remember that you can use root user as well}
    Hostname {ip address}
    Port {Port number}
``` 

Now, you might be a bit confused right? So, see the following example and try to understand(You can even copy and paste the same text inside config file but take care about IP Address):
``` BASH
Host machine1
    User root
    Hostname 192.168.1.2
    Port 22
```
Next time, when I need to connect to the `machine1` containing the ip address of `192.168.1.2` , I don't need to write and mention everything just like you learned in the last lesson. Instead, I can connect to it just like:
```BASH
ssh machine1
```
And remember that `you can add as more machine as you can in that config file` . However, it's your duty to remember the name or you can just visit the file in order to see the name of the machine that is targeted by you in order to connect.
___

## SSH Keys
SSH keys help to connect to the remove server or a computer in much more efficient and secure way. As you know, ssh is secured using password but that password can be bruteforced and the attacker can gain access into your computer or the server. So, in this case ssh keys comes into the action that contains the highest level of security as it uses cryptography. By creating a ssh key, you can disable password authentication which means you can connect to the remote server or the computer without entering the password.

You can generate ssh keys using command `ssh-keygen` and it will ask you to tell the name of output directory for storing ssh key and ask for password too. Finally, it will display ssh key fingerprint and it's ramdomart image. However, you need to be sure that you are running this command in the main computer. When you overwrite the sshkey, you will overwrite the current key and lose the access to SSH connection using that current key.
While using `ssh-keygen` command, you can add several flags. You can use `-C` flag followed by the previous command `as a comment but it should be enclosed inside quotes`.

SSH key are of two type, which are `private key` and `public key`. Public key have the extension of pub at the end of file while private key don't have any such extension. You can add a public key in the remote computer for encryption whereas private is kept in your computer(local computer) for the decryption of public key.

You can copy the content of public ssh key from your local computer and after connecting to remote computer using ssh, you can paste the content of public key of your computer to the remove computer and next time, when you try to log in to the same computer, you don't need the passphrase. However, you it might be necessary to enter the password that you set while generating the ssh key using `ssh-keygen` command. But, you can disable password login and allow only ssh key login by heading over to sshd_config file present inside ssh directory which is also present inside etc directory and then find a line which match `PasswordAuthentication` and it's value is set to yes by default. Here, all you need to do is set that "yes" value to "no" and then save that file. Finally, you can restart ssh service to get the changes applied. But, secured auto-login is one of the key feature of openssh and disabling that option might not be the good choice for you.

One key thing which is necessery to tell you is that `if you don't provide the comment, your computer name is going to be written at the end of public key as a comment`.

Now, your job is to go to sshd_config file inside /etc/ssh directory and view various option there. You can change several things such as root login, default port and login count.

### I hope you guys got a chance to learn something new about SSH. It's not a big topic but it is quite essential tool.