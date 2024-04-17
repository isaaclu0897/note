
As Github mentioned, the company will block ssh connections, so Github established a connection to SSH over HTTPS, allowing you to operate git through the HTTPS protocol.

> Sometimes, firewalls refuse to allow SSH connections entirely. If using HTTPS cloning with credential caching is not an option, you can attempt to clone using an SSH connection made over the HTTPS port. Most firewall rules should allow this, but proxy servers may interfere.

### Testing connections

You can test using SSH over http behind a Proxy by following the command
```bash
$ ssh -T -p 443 git@ssh.github.com -o "ProxyCommand nc -X connect -x <PROXYHOST>:<PROXYPORT> %h %p"
> Hi USERNAME! You've successfully authenticated, but GitHub does not
> provide shell access.
```

### Configure SSH Config

Finally, you can use ssh into `git@github.com` and persist the configuration
```bash
# ~/.ssh/config
Host github.com
    User git
    HostName ssh.github.com
    Port 443
    ProxyCommand nc -X connect -x <PROXYHOST>:<PROXYPORT> %h %p

# Set default value using Host * section
# Since the first obtained value for each parameter is used,
# more host-specific declarations should be given near the beginning of the file,
# and general defaults at the end. "So it should be placed at the end."
# Reference: man ssh_config
Host *
    User root
```

### Reference article

> [Using ssh over the https port](https://docs.github.com/en/authentication/troubleshooting-ssh/using-ssh-over-the-https-port)
> [Using github ssh behind http proxy](https://adangel.org/2020/10/15/github-behind-proxy/)