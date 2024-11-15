# WiCys SANS Security Scholarship
# Tier 2 CTF Challenge

## :green_book: Introduction

I have had the opportunity to be a part of the [WiCys Security Training Scholarship](https://www.wicys.org/benefits/security-training-scholarship/). I've passed the first stage, which was a CTF challenge. Only 500 out of 2000 people moved on to the next stage. 

Stage 2 consists of gamified learning through [TryHackMe](www.tryhackme.com). I went through the Intro to Cybersecurity, Pre Security, Web Fundamentals, Jr. Pen Tester, and TryHackMe's new Cybersecurity 101 training rooms. I am now entering the final portion of the stage, which is a CTF challenge hosted on TryHackMe.

I did not think about doing a write-up to keep track of my learning progress before. I actually only recently learned of doing write-ups through GitHub. I'll be taking notes of how I solve this CTF challenge, but I won't be providing the exact answers.

## :one: 1. Start the AttackBox.

I will be using the AttackBox built in to THM.

## :two: 2. Web Exploitation(Easy) Bruteforce Me

### Task Hint: I forgot my credentials yet again... Can you guess them for me? I think my user was either pedro, admin or root.

### Solution:

It's good to know which wordlists are available on your machine. Use the following command to navigate to the wordlists folder of your machine.
```
cd /usr/share/wordlists
```
Use the command `ls` to list the available wordlists.

I'm going to start with `fasttrack.txt`

Navigate to the target machine by entering the target IP in a browser. I am using Firefox.

The page is a basic login screen. 

Use browser developer tools (`F12` or right-click > "Inspect") to analyze the login form and understand its structure.

Since we are trying to brute force a web application, I am going to go to the Network tab in the developer tools to review GET and POST.

I'm going to try a simple password combo on one of the usernames provided.

I tried `admin` and `admin`

I can see a POST submission.

Right-click the POST request in the Network tab and select "Edit & Resend."
Experiment with different credentials to confirm how the server handles incorrect logins.

Review the structure of the request body (e.g., `user=admin&pass=test`).

Identify the error message (e.g., `Invalid credentials`) returned by the server for incorrect logins.

I am going to be using Hydra to try to brute force.

     ```
     hydra -l admin -P /usr/share/wordlists/fasttrack.txt 10.10.216.219 http-post-form "/:user=^USER^&pass=^PASS^:F=Invalid credentials"
     ```

Hydra was able to quicky find a password for the admin account.

Trying that password on the web page, was able to get the flag.

### Notes:

This one was suprisingly more difficult than I thought, and it was just the first challenge.
https://infinitelogins.com/2020/02/22/how-to-brute-force-websites-using-hydra/

## :three: 3. Web Exploitation(Easy) Endpoint

### Task Hint: You’ve been summoned to investigate a mysterious web application that has recently come under scrutiny. Rumors circulate about hidden messages and secrets concealed within the app’s architecture. As a seasoned investigator, your mission is to navigate the web application, searching for clues embedded in its responses.

### Solution

### Notes

## :six: Web Exploitation [Easy] Time Travel

### Task Hint: 
To find this flag, you must travel back in time with the Wayback machine!
Targeted website: https://www.embeddedhacker.com
Targeted time: 2 January 2020

### Solution

Using the [Wayback Machine](https://web.archive.org/) I typed in the URL and selected the date. Scrolling through the page I was able to find the flag.

## :one::one: 11. Cryptography (Easy) B4sed

### Task Hint: Can you decode this?

KZCWQTTFGJJHAWSHGUYFQMSWGRRUOVTKMRDDS2CYGJJHMZCXJJZVUVRZNFHEQTTMKAZTAPI=

### Solution
I used the Magic tool in CyberChef and was able to retrieve the flag.

## :one::two: 

Task Hint: You didn’t finish studying for your SANS WiCyS exam because you were too busy pwning TryHackMe boxes. Before the exam starts, you tell your friend Gonzo that you need his help.

Quick on his feet, Gonzo devises a genius plan: He will encrypt a message and send it to you. That way, if you get caught, the teacher will have no proof you’re cheating. Genius!

During the exam,  Gonzo notices your distress signal and sends you this message:

TAe1a_H{nwr_c2_c4}Mss_3b

But, with all the stress from the exam, you forgot the decryption key. You remember Gonzo mentioning a rail. Can you figure it out before time runs out?

### Solution

This looks like it is using a Rail Fence Cipher.

Using dCode I was able to solve the flag.

