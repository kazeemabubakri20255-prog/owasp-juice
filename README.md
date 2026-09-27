# Task 6 — Exploiting Application-Based Vulnerabilities

## Overview

This repository contains my practical assignment report for Task 6 of the
CyberProwess Bootcamp 2026: identifying and exploiting common web application
vulnerabilities, documenting evidence, and recommending fixes.

All testing was performed against **local, self-hosted, deliberately vulnerable
applications** running as Docker containers inside an isolated Kali Linux VM.
No production systems, public websites, or third-party infrastructure were
tested at any point.

## Targets

- **OWASP Juice Shop** — run locally via Docker (`bkimminich/juice-shop`), port 3000
- **DVWA (Damn Vulnerable Web Application)** — run locally via Docker
  (`vulnerables/web-dvwa`), port 8081, security level set to Low

## Tools Used

- Burp Suite Community Edition (intercepting proxy)
- FoxyProxy (Firefox proxy switching)
- sqlmap (automated SQL injection testing)
- Docker (hosting the vulnerable lab targets)

## What's Covered

| Task | Vulnerability | Key Finding |
|------|---------------|-------------|
| 6.1  | SQL Injection | Authentication bypass on the login endpoint via `' OR 1=1--`; manual testing succeeded where sqlmap's automated scan did not |
| 6.2  | Cross-Site Scripting | Confirmed DOM-based XSS via the search feature; reflected and stored XSS tested for comparison |
| 6.3  | Broken Access Control / IDOR | Viewed another user's shopping basket by changing a numeric ID (horizontal); found an admin API endpoint with no server-side role check despite a blocked frontend page (vertical) |
| 6.4  | Command Injection & File Upload | Achieved OS command execution through an unsanitized ping utility; uploaded and executed a PHP file with no server-side validation |

Each section of the report includes: the payload used, request/response
evidence captured in Burp Suite, root cause analysis, impact assessment, and
recommended remediation.

## Report

The full write-up, including screenshots and technical evidence for every
finding, is here: `Kazeem_Task6_Practical_Assignment_Report.docx`

## Notes

This was completed as part of a structured, ongoing cybersecurity learning
path alongside other coursework and certifications (ISC2 CC). Setting up the
proxy chain (Firefox → FoxyProxy → Burp Suite) and getting Docker running
correctly took up a fair amount of the actual time spent — a good reminder
that lab setup is its own skill, separate from the exploitation itself.
