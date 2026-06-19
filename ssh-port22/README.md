# SSH (Port 22): Enumeration and Authentication Testing

## Goal
Understand how SSH works and how it is tested and attacked, using port
22 on a lab target. Focus on identifying the service, examining its
authentication methods, and seeing how login attempts appear in the
target's logs — connecting the attacker's actions to the defender's view.

## Environment
| Host          | OS               | Role               |
|---------------|------------------|--------------------|
| Old laptop    | Kali Linux       | Attacker / host    |
| VirtualBox VM | Metasploitable 2 | Vulnerable target  |

Testing was performed on an isolated host-only network.

## Steps

**1. Reconnaissance.** Scanned the target for the SSH service and its
version:
```bash
nmap -p 22 -sV <TARGET_IP>
```
Port 22 was open, running OpenSSH 4.7p1 — an old version, typical of the
deliberately outdated Metasploitable 2 target.

**2. Authentication analysis.** Checked which authentication methods the
SSH server offered:
```bash
ssh -v <USER>@<TARGET_IP>
```
The verbose output listed the authentication methods the server accepted
(e.g. password authentication).

**3. Simulated login attempts and log review.** Made login attempts
against the service, then reviewed the resulting entries in the target's
authentication log:
```bash
cat /var/log/auth.log
```
The log recorded each attempt, including timestamps and the source IP of
the attacker machine.

## Result
The authentication log captured the login attempts from the Kali host,
showing how every connection — successful or failed — is recorded on the
target. The screenshot below shows these log entries.

<img width="1280" height="1706" alt="SSH auth log entries" src="https://github.com/user-attachments/assets/a9501fd5-3f6d-4228-a78b-a507d45df758" />

## Why It Matters
- SSH (port 22) is one of the most commonly exposed and targeted
  services on internet-facing hosts.
- Weak or default credentials are a frequent entry point — brute-force
  and credential-guessing attacks against SSH are constant in the real
  world.
- Reviewing the auth logs is the bridge into the defensive side: every
  login attempt leaves a trace, which is exactly what a SIEM or
  monitoring setup would alert on. This is the link between offense and
  detection.
- Maps to MITRE ATT&CK **T1021.004 – Remote Services: SSH**.

## Lessons Learned
SSH was confusing at first — understanding the different authentication
methods and how the handshake works took some effort, but testing it
hands-on made it click. Seeing my own login attempts show up in the
target's logs was the moment the attacker/defender relationship became
concrete.
