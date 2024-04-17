
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

https://docs.github.com/en/authentication/troubleshooting-ssh/using-ssh-over-the-https-port

https://adangel.org/2020/10/15/github-behind-proxy/