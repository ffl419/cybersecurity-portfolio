# Ubuntu Penetration Testing Lab

## Project Overview

This project documents my first beginner penetration testing lab using Ubuntu, Docker, Nmap, Firefox Developer Tools, and OWASP Juice Shop.

The purpose of this lab was to create a controlled environment where I could practice basic penetration testing concepts, including network reconnaissance, service detection, client-side source inspection, and web application security challenges.

All security testing was performed against my own local OWASP Juice Shop environment.

---

## Tools Used

- Ubuntu Linux
- Docker
- Nmap
- OWASP Juice Shop
- Firefox
- Firefox Developer Tools

---

## 1. Ubuntu Preparation

I started by updating Ubuntu:

```bash
sudo apt update
```

I then upgraded the installed packages:

```bash
sudo apt upgrade -y
```

---

## 2. Docker Installation

I installed Docker:

```bash
sudo apt install docker.io -y
```

I checked whether Docker was running:

```bash
sudo systemctl status docker
```

I then tested Docker:

```bash
sudo docker run hello-world
```

The successful Hello World test confirmed that Docker was working.

---

## 3. OWASP Juice Shop Setup

I downloaded the OWASP Juice Shop Docker image:

```bash
sudo docker pull bkimminich/juice-shop
```

I launched OWASP Juice Shop and mapped port 3000 on Ubuntu to port 3000 inside the Docker container:

```bash
sudo docker run -d -p 3000:3000 bkimminich/juice-shop
```

I accessed the application through Firefox at:

```text
http://localhost:3000
```

### OWASP Juice Shop Running

![OWASP Juice Shop running locally](screenshots/Screenshot1.jpg)

This confirmed that my intentionally vulnerable training application was running locally.

---

## 4. Installing Nmap

I installed Nmap:

```bash
sudo apt install nmap -y
```

I verified the installation:

```bash
nmap --version
```

---

## 5. Basic Network Reconnaissance

I performed my first Nmap scan against my own Ubuntu loopback address:

```bash
nmap 127.0.0.1
```

The scan identified open TCP ports on my local machine, including port 3000.

Port 3000 was important because OWASP Juice Shop was running on that port.

### Basic Nmap Scan

![Basic Nmap scan](screenshots/Screenshot2.jpg)

### What I Learned

This introduced me to basic network reconnaissance and how Nmap can identify open ports on a target system.

---

## 6. Nmap Service Detection

After discovering port 3000, I performed a focused service-detection scan:

```bash
nmap -sV -p 3000 127.0.0.1
```

### Command Breakdown

- `nmap` - Runs the Nmap scanner
- `-sV` - Performs service/version detection
- `-p 3000` - Scans only port 3000
- `127.0.0.1` - Targets my own local computer

The results showed that TCP port 3000 was open.

The service-detection output also returned HTTP information associated with the OWASP Juice Shop application.

### Service Detection - Part 1

![Nmap service detection part 1](screenshots/Screenshot3A.jpg)

### Service Detection - Part 2

![Nmap service detection part 2](screenshots/Screenshot3B.jpg)

### What I Learned

I learned the difference between simply discovering an open port and performing additional service detection against that port.

---

# Web Application Security Testing

After completing basic reconnaissance, I worked through several beginner challenges included with OWASP Juice Shop.

---

## 7. Score Board Challenge

The first challenge involved discovering the hidden Score Board.

The Score Board was not available through the application's normal navigation menu.

I opened Firefox Developer Tools and used the Debugger to inspect the client-side JavaScript.

I searched the JavaScript files for:

```text
score-board
```

During the investigation, I discovered a client-side route:

```text
routerLink:'/score-board'
```

I then navigated to:

```text
http://localhost:3000/#/score-board
```

OWASP Juice Shop confirmed that I successfully discovered the hidden Score Board.

### Challenge Completed

![Score Board challenge completed](screenshots/Screenshot4.jpg)

### What I Learned

This challenge demonstrated that functionality hidden from normal application navigation can still be referenced within client-side JavaScript.

It also gave me hands-on experience using browser developer tools during security testing.

---

## 8. DOM XSS Challenge

The second web application challenge I completed was DOM XSS.

This training exercise demonstrated how unsafe handling of user-controlled input in frontend JavaScript can cause content to be improperly inserted into the Document Object Model (DOM).

OWASP Juice Shop confirmed that I successfully completed the challenge.

### Challenge Completed

![DOM XSS challenge completed](screenshots/Screenshot5.jpg)

### What I Learned

This challenge introduced me to DOM-based Cross-Site Scripting concepts.

I learned that user-controlled input must be handled carefully, including when the processing occurs inside the browser.

---

## 9. Bonus Payload Challenge

The third challenge I completed was the Bonus Payload challenge.

This exercise built on concepts demonstrated during the DOM XSS challenge.

The application processed specially crafted content through the search functionality and displayed embedded content inside the search results.

OWASP Juice Shop confirmed that I successfully completed the challenge.

### Challenge Completed

![Bonus Payload challenge completed](screenshots/Screenshot6.jpg)

### What I Learned

This exercise further demonstrated how unsafe handling of HTML and other user-controlled content can affect the content displayed by a web application.

---

# Skills Practiced

Through this project, I gained hands-on experience with:

- Ubuntu Linux
- Linux terminal commands
- Docker containers
- OWASP Juice Shop
- Nmap
- Network reconnaissance
- TCP ports
- Service detection
- HTTP services
- Firefox Developer Tools
- Client-side JavaScript inspection
- Application route discovery
- Web application security testing
- DOM-based XSS concepts
- Security lab documentation

---

# Commands Used

The main commands used during this project were:

```bash
sudo apt update
sudo apt upgrade -y

sudo apt install docker.io -y
sudo systemctl status docker
sudo docker run hello-world

sudo docker pull bkimminichd in a controlled local lab environment.

OWASP Juice Shop is an intentionally vulnerable web application designed for cybersecurity education and security testing.

All testing documented in this project was performed against systems and applications under my control.

The techniques documented in this project are intended for educational and authorized security testing purposes only.

---

# Key Takeaways

This project helped me understand that penetration testing involves more than simply running security tools.

I practiced:

1. Building a controlled security testing environment
2. Running a vulnerable application inside Docker
3. Performing basic reconnaissance with Nmap
4. Identifying open ports
5. Performing focused service detection
6. Inspecting client-side JavaScript
7. Discovering hidden application functionality
8. Learning basic DOM XSS concepts
9. Documenting cybersecurity findings

Most importantly, this project gave me practical experience performing and documenting cybersecurity exercises in a controlled environment.

---

# Future Improvements

As I continue developing my cybersecurity skills, I plan to expand this lab by:

- Completing additional OWASP Juice Shop challenges
- Learning additional Nmap features
- Studying web application vulnerabilities
- Practicing vulnerability identification and remediation
- Improving my penetration testing documentation and reporting skills

---

# Disclaimer

This project is for educational purposes only.

Security testing should only be performed against systems that you own or have explicit authorization to test.
