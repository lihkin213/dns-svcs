---

copyright:
  years: 2019
lastupdated: "2019-11-12"

keywords: DNS Resolver, CentOS, RHEL, Ubuntu

subcollection: dns-svcs

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}
{:generic: data-hd-programlang="generic"}
{:download: .download}
{:DomainName: data-hd-keyref="DomainName"}



# Updating the DNS resolver for different OSes
{: #updating-dns-resolver}

{{site.data.keyword.cloud}} DNS Services is in Experimental Release. At this time the service is available to whitelisted customers only.
{: important}

This section describes how to update the DNS resolver for the following operating systems:

 - CentOS 7.x
 - RHEL 7.x
 - Ubuntu Linux 18.04 LTS Bionic Beaver
 - Debian GNU/Linux 9.x Stretch/Stable
 
For each operating system, two different methods are provided. The first is a manual method for use when the system is already up and running. The second method makes use of cloud-init to configure the system when it starts. The cloud config file can be pasted or imported into the User Data section on the VSI creation page.

## CentOS 7.x
{: #updating-dns-resolver-centos}

### Method 1: Manually modifying `/etc/resolv.conf`
{: #updating-dns-resolver-centos-resolv}

CentOS 7.x makes use of the `/etc/resolv.conf` file for the DNS resolver configuration. Update this file with the DNS Services nameservers `161.26.0.7` and `161.26.0.8`.

### Method 2: Using cloud-init for CentOS 7.x
{: #updating-dns-resolver-centos-cloud-init}

Cloud config files can be pasted or imported into the User Data section on the VSI creation page.

The following sample cloud config file creates the file `/etc/dhcp/dhclient.conf` and updates the per-interface file `/etc/sysconfig/network-scripts/ifcfg-eth0` for the `eth0` interface.

```
#cloud-config
write_files:
  - path: /etc/dhcp/dhclient.conf
    content: |
      supersede domain-name-servers 161.26.0.7, 161.26.0.8;

runcmd:
  - echo "PEERDNS=yes" >> /etc/sysconfig/network-scripts/ifcfg-eth0
  - echo "DNS1=161.26.0.7" >> /etc/sysconfig/network-scripts/ifcfg-eth0
  - echo "DNS2=161.26.0.8" >> /etc/sysconfig/network-scripts/ifcfg-eth0
  - reboot
```
{:codeblock}

## RHEL 7.x
{: #updating-dns-resolver-rhel}

### Method 1: Manually modifying `/etc/resolv.conf`
{: #updating-dns-resolver-rhel-resolv}

RHEL 7.x makes use of the `/etc/resolv.conf` file for the DNS resolver configuration. Update this file with the DNS Services nameservers `161.26.0.7` and `161.26.0.8`.

### Method 2: Using cloud-init for RHEL 7.x
{: #updating-dns-resolver-rhel-cloud-init}

Cloud config files can be pasted or imported into the User Data section on the VSI creation page.

The following sample cloud config file creates the file `/etc/dhcp/dhclient.conf` and updates the per-interface file `/etc/sysconfig/network-scripts/ifcfg-eth0` for the `eth0` interface.

```
#cloud-config
write_files:
  - path: /etc/dhcp/dhclient.conf
    content: |
      supersede domain-name-servers 161.26.0.7, 161.26.0.8;

runcmd:
  - echo "PEERDNS=yes" >> /etc/sysconfig/network-scripts/ifcfg-eth0
  - echo "DNS1=161.26.0.7" >> /etc/sysconfig/network-scripts/ifcfg-eth0
  - echo "DNS2=161.26.0.8" >> /etc/sysconfig/network-scripts/ifcfg-eth0
  - reboot
```
{:codeblock}

## Ubuntu Linux 18.04 LTS Bionic Beaver
{: #updating-dns-resolver-ubuntu}

### Method 1: Manually modifying `/etc/netplan/50-cloud-init.yaml`
{: #updating-dns-resolver-ubuntu-resolv}

Ubuntu Linux 18.04 makes use of netplan and the `/etc/netplan/50-cloud-init.yaml` file for the DNS resolver configuration. Update this file with the DNS Services nameservers `161.26.0.7` and `161.26.0.8`. To apply the changes run the command:

```console
sudo netplan apply
```
{:pre}

### Method 2: Using cloud-init for Ubuntu Linux
{: #updating-dns-resolver-ubuntu-cloud-init}

Cloud config files can be pasted or imported into the User Data section on the VSI creation page.

If your OS is configured to use 161.26.0.10 and 161.26.0.11 DNS resolvers, you can use the following sample cloud config to issue two `runcmd` commands that overwrite the default nameservers in the `/etc/netplan/50-cloud-init.yaml` file and apply the changes.

If your OS is configured with different name servers, the script must be modified to fit your name servers.
{:note}

```
#cloud-config
runcmd:
  - [sed, -i, 's/161.26.0.10/161.26.0.7/g', /etc/netplan/50-cloud-init.yaml]
  - [sed, -i, 's/161.26.0.11/161.26.0.8/g', /etc/netplan/50-cloud-init.yaml]
  - netplan apply
```
{:codeblock}


## Debian GNU/Linux 9.x Stretch/Stable
{: #updating-dns-resolver-debian}

### Method 1: Manually modifying `/etc/network/interfaces.d/50-cloud-init.cfg`
{: #updating-dns-resolver-debian-resolv}

Debian GNU/Linux 9.x Stretch/Stable uses the `/etc/network/interfaces.d/50-cloud-init.cfg` file for the DNS resolver configuration. Update this file with the DNS Services nameservers `161.26.0.7` and `161.26.0.8`. To apply the changes, reboot the system.

### Method 2: Using cloud-init
{: #updating-dns-resolver-debian-cloud-init}

Cloud config files can be pasted or imported into the User Data section on the VSI creation page.

The following sample cloud config overwrites the nameservers in the `/etc/network/interfaces.d/50-cloud-init.cfg` and reboots the system to apply the changes.

```
#cloud-config
runcmd:
  - sed -i -e "s/\(dns-nameservers \).*/\1161.26.0.7 161.26.0.8/" /etc/network/interfaces.d/50-cloud-init.cfg
  - reboot
```
{:codeblock}
