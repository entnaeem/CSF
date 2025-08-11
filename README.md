# ConfigServer Security & Firewall (CSF) Installation Guide

**Copyright © 2006–2018, Way to the Web Limited**  
**URL:** [http://www.configserver.com](http://www.configserver.com)  
**Email:** sales@waytotheweb.com  

---

## Installation

Installation is quite straightforward:

```bash
cd /usr/src
rm -fv csf.tgz
wget -O csf.tgz https://github.com/entnaeem/CSF/blob/main/csf.tgz
tar -xzf csf.tgz
cd csf
sh install.sh
```

Next, test whether you have the required iptables modules:

```bash
perl /usr/local/csf/bin/csftest.pl
```

> **Note:** Don’t worry if you cannot run all the features, as long as the script doesn’t report any **FATAL** errors.

You should not run any other iptables firewall configuration script.  
For example, if you previously used APF+BFD, remove them to avoid conflicts:

```bash
sh /usr/local/csf/bin/remove_apf_bfd.sh
```

That’s it! You can then configure **CSF** and **LFD** by reading:

- `/etc/csf/csf.conf`
- `/etc/csf/readme.txt`

---

## cPanel & DirectAdmin Notes
- Installation is preconfigured to work with all standard ports open.
- CSF auto-configures your SSH port if it’s running on a non-standard port.
- CSF auto-whitelists your connected IP address (where possible) on installation.

---

## Kernel Logging
Ensure that the kernel logging daemon (**klogd**) is enabled.  
On some VPS (e.g., RedHat/CentOS v5), this may be disabled.

Check `/etc/init.d/syslog` and ensure that any `klogd` lines are **not** commented out.  
If you make changes, restart syslog.

---

## Perl Modules

While most are included in a standard Perl installation, you may need to install:

### On RPM-based systems:
```bash
yum install perl-libwww-perl.noarch perl-LWP-Protocol-https.noarch perl-GDGraph
```

### On APT-based systems:
```bash
apt-get install libwww-perl liblwp-protocol-https-perl libgd-graph-perl
```

### Via CPAN:
```bash
perl -MCPAN -eshell
cpan> install LWP LWP::Protocol::https GD::Graph
```

---

## InterWorx Installation

1. Enable CSF in:
   ```
   InterWorx > NodeWorx > Plugins > CSF
   ```
2. See the InterWorx section in:
   ```
   /etc/csf/readme.txt
   ```

---

## Webmin Module Installation/Upgrade

1. Install CSF as above.  
2. Install the CSF Webmin module:  
   ```
   Webmin > Webmin Configuration > Webmin Modules
   From local file: /usr/local/csf/csfwebmin.tgz > Install Module
   ```

---

## Uninstallation

Removing CSF and LFD:

```bash
cd /etc/csf
sh uninstall.sh
```
