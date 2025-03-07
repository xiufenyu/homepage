---
sidebar_position: 4
description: How to set up the client using Narrowlink
keywords: [Client, Narrowlink, Narrow, Link, Networking, Internet, Security, Privacy, Open Source, Self-hosted, Tutorial, How-to, Guide, Nat, Firewall, Proxy, Reverse Proxy, Tunnel]
---

# Client Setup

To configure the client, you need to create a token using the Token Generator component. Follow the same steps as for generating an agent token, but modify the token-generator.yaml file as shown below to generate a client token:

```yaml
secret: [1,2,3,4] # The secret for signing tokens, It must be the same as the gateway token secret, it is as byte array
tokens: # list of tokens
  #- !Agent # agent token
  # ...
  - !Client # client token
    uid: 00000000-0000-0000-0000-000000000001 # client uid, please use a unique uid for each user
    name: client_name_1 # client name, please use a unique name for each client (not effective yet)
    exp: 1704067200 # expiration time in seconds since epoch (Monday, January 1, 2024 0:00:00 GMT)
    policies: # policies for this client
      permit: true # whitelist mode
      policies: # list of policies
        - !Any # any type of protocols
          - null # agent name, null means any agent
          - true # allow or dency this agent
```

:::note
Note that users can have multiple clients and agents. Narrowlink uses the `uid` field to indicate the user of the client. Therefore, a client can only reach agents that have the same uid. Also, each client must have a unique name.
:::

Run the token generator with the following command to obtain the client token:

```bash

narrowlink-token-generator token-generator.yaml
```

Next, configure the client by creating a file named client.yaml in the folder where you will run the client, and insert the following content:

```yaml
gateway: gateway.domain.tld:443 # Address of the gateway
token: eyJ0eX....kNHYQ_4 # Token for authentication
```

Replace the token field with the value obtained from the token generator, and replace the gateway field with the address of the gateway.

Finally, run the client with the following command to get a list of the agents:

```bash
narrowlink list
AgentInfo {
    name: "agent_name",
    socket_addr: "127.0.0.1:44236",
    since: 2023-0-1T0:0:0-00:00,
    ping: 1,
}
```

You can also use `narrowlink list -h` to get more information about the command or use `narrowlink -h` to get a list of all commands.

:::info
Clients can be restricted to access specific agents and their destinations by using access control policies. Please refer to the [Access Control](/docs/tutorial-extras/access-control) section for more information.

:::

That's it! You have successfully configured the client. Now, you can set up a local proxy server to route your traffic through the agent. For more information, please refer to the Share Network Access section. Additionally, you can check the [Tutorial - Extra](/docs/category/tutorial---extras/) or [Client](/docs/client) sections in the documentation for more information.

That's it! You have successfully configured the client. Now, you can use setup a local proxy server to route your traffic through the agent. Please refer to the [Share Network Access](/docs/tutorial-extras/share-network-access) section for more information. Or you can check the Extract or Client documentation for more information about the client.