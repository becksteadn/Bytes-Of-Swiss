# Bytes of Swiss

| |  |  |
|--------|--------|-------|
| Master | [![Master](https://circleci.com/gh/becksteadn/Bytes-Of-Swiss/tree/master.svg?style=svg)](https://circleci.com/gh/becksteadn/Bytes-Of-Swiss/tree/master) | [![Build status](https://ci.appveyor.com/api/projects/status/q1rarjol6yxy1g4t/branh/master?svg=true)](https://ci.appveyor.com/project/becksteadn/bytes-of-swiss/branch/master) |
| Build | [![Build](https://circleci.com/gh/becksteadn/Bytes-Of-Swiss/tree/build.svg?style=svg)](https://circleci.com/gh/becksteadn/Bytes-Of-Swiss/tree/build) | [![Build status](https://ci.appveyor.com/api/projects/status/q1rarjol6yxy1g4t/branch/build?svg=true)](https://ci.appveyor.com/project/becksteadn/bytes-of-swiss/branch/build) |    

Bytes of Swiss is a library of no frills Ansible roles that can be combined to make a vulnerable virtual machine. This can be used for cybersecurity King of the Hill competitions, penetration testing practice, or to test both offensive and defense tools. 

Vulnerabities are located in `roles/vuln` and pull in services like an FTP server or database from `roles/service` as needed. The `roles/misc` directory contains helper roles like adding a new user.  

All roles are tested with [Molecule](https://molecule.readthedocs.io/en/latest/) and [Vagrant](https://www.vagrantup.com/).

## Example 

This makes an existing machine vulnerable by making a new bind shell every minute, creating a PHP shell, and running telnet.

```
---
- hosts: vulnerable
  roles:
    - vuln/bind-shell
    - vuln/web-shell
    - service/telnet
```

### Try It Out

Download the repository.

`git clone https://github.com/becksteadn/Bytes-Of-Swiss.git`

Start the example VM with Vagrant

`vagrant up`

Run the example playbook.

`ansible-playbook -i vagrant.ini example.yml`

Exploit the machine.

* Web shell
  * `curl localhost:8080/cmd.php?cmd=cat%20/etc/passwd`
* Telnet
  * `telnet localhost 2323`
  * Log in with `vagrant:vagrant`
* Bind shell
  * `vagrant ssh`
  * `sudo netstat -tunlp`
  * Observe the processes listening on high ports. Connect to one with `nc` and run some bash commands. 

## Contributing

Any help or suggestions are greatly appreciated! Check out `CONTRIBUTING.md` for details.