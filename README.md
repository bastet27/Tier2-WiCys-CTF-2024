# WiCys SANS Security Scholarship
# Tier 2 CTF Challenge

## :green_book: Introduction

I have had the opportunity to be a part of the [WiCys Security Training Scholarship](https://www.wicys.org/benefits/security-training-scholarship/). I've passed the first stage, which was a CTF challenge. Only 500 out of 2000 people moved on to the next stage. 

Stage 2 consists of gamified learning through [TryHackMe](www.tryhackme.com). I went through the Intro to Cybersecurity, Pre Security, Web Fundamentals, Jr. Pen Tester, and TryHackMe's new Cybersecurity 101 training rooms. I am now entering the final portion of the stage, which is a CTF challenge hosted on TryHackMe.

I did not think about doing a write-up to keep track of my learning progress before. I actually only recently learned of doing write-ups through GitHub. I'll be taking notes of how I solve this CTF challenge, but I won't be providing the exact answers.

## :one: 1. Start the AttackBox.

I will be using the AttackBox built in to THM.

## :two: 2. Web Exploitation(Easy) Bruteforce Me

### Level Hint: I forgot my credentials yet again... Can you guess them for me? I think my user was either pedro, admin or root.

### Solution:

It's good to know which wordlists are available on your machine. Use the following command to navigate to the wordlists folder of your machine.
```
cd /usr/share/wordlists
```
Use the command `ls` to list the available wordlists.

I'm going to start with `fasttrack.txt`

Navigate to the target machine by entering the target IP in a browser. I am using Firefox.

########################## edit text here ### CTF Write-Up: Brute-Forcing Login with Hydra

#### **Steps**

1. **Navigate to the Target**
   - Open the target web application at `http://10.10.216.219` in your browser.

2. **Inspect the Page**
   - Use browser developer tools (`F12` or right-click > "Inspect") to analyze the login form and understand its structure.

3. **Test with a Sample Password**
   - Enter the username `admin` and a sample password like `admin` to observe the behavior of the application.

4. **Inspect the POST Form**
   - Check the form submission in the **Network** tab of the browser developer tools.
   - Note the request URL and fields used in the POST request (e.g., `user` and `pass`).

5. **Edit & Resend the Request**
   - Right-click the POST request in the Network tab and select "Edit & Resend."
   - Experiment with different credentials to confirm how the server handles incorrect logins.

6. **Analyze the Request Body**
   - Review the structure of the request body (e.g., `user=admin&pass=test`).
   - Identify the error message (e.g., `Invalid credentials`) returned by the server for incorrect logins.

7. **Craft the Hydra Command**
   - Use Hydra to automate brute-forcing the login form. The successful command:
     ```bash
     hydra -l admin -P /usr/share/wordlists/fasttrack.txt 10.10.216.219 http-post-form "/:user=^USER^&pass=^PASS^:F=Invalid credentials"
     ```

8. **Capture the CTF Flag**
   - Once Hydra finds the correct credentials, log in to the application and retrieve the flag.

#### **Key Hydra Command**
```bash
hydra -l admin -P /usr/share/wordlists/fasttrack.txt 10.10.216.219 http-post-form "/:user=^USER^&pass=^PASS^:F=Invalid credentials"
```

#### **Outcome**
- The correct credentials were brute-forced using Hydra.
- The flag was retrieved from the target application after successful login. 🎉


### Notes:
