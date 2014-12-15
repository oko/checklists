# Basic Ubuntu/Debian Server Setup Checklist

- [ ] Update server, reboot, and install useful stuff.
    - [ ] `apt-get update && apt-get upgrade && reboot`
    - [ ] `apt-get install salt-minion git vim tmux zsh`
- [ ] Set up main user and group
    - [ ] `groupadd -g <5000+ gid> <main user group>`
    - [ ] `useradd -m -u <5000+ uid> -g <main user group> <main user name>`
    - [ ] `passwd <main user name>`
    - [ ] `su <main user name>`
        - [ ] `mkdir ~/.ssh`
        - [ ] `vim ~/.ssh/authorized_keys`
- [ ] Set up firewall
    - [ ] `curl -LSso ip4tables.sh https://gist.githubusercontent.com/oko/8103bb276dbc12ea0ad8/raw`
    - [ ] `curl -LSso ip6tables.sh https://gist.githubusercontent.com/oko/ba552a0612a60a03f45f/raw`
    - [ ] Edit `ip4tables.sh` and `ip6tables.sh` as necessary.
    - [ ] `sh ip4tables.sh && sh ip6tables.sh`
    - [ ] `iptables-save > /etc/iptables.rules`
    - [ ] `ip6tables-save > /etc/ip6tables.rules`
    - [ ] Add `pre-up iptables-restore < /etc/iptables.rules` to interfaces in `/etc/network/interfaces`
- [ ] Configure Salt minion in `/etc/salt/minion`
    - [ ] `file_client: local`
    - [ ] File roots
        ```
        file_roots:
          base:
            - /srv/salt/subdir
        ```
    - [ ] `service salt-minion restart`
    - [ ] `mkdir -p /srv/salt`
    - [ ] `git clone https://gitreposite.com/user/cfgrepo.git /srv/salt/subdir`
    - [ ] `salt-call state...`
