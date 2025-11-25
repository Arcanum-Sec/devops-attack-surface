# 🎯 DevOps Attack Surface Guide

An interactive, single-page reference for penetration testers targeting DevOps infrastructure. Built by [Arcanum Security](https://github.com/Arcanum-Sec).

**🌐 Live Site:** [arcanum-sec.github.io/devops-attack-surface](https://arcanum-sec.github.io/devops-attack-surface/)

> ⚠️ **Work in Progress:** This guide originated from our internal pentest methodology wiki at Arcanum and has been enhanced with AI assistance. We're actively adding tools, CVEs, and attack vectors. PRs welcome!

## 📊 What's Inside

**88+ tools** across **15 categories**, each with:

- 🔌 **Default Ports** — For service discovery and scanning
- 🌐 **Access URLs** — Common URL patterns for SaaS tools (great for recon)
- 🔑 **Default Credentials** — Where applicable
- ⚔️ **Attack Vectors** — With CVE links and exploitation techniques

### Categories

| Category | Tools |
|----------|-------|
| 📚 Knowledge Bases | SharePoint, Confluence, MediaWiki, Notion, Wiki.js, TikiWiki, DokuWiki |
| 📋 Dev & Project Management | Jira, Trello, Redmine |
| 🔀 Source Code Management | Git, GitHub, GitLab, Bitbucket, SVN, Perforce Helix Core |
| 📦 Repository Management | Artifactory, Nexus, AWS CodeArtifact, Cloudsmith |
| 🏗️ Build Servers | Jenkins, TeamCity, Bamboo, CircleCI, GitHub Actions, GitLab CI |
| 🚀 Deployment Platforms | Octopus Deploy, UrbanCode, Codefresh, ArgoCD |
| ⚙️ Configuration Management | Ansible, Chef, Puppet, Salt, CFEngine, PowerShell DSC |
| 📊 Operations & Monitoring | Splunk, Elastic (ELK), Grafana, Graylog, Nagios, StackStorm |
| 🏗️ Infrastructure as Code | Terraform, CloudFormation, ARM Templates, GCP Deployment Manager |
| 🔐 Secrets Managers | HashiCorp Vault, AWS Secrets Manager, Azure Key Vault, CyberArk, Akeyless |
| 🗄️ Databases | PostgreSQL, MySQL, MongoDB, Redis, MSSQL, Oracle, Elasticsearch, Cassandra, CouchDB |
| 🌐 CMS & Web Platforms | WordPress, Drupal, Joomla, Magento, Tomcat, JBoss, WebLogic, phpMyAdmin |
| 🌐 Network Infrastructure | Cisco, Juniper, Fortinet, Palo Alto, Dell iDRAC, HP iLO, VMware ESXi/vCenter, Proxmox |
| 📨 Message Queues | RabbitMQ, Apache ActiveMQ, Kafka, ZooKeeper |

## 🚀 Quick Start

### Option 1: Use the Live Site
Visit **[arcanum-sec.github.io/devops-attack-surface](https://arcanum-sec.github.io/devops-attack-surface/)**

### Option 2: Run Locally
```bash
git clone https://github.com/Arcanum-Sec/devops-attack-surface.git
cd devops-attack-surface
python3 -m http.server 8080
# Open http://localhost:8080
```

## 🔍 Internal Pentest Workflow

The guide includes ready-to-run commands for internal penetration testing:

### 1. Enumerate Internal Ranges
```bash
for range in "10.0.0.0/8" "172.16.0.0/12" "192.168.0.0/16"; do
    echo "$range" | mapcidr -silent >> all_targets.txt
done
```

### 2. Discover DevOps Services
```bash
cat all_targets.txt | httpx -p 80,443,8080,8443,9000,3000,5000,8081,9090,6443,8929,7990,1666,9001,5601,9200,5432,3306,27017,6379,1433,15672,8161,7001,5984,9042 -title -tech-detect -status-code -threads 100 -o live_services.txt
```

### 3. Scan for Vulnerabilities
```bash
nuclei -l live_services.txt -tags devops,cicd,default-login,exposed,panel,jenkins,gitlab,kubernetes,docker,mysql,postgres,mongodb,redis,wordpress,drupal,tomcat,weblogic,activemq,rabbitmq -severity info,low,medium,high,critical -o all_findings.txt
```

## 📖 Features

- 🔍 **Search** — Find tools, ports, or credentials instantly
- 📋 **Copy** — Click any value to copy to clipboard
- 🎯 **Interactive** — Expand/collapse categories and tool details
- 📱 **Responsive** — Works on desktop and mobile
- ⚡ **Fast** — Pure HTML/CSS/JS, no frameworks, works offline

## ⚠️ Disclaimer

This tool is for **authorized security testing only**. Always obtain proper authorization before testing any systems.

**Intended use cases:**
- Authorized penetration testing
- Red team operations
- Security assessments
- CTF competitions
- Security research and education

## 🤝 Credits

- **Arcanum Security** — Internal methodology and curation
- **Original DevOps Class** — Based on work by Tom and Colbert from Accenture (formerly FusionX)
- **AI Enhancement** — Structure, CVE research, and content expansion

## 📝 Contributing

Found something missing? Have a new CVE or attack vector? PRs and issues welcome!

## 📄 License

MIT License — Free to use for educational and authorized security testing purposes.

## 🔗 Resources

- [OWASP Testing Guide](https://owasp.org/www-project-web-security-testing-guide/)
- [CIDER Security - Top 10 CI/CD Security Risks](https://www.cidersecurity.io/top-10-ci-cd-security-risks/)
- [HackTricks](https://book.hacktricks.xyz/)
- [PayloadsAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings)

---

**Maintained by [Arcanum Security](https://github.com/Arcanum-Sec)** | **Last Updated:** November 2025
