The SSH config file supports a wide variety of configuration options that allow you to customize how you connect to remote servers. Here is a comprehensive list of the key options available for use in the SSH config file, along with explanations for each:

### **Commonly Used SSH Config File Options**

1. **Host**: Defines the alias or pattern for the hosts that follow this block.

   - Example:
     ```bash
     Host github.com
     Host myserver.com
     ```

2. **HostName**: Specifies the real hostname or IP address to connect to.

   - Example:
     ```bash
     HostName github.com
     HostName 192.168.1.1
     ```

3. **User**: The username to log in as on the remote machine.

   - Example:
     ```bash
     User git
     ```

4. **Port**: Specifies the port number for the SSH connection (default is 22).

   - Example:
     ```bash
     Port 2222
     ```

5. **IdentityFile**: Specifies the file for the SSH private key to use for authentication.

   - Example:
     ```bash
     IdentityFile ~/.ssh/id_rsa
     ```

6. **IdentitiesOnly**: Forces SSH to use only the identity file specified in `IdentityFile`, ignoring other identities provided by the SSH agent.

   - Example:
     ```bash
     IdentitiesOnly yes
     ```

7. **ForwardAgent**: Enables or disables SSH agent forwarding (allowing remote servers to use your local SSH key).

   - Example:
     ```bash
     ForwardAgent yes
     ```

8. **ProxyCommand**: Specifies a command to use to connect to the server, often used for connecting through a jump host or proxy.

   - Example:
     ```bash
     ProxyCommand ssh proxyuser@proxyhost nc %h %p
     ```

9. **ProxyJump**: Similar to `ProxyCommand`, but a simpler method for jump host setup.

   - Example:
     ```bash
     ProxyJump user@jump.example.com
     ```

10. **ServerAliveInterval**: Sets a timeout interval in seconds for sending keepalive messages to the server.

    - Example:
      ```bash
      ServerAliveInterval 60
      ```

11. **ServerAliveCountMax**: Specifies the maximum number of keepalive messages the client will send without receiving any response from the server before giving up.

    - Example:
      ```bash
      ServerAliveCountMax 3
      ```

12. **StrictHostKeyChecking**: Determines how strict the host key verification should be.

    - `yes`: Only allow known hosts, rejecting new ones.
    - `no`: Automatically accept new host keys.
    - `ask`: Prompt the user to confirm new host keys.
    - Example:
      ```bash
      StrictHostKeyChecking no
      ```

13. **UserKnownHostsFile**: Specifies the file where known host keys are stored.

    - Example:
      ```bash
      UserKnownHostsFile ~/.ssh/known_hosts
      ```

14. **LogLevel**: Specifies the verbosity of logging. Valid options are `QUIET`, `FATAL`, `ERROR`, `INFO`, `VERBOSE`, `DEBUG1`, `DEBUG2`, `DEBUG3`.

    - Example:
      ```bash
      LogLevel DEBUG
      ```

15. **ControlMaster**: Enables the sharing of multiple SSH sessions over a single connection.

    - Example:
      ```bash
      ControlMaster auto
      ```

16. **ControlPath**: Specifies the path to the control socket for connection multiplexing.

    - Example:
      ```bash
      ControlPath ~/.ssh/sockets/%r@%h:%p
      ```

17. **ControlPersist**: Keeps the master connection open in the background for a specific amount of time or indefinitely.

    - Example:
      ```bash
      ControlPersist yes
      ```

18. **Compression**: Enables compression for the SSH connection.

    - Example:
      ```bash
      Compression yes
      ```

19. **LocalForward**: Sets up local port forwarding. Forward traffic from a local port to a remote address and port.

    - Example:
      ```bash
      LocalForward 8080 127.0.0.1:80
      ```

20. **RemoteForward**: Sets up remote port forwarding. Forward traffic from a remote port on the server to a local address and port.

    - Example:
      ```bash
      RemoteForward 9090 127.0.0.1:8080
      ```

21. **GSSAPIAuthentication**: Enables or disables GSSAPI-based authentication.

    - Example:
      ```bash
      GSSAPIAuthentication no
      ```

22. **SendEnv**: Specifies which environment variables should be sent to the server.

    - Example:
      ```bash
      SendEnv LANG LC_*
      ```

23. **ForwardX11**: Enables X11 forwarding, allowing you to run graphical applications remotely.

    - Example:
      ```bash
      ForwardX11 yes
      ```

24. **ForwardX11Trusted**: Specifies whether X11 forwarding should be trusted.

    - Example:
      ```bash
      ForwardX11Trusted yes
      ```

25. **BatchMode**: Disables password/passphrase prompting, useful for automated scripts.

    - Example:
      ```bash
      BatchMode yes
      ```

26. **PermitLocalCommand**: Allows local commands to be executed by the `LocalCommand` directive.

    - Example:
      ```bash
      PermitLocalCommand yes
      ```

27. **LocalCommand**: Specifies a command to execute locally after successfully connecting to the server.

    - Example:
      ```bash
      LocalCommand echo "Connected to %h"
      ```

28. **DynamicForward**: Specifies a SOCKS proxy on a local port for dynamic forwarding.

    - Example:
      ```bash
      DynamicForward 1080
      ```

29. **KexAlgorithms**: Specifies the key exchange algorithms used by SSH.

    - Example:
      ```bash
      KexAlgorithms curve25519-sha256@libssh.org
      ```

