🛡️ Bug Bounty Recon & Vulnerability Research Toolkit

A professional-grade Reconnaissance & Vulnerability Assessment framework built for Bug Bounty Hunters and Security Researchers.
This toolkit helps you systematically map the attack surface, discover hidden assets, and identify common & advanced web vulnerabilities using industry-standard tools.

💡 From subdomain enumeration to advanced fuzzing — everything follows a clean, real-world bug bounty workflow.

🚀 Methodology Overview

The recon process is divided into 5 structured phases, designed to maximize coverage while minimizing noise.

🔍 Phase 1: Subdomain Enumeration (Passive & Active)

Identify the full external footprint of the target using multiple intelligence sources.

🧰 Tools Used

VirusTotal – Initial domain intelligence

Subfinder – Fast & passive subdomain discovery

Assetfinder – Additional asset discovery

📌 Commands
subfinder -d target.com -o subdomains.txt
assetfinder -subs-only target.com >> subdomains.txt
sort -u subdomains.txt -o subdomains.txt

🌐 Phase 2: Live Host Discovery & Probing

Filter out dead assets and focus only on reachable & responsive hosts.

🧰 Tool Used

Httpx – HTTP probing, status codes & tech detection

📌 Command
cat subdomains.txt | httpx -silent -o live_subdomains.txt


✅ Optional precision:

httpx -mc 200

🧭 Phase 3: Endpoint & Parameter Mining

Discover endpoints, parameters, and hidden inputs where vulnerabilities usually live.

🧰 Tools Used

Waybackurls / GAU – Historical URL extraction

ParamSpider – Automated parameter discovery

Grep – Pattern-based sensitive endpoint detection

🔎 Interesting Patterns
admin | login | backup | config | test | old | dev

🧪 Phase 4: Vulnerability Scanning (Automated)

Targeted scans for specific vulnerability classes to reduce false positives.

🧰 Tools & Usage
Vulnerability	Tool
SQL Injection	sqlmap
XSS	dalfox
CVEs & Misconfigs	nuclei
CORS	cors_scan.py
CSRF	xsrfprobe
SSTI	sstimap
📌 Examples
sqlmap -m params.txt --random-agent --batch
dalfox file urls.txt
nuclei -l live_subdomains.txt -t templates/

🧨 Phase 5: Advanced Crawling & Fuzzing

Dig deeper to uncover hidden paths, APIs, and forgotten files.

🧰 Tools Used

Katana – Modern, JS-aware crawler

Gobuster / Dirb – Directory & file brute-forcing

katana -u https://target.com -o katana_urls.txt
gobuster dir -u https://target.com -w wordlist.txt

🛠️ Toolset Summary
Tool	Purpose
Subfinder / Assetfinder	Subdomain Discovery
Httpx	Live Host Probing
Waybackurls / GAU	Historical URLs
ParamSpider	Parameter Mining
Nuclei	Template-based Scanning
Sqlmap	SQL Injection
Dalfox	XSS Detection
Katana	Advanced Crawling
📜 Pro Tips (Real Bug Bounty Mindset)

🧹 Clean Your Data
Always remove duplicates:

sort -u urls.txt -o urls.txt


🎯 Attack with Precision
Focus only on valid endpoints:

httpx -mc 200


⚡ Speed Matters
Chain tools using pipes for faster recon:

cat subdomains.txt | httpx | nuclei

⚠️ Legal Disclaimer

This toolkit is intended strictly for educational purposes and authorized Bug Bounty programs only.
❌ Unauthorized scanning or testing of systems without permission is illegal and unethical.
