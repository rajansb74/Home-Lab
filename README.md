# Home-Lab

An ethical hacking home lab built on repurposed hardware to practice
penetration testing and defensive concepts in a fully isolated
environment. Built and documented incrementally as I learn.

## Environment

| Host | OS | Role |
|------|----|----|
| Old laptop | Kali Linux | Attacker / host machine |
| VirtualBox VM | Metasploitable 2 | Vulnerable target |

All testing is performed on an isolated host-only network — nothing is
exposed beyond the lab.

## Scenarios

- [First Exploit - Metasploitable 2](metasploit-exploit/README.md)
- [SSH (Port 22) - Enumeration & Auth Testing](ssh-port22/README.md)

## Learning Notes

- [Networking notes (subnetting, CIDR, ports)](notes/networking.md)

## Next Steps

- Expand the lab with additional vulnerable targets
- Explore further services/ports and document each as a scenario
- Add a SIEM (e.g. Wazuh) to practice the defensive side
