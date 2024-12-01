# My Suckless Void Video Editing Workstation

Ansible-based setup of my video editing workstation. Based on `dwm` window manager from
Suckless software, but will probably work with something else just as well.

## TL;DR

Install Void Linux (bare bones, without any desktop environment).

### Prepare to Provision Locally

Become `root` (`sudo -i`).

Run

```bash
xbps-install -Su xbps
xbps-install -Su
xbps-install git vim python3-pipx

pipx ensurepath
pipx completions
pipx install --include-deps ansible

git clone https://github.com/tvendelin/void_desktop.git 
cd void_desktop
```

### Prepare to Provision over SSH

Enable `sshd`, optionally create an SSH key pair on the ansible control host, add the
public key to `~/.ssh/authorized_hosts` on the target. Make sure Python is installed  on
the target host before running Ansible.

### Review the Playbook

The playbook includes two plays. The first one is to be executed as `root` (hence the `-K`
option below). The other one clones a git repo with my dotfiles and copies the dotfiles to
the user's home. In all likelihood you've got your own dotfiles, so change according to
you needs.

Edit (or have a look at) `base_install.yaml`. The `vars` are set to their defaults, but
you might want to change some.

For SSH-based provisioning, change `localhost` to the actual target host. Add the
authentication parameters.

### Run

```
ansible-playbook base_install.yaml -K
```

Manually install DaVinci Resolve (requires clicking through EULA, and a few other things).
