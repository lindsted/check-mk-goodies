Check_MK goodies
================

Some useful Linux checks for the [Check_MK](https://mathias-kettner.de) monitoring system.

Currently, all the checks are [Check_MK local checks](https://mathias-kettner.de/cms_localchecks.html).
They are used together with the Check_MK Linux agent.

Installation
============

To use these scripts, you need to install the
[Linux Agent for Check_MK](https://mathias-kettner.de/cms_agent_linux.html).

Put the scripts under the "local" directory of the Linux agent, which is
/usr/lib/check_mk_agent/local on most systems. (When using CentOS/Red Hat and
installing the agent from the EPEL repositories, the directory is
/usr/share/check_mk_agent/local.)

osinfo
======

This shell script makes some informations about the Linux OS available to
the Check_MK monitoring console. Those are:

  * [uname](https://linux.die.net/man/1/uname) system and kernel information
  * [lsb_release](https://linux.die.net/man/1/lsb_release) information about the
    installed Linux distribution
  * [hostname](http://man7.org/linux/man-pages/man1/hostname.1.html) output
    about the system name and IP addresses
  * The kernel command line arguments use for booting (from /proc/cmdline)

The check status is always OK, entries in the monitoring console will never
get yellow or red.

The output of the osinfo script is rather static. It is therefore sufficient
to check it once an hour or even less. This can be achieved by putting the
script in a subdirecory called '3600', where the name denotes the number
of seconds until a cached output is renewed.

lscpu
=====

This Perl script parses the output of the [lscpu](https://linux.die.net/man/1/lscpu)
command and makes it available on the Check_MK console. It displays the
CPU model, number of topology of virtual processors, minimum and maximum
CPU frequencies in MHz, and the size of the CPU caches.

The output of the lscpu script is also rather static, it is usually sufficient
to cache it for one hour or more.

mhz
===

The ''mhz'' handles the "CPU MHz" output of the [lscpu](https://linux.die.net/man/1/lscpu)
command, which is usually the current frequency of the first processor. On modern
processors, the frequency is dynamically adjusted according to the system load.
The output is therefore dynamic, the script should be executed on every Check_MK
agent run.

The output also contains performance data, so Check_MK shows up the history
of the mhz value as a diagram.

Note that the script is usually executed in a series of other scripts/programs
started by the Linux agent. The measured CPU frequency can therefore be higher
than the average on the system.
