# Fixing the Permissions on my Project Zomboid Server

## Introduction
Since I plan on using my Dell OptiPlex 7090 as the host machine for my Vaultwarden password manager, I decided that it'll need a lot of hardening before I'm ready to set things up. While this machine *does* sit behind a firewall on the network perimeter, it's still good practice to protect a machine that essentially carries the most valuable digital payload in my lab. The biggest outward-facing risk I identified was my Project Zomboid server. Due to its nature as a video game server, it has to listen, constantly, on an open port. And I had it running ass root, too. Not good, since that could potentially give a threat actor full access to the device.
## Setting up ownership
So, my first course of action was to create a new user, with, of course, the least possible privileges. 

```bash
sudo adduser --system --group --home /home/zomboid --shell /usr/sbin/nologin zomboid
```

Since this user is only for this one server, and isn't an actual human user, I used the --system flag to declare it as such. Then, the --group and --home flags create a separate group and a home directory, respectively. The idea here is to make a user that simply runs the server as a process, and does only that. I don't allow an actual login, or any shell/ssh privileges, as it won't be needed and isn't worth the risk. After backing up the server files and copying them to their new directories, (integrity of save data needed to be preserved) I was able to change ownership of both the game directory and server files to the zomboid user.
```bash
sudo chown -R zomboid:zomboid /home/zomboid/Zomboid
sudo chown -R zomboid:zomboid /home/zomboid/pz_server
```

I used '-R' to make the changes recursive, and then double-checked that everything went through. I got

<img width="1071" height="69" alt="image" src="https://github.com/user-attachments/assets/cf104a36-e6e8-4b33-8bb2-d32311b9e2d5" />

Looks good, and its a relief to not have that running as root anymore.
