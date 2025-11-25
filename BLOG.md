# Introducing the DevOps Attack Surface Guide: A Pentester's Cheatsheet for Modern Infrastructure

**By Jason Haddix | Arcanum Security**

---

If you've done any internal penetration testing in the last few years, you know the landscape has changed dramatically. Gone are the days when you'd pop a box, grab some hashes, and call it a day. Today's enterprise environments are a sprawling maze of CI/CD pipelines, container orchestration, secrets managers, artifact repositories, and configuration management tools—each one a potential goldmine for attackers.

After years of building out internal methodology documentation at Arcanum, we decided it was time to give back to the community. Today, we're releasing the **DevOps Attack Surface Guide**—an interactive, searchable reference for penetration testers targeting DevOps infrastructure.

## Why This Matters

During internal engagements, my team and I kept running into the same scenario: we'd land on a network and immediately start hunting for Jenkins, GitLab, Vault, Artifactory, and the dozens of other tools that make up modern DevOps stacks. Each one has its own default ports, default credentials, common misconfigurations, and CVEs worth knowing.

We were tired of grepping through scattered notes and bookmarks. We needed a single, consolidated resource that answered questions like:

- "What port does TeamCity run on?"
- "What are the default creds for Nexus?"
- "What's that recent Perforce CVE everyone's talking about?"
- "How do I find exposed Terraform state files?"

So we built one.

## What's Inside

The guide covers **88+ tools** across **15 categories**:

- **Knowledge Bases** — SharePoint, Confluence, MediaWiki, Notion, Wiki.js
- **Source Code Management** — Git, GitHub, GitLab, Bitbucket, Perforce, SVN
- **Repository Management** — Artifactory, Nexus, AWS CodeArtifact
- **Build Servers** — Jenkins, TeamCity, Bamboo, CircleCI, GitHub Actions
- **Deployment Platforms** — Octopus Deploy, Codefresh, ArgoCD
- **Configuration Management** — Ansible, Chef, Puppet, Salt
- **Operations & Monitoring** — Splunk, Elastic Stack, Grafana, Nagios
- **Secrets Managers** — HashiCorp Vault, AWS Secrets Manager, Azure Key Vault, CyberArk
- **Databases** — PostgreSQL, MySQL, MongoDB, Redis, MSSQL, Oracle
- **CMS & Web Platforms** — WordPress, Drupal, Tomcat, WebLogic, JBoss
- **Network Infrastructure** — Cisco, Juniper, Fortinet, Palo Alto, VMware

For each tool, you get:

- **Default ports** for service discovery
- **Access URLs** for SaaS tools (great for recon and Google dorking)
- **Default credentials** where applicable
- **Attack vectors** with links to relevant CVEs and research
- **Common misconfigurations** we've seen in the wild

## Built for Speed

The guide includes ready-to-run commands for your internal pentest workflow:

```bash
# Enumerate internal ranges
for range in "10.0.0.0/8" "172.16.0.0/12" "192.168.0.0/16"; do
    echo "$range" | mapcidr -silent >> targets.txt
done

# Discover DevOps services
cat targets.txt | httpx -p 80,443,8080,8443,9000,3000,8081,9200,5601,8200 \
    -title -tech-detect -status-code -o live_services.txt

# Scan for vulnerabilities and default creds
nuclei -l live_services.txt -tags devops,cicd,default-login,jenkins,gitlab \
    -severity medium,high,critical -o findings.txt
```

## A Living Document

**Fair warning: this is a work in progress.** The guide originated from our internal pentest methodology wiki at Arcanum, and we've been enhancing it with the help of AI to fill gaps, add recent CVEs, and improve the overall structure. We'll continue updating it as new vulnerabilities drop and as we discover new attack patterns during engagements.

If you spot something missing or incorrect, PRs are welcome.

## Try It Out

The guide is live now at: **[arcanum-sec.github.io/devops-attack-surface](https://arcanum-sec.github.io/devops-attack-surface/)**

It's fully client-side, searchable, and works great on mobile for those times you're on-site and need a quick reference.

## What's Next

We're planning to add:

- Container & Kubernetes section (Docker, K8s, Helm, etc.)
- Cloud-specific attack patterns (AWS, Azure, GCP misconfigs)
- More IoT/embedded systems common in enterprise environments
- Integration with Nuclei template recommendations

## Final Thoughts

The DevOps attack surface is only going to keep growing. Every new tool added to the pipeline is another potential entry point. My hope is that this resource helps pentesters work more efficiently and helps defenders understand what attackers are looking for.

Happy hunting.

— **Jason Haddix**
Founder, Arcanum Security
[@jhaddix](https://twitter.com/jhaddix)

---

*The DevOps Attack Surface Guide is open source and available at [github.com/Arcanum-Sec/devops-attack-surface](https://github.com/Arcanum-Sec/devops-attack-surface).*