30. **Ciphers**: Specifies the ciphers to use for encryption.

    - Example:
      ```bash
      Ciphers aes128-ctr,aes192-ctr,aes256-ctr
      ```

31. **MACs**: Specifies the message authentication codes used by SSH.

    - Example:
      ```bash
      MACs hmac-sha2-512,hmac-sha2-256
      ```

32. **RekeyLimit**: Specifies how much data or time can pass before SSH renegotiates the encryption key.

    - Example:
      ```bash
      RekeyLimit 1G 1h
      ```

33. **VisualHostKey**: Shows a visual representation of the remote host key when connecting.

    - Example:
      ```bash
      VisualHostKey yes
      ```

34. **CanonicalizeHostname**: Enables canonicalization of the hostname, useful when using a non-standard DNS or search domain.

    - Example:
      ```bash
      CanonicalizeHostname yes
      ```

35. **CanonicalizeMaxDots**: Limits the number of domain name components in canonicalized names.

    - Example:
      ```bash
      CanonicalizeMaxDots 1
      ```

36. **CanonicalDomains**: Specifies search domains to append when canonicalizing hostnames.
    - Example:
      ```bash
      CanonicalDomains example.com
      ```

### **Example of SSH Config File with Various Options**

Here’s an example SSH config file using many of the above options:

```bash
# Configuration for personal GitHub account
Host github-personal
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_rsa_github_account1
    IdentitiesOnly yes
    ForwardAgent yes
    ServerAliveInterval 60
    ServerAliveCountMax 3
    Compression yes

# Configuration for work GitHub account
Host github-work
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_rsa_github_account2
    IdentitiesOnly yes
    ForwardX11 yes
    StrictHostKeyChecking no

# Remote server configuration with jump host
Host myserver
    HostName myserver.com
    User myuser
    IdentityFile ~/.ssh/id_rsa_work
    ProxyJump jumpuser@jumphost.example.com
    LocalForward 8080 localhost:80
    RemoteForward 9090 localhost:8080
    LogLevel DEBUG3
    ControlMaster auto
    ControlPath ~/.ssh/sockets/%r@%h:%p
    ControlPersist yes
```

### **Commenting Out Options**

To comment out a setting, just add a `#` at the beginning of the line. This will disable the setting.

For example:

```bash
# HostName github.com  # Commented out, this won't be used
# User git
```

This list gives you a wide range of flexibility when configuring SSH for different hosts. Let me know if you'd like more details or specific examples for any of the options!

### **Global Options**

```
**Host:** Specifies the hostname or IP address of the remote host.
**Hostname:** Overrides the hostname in the Host directive.
**Port:** Sets the port number for the connection.
**User:** Sets the username for the connection.
**IdentityFile:** Specifies the path to the private key file for authentication.
**IdentitiesOnly:** Restricts authentication to the specified IdentityFile.
**PreferredAuthentications:** Specifies the preferred authentication methods.
**ForwardX11:** Enables X11 forwarding.
**ForwardAgent:** Enables SSH agent forwarding.
**ForwardX11Trusted:** Enables X11 forwarding without security checks.
**ForwardAgentTrusted:** Enables SSH agent forwarding without security checks.
**GatewayPorts:** Enables gateway port forwarding.
**LocalForward:** Specifies a local port forwarding rule.
**RemoteForward:** Specifies a remote port forwarding rule.
**DynamicForward:** Enables dynamic port forwarding.
**AddressFamily:** Specifies the IP address family for the connection.
**ServerAliveInterval:** Sets the interval for sending keep-alive messages.
**ServerAliveCountMax:** Sets the maximum number of consecutive keep-alive failures before the connection is closed.
**StrictHostKeyChecking:** Controls host key checking.
**TCPKeepAlive:** Enables TCP keep-alive messages.
**UseThrottle:** Enables bandwidth throttling.
**ThrottleDelay:** Sets the delay between packets when throttling is enabled.
**ThrottleRate:** Sets the maximum bandwidth when throttling is enabled.
**ExitOnForwardFailure:** Exits the SSH client if a port forwarding attempt fails.
**LogLevel:** Sets the logging level.
**BatchMode:** Disables interactive prompts.
**NoEcho:** Disables echoing of input.
**NoAgentForwarding:** Disables SSH agent forwarding.
**NoUserKnownHostsFile:** Disables known hosts file checking.
**NoHostVerification:** Disables host key verification.
**NoCompression:** Disables compression.
**NoDelay:** Disables Nagle's algorithm.
**NoDelayPing:** Disables pinging of the remote host.
**NoAffinity:** Disables CPU affinity.
**NoKeepAlive:** Disables keep-alive messages.
**NoKnownHosts:** Disables known hosts file checking.
**NoProtocolCompat:** Disables protocol compatibility.
**NoStrictHostKeyChecking:** Disables strict host key checking.
**NoTTY:** Disables pseudo-terminal allocation.
**NoVerifyHostKeyDNS:** Disables DNS-based host key verification.
**NoVerifyHostKeyRSA:** Disables RSA host key verification.
**NoVerifyHostKeyDSA:** Disables DSA host key verification.
**NoVerifyHostKeyECDSA:** Disables ECDSA host key verification.
**NoVerifyHostKeyED25519:** Disables Ed25519 host key verification.
**NoVerifyHostKeyECDH:** Disables ECDH host key verification.
**NoVerifyHostKeySSH1:** Disables SSH-1 host key verification.
**NoVerifyHostKeySSH2:** Disables SSH-2 host key verification.
```
