---
sidebar_position: 7
description: How to use Narrowlink to connect to your remote machine using SSH
keywords: [SSH, Integration, Gateway, Agent, Client, Narrowlink, Narrow, Link, Networking, Internet, Security, Privacy, Open Source, Self-hosted, Tutorial, How-to, Guide, Nat, Firewall, Proxy, Reverse Proxy, Tunnel]
---

# SSH Integration

The Narrowlink client can acts like `netcat` command to connect to the services that are running on the agent network machine. It is useful for various porpurses such as connecting to a ssh server.

Add the bellow setting to your ssh client configuration which is normally at `~/.ssh/config` to use narrowlink to conenct to your machines:

```bash
Host <agent_name>
    ProxyCommand narrowlink connect -n <agent_name> %h:%p
    HostName 127.0.0.1
    Port 22
    User <username> # server username
    #StrictHostKeyChecking no #optional to ignore host key checking
    #UserKnownHostsFile=/dev/null #optional to ignore host key checking
```

Replace `<agent_name>` with the name of the machine you want to connect to, `<username>` with your actual username.

- You can now use `ssh office` command to connect to the office machine.

:::tip
You can set up your SSH server to listen only on localhost to prevent unauthorized remote access to your machine. Instead, you can connect to your machine through Narrowlink for secure access.
:::

Enjoy seamless ssh access to your remote machine.