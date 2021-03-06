# Setup

## WirtBot®

If you want to run your own WirtBot you will need the following things:

- A machine with a public IP on the internet
- Root access on this machine
- WireGuard® already installed
- A valid SSL certificate for your machine
- Port 3030 opened in your firewall
- Your system is managed with [systemd](https://en.wikipedia.org/wiki/Systemd)
- Your WireGuard configuration should be at `/etc/wireguard/server.conf`.

Having these things is the first **80%** of finishing your WirtBot and you should find plenty of documentation about these things on the internet.
Here are a few links:

- [What is Linux?](https://www.linux.com/what-is-linux/)
- [Initial Server Setup with Ubuntu](https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-16-04)
- [nftables as a firewall](https://wiki.debian.org/nftables)
- [HTTPS with LetsEncrypt](https://letsencrypt.org/about/)
- [systemd](https://wiki.archlinux.org/index.php/Systemd)
- [WireGuard installation](https://www.wireguard.com/install)

If you come across a good tutorial, or have vast knowledge about these topics, contributions to make this documentation easier are highly encouraged!
Just contact me for info on how to help out or send a PR on this [repo](https://github.com/b-m-f/wirt/docs/) if you know what that is.

But what about the last **20%**?

Finishing up the setup requires the [WirtBot executable](https://github.com/b-m-f/wirt/releases) to be running on your machine.

This can be achieved with the following steps:

- Download a release from https://github.com/b-m-f/wirt/releases and place it into `/usr/bin/`
- `sudo chmod +x /usr/bin/wirtbot` to make it executable
- Get the public key of your WirtUI from the [settings section](https://wirt.network/dashboard) on the Dashboard
- Copy https://github.com/b-m-f/Wirt/blob/master/WirtBot/wirtbot.service to `/etc/systemd/system/wirtbot.service`
  - **Make sure to change the variables in that file**!
  - PUBLIC_KEY: this is the public key from the WirtUI
  - SSL_PEM_CERT: this is the location of your SSL certificate
  - SSL_KEY: this needs the location to your SSL key
  - User and Group: choose the user and the group that is used to run the `wirtbot` or delete these lines to use the root user.
  - You can leave the port and host setting at the default, unless you really know what you are doing
- When configured correctly you can now run `systemctl enable --now wirtbot` to start the WirtBot. Use `journalctl -xe` if something is going wrong to get more information on what happened
- The last step to finish up the setup is the activation of a reloader. Copy https://github.com/b-m-f/Wirt/blob/master/WirtBot/wireguard-restarter.sh to `/usr/bin/wireguard-restarter.sh`
- Now copy https://github.com/b-m-f/Wirt/blob/master/WirtBot/wireguard-restarter.service to `/etc/systemd/system/wireguard-restarter.service`
- Run `systemctl enable --now wireguard-restarter`

### Testing your setup

To verify that everything is running correctly you can now add your hostname for which your SSL certificate is valid to your server on the [Dashboard](https://wirt.network/dashboard).

Now add a new mobile device, scan the presented QR code with your WireGuard app and verify that you can reach other devices on your network.

For verification you can always try to ping the WirtBot. Its IP in the network is always `SUBNET` + 1. With the default settings this is `10.10.0.1`

### Using a different interface name

If you would like to use i.e. `wg0` instead of `server`for the interface name make sure to change this in the `wireguard-restarter` and add the `CONFIG_PATH` environment variable to your `wirtbot` service.

## WirtUI

Nothing to set up here.

By reaching the website your setup is done. If you have set up the WirtBot following the above instructions it should already be connected to the WirtUI and you are ready to go.
