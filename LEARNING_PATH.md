# LEARNING_PATH

> A structured DevOps learning path designed for the team.
>
> This document explains **what to learn, why it matters, prerequisites, and expected outcomes**.
>
> The roadmap answers:
>
> > "What should we accomplish next?"
>
> This document answers:
>
> > "What knowledge and skills do we need to get there?"

## Workflow

1. Learn the fundamentals.
2. Write documentation.
3. Perform hands-on labs.
4. Build something practical.
5. Review each other's work.
6. Add improvements to the repository.

---

## Level 0 — Engineering Foundations

### Goal

Build the habits required for professional engineering work.

### Learn

- Git workflow
- Documentation
- Debugging methodology
- Reading documentation
- Problem decomposition
- Basic system thinking

### Practice

- Write clear README files
- Create issues
- Use branches
- Submit pull requests
- Review teammate changes

### Outcome

You can collaborate on software projects professionally.

---

## Level 1 — Linux Administration

### Prerequisites

None.

### Learn

#### System Fundamentals

- Linux filesystem hierarchy
- Processes
- Threads
- Services
- systemd
- Package management
- Environment variables

#### Users & Permissions

- Users
- Groups
- Ownership
- chmod
- chown
- sudo
- ACLs

#### Storage

- Partitions
- Filesystems
- Mounting
- Disk usage
- Volumes

#### Administration

- SSH
- Logs
- Journaling
- System troubleshooting

### Practice

Build:

- Linux server setup guide
- User management scripts
- Server troubleshooting checklist

### Outcome

You can operate and troubleshoot Linux servers.

---

## Level 2 — Networking Fundamentals

### Prerequisites

Linux basics.

### Learn

#### Network Fundamentals

- OSI model
- TCP/IP
- IP addressing
- Subnetting
- Ports
- Protocols

#### Core Services

- DNS
- DHCP
- HTTP/HTTPS
- SSH
- FTP/SFTP

#### Troubleshooting

- ping
- traceroute
- netstat
- ss
- tcpdump
- dig
- curl

#### Security

- Firewalls
- Network segmentation
- TLS certificates

### Practice

Build:

- Network troubleshooting handbook
- Local service monitoring scripts

### Outcome

You understand how machines communicate.

---

## Level 3 — Git & Collaboration

### Prerequisites

Basic command line.

### Learn

- Repository structure
- Commits
- Branches
- Merging
- Rebasing
- Tags
- Releases
- Pull Requests
- Code reviews

### Practice

Team workflow:

```
Issue => Branch => Commit => Pull Request => Review => Merge

```

### Outcome

You can work effectively in engineering teams.

---

## Level 4 — Bash Automation

### Prerequisites

Linux fundamentals.

### Learn

- Shell environment
- Variables
- Conditions
- Loops
- Functions
- Pipes
- Redirects
- Text processing
- Error handling

Tools:

- grep
- sed
- awk
- jq
- xargs

### Practice

Build:

- System audit scripts
- Backup scripts
- Deployment helpers
- Server health checks

### Outcome

You can automate repetitive operations.

---

## Level 5 — Docker & Containers

### Prerequisites

Linux + networking.

### Learn

#### Container Concepts

- Images
- Containers
- Registries
- Layers
- Volumes
- Networks

#### Docker Usage

- Dockerfile
- docker compose
- Container lifecycle
- Image optimization

#### Internals

- Namespaces
- cgroups
- Overlay filesystem

### Practice

Build:

- Multi-container applications
- Development environments
- Local infrastructure stacks

### Outcome

You understand modern application packaging.

---

## Level 6 — Web Infrastructure

### Prerequisites

Networking + Docker.

### Learn

#### Reverse Proxy

- Nginx
- HAProxy
- Traefik

#### Concepts

- HTTP routing
- Load balancing
- SSL termination
- Virtual hosts

### Practice

Deploy:

```

Internet
|
Reverse Proxy
|
Application Containers
|
Database

```

### Outcome

You can expose and route applications.

---

## Level 7 — Automation & Configuration Management

### Prerequisites

Linux administration.

### Learn

### Ansible

- Inventory
- Playbooks
- Roles
- Variables
- Templates
- Handlers

### Python

- Automation scripts
- APIs
- CLI tools
- Data processing

### Practice

Build:

- Server provisioning scripts
- Automated configuration systems

### Outcome

You can manage multiple systems consistently.

---

## Level 8 — Observability

### Prerequisites

Linux + Docker.

### Learn

#### Monitoring

- Metrics
- Logs
- Alerts
- Dashboards

#### Tools

- Prometheus
- Grafana

#### Concepts

- Time-series data
- Service health
- SLI
- SLO
- SLA

### Practice

Build:

- Application dashboard
- Server monitoring stack

### Outcome

You can understand system behavior.

---

## Level 9 — Kubernetes

### Prerequisites

Docker + Networking.

### Learn

#### Core Concepts

- Cluster architecture
- Nodes
- Pods
- Services
- Deployments
- ConfigMaps
- Secrets

#### Operations

- Scaling
- Rolling updates
- Networking
- Storage
- Troubleshooting

### Practice

Deploy:

- Applications
- Databases
- Monitoring stacks

### Outcome

You understand container orchestration.

---

## Level 10 — CI/CD & GitOps

### Prerequisites

Git + Docker + Kubernetes.

### Learn

#### CI/CD Concepts

- Build pipelines
- Testing
- Artifact management
- Deployment automation

#### Tools

- GitHub Actions
- Jenkins

#### GitOps

- Infrastructure as code workflow
- Automated deployments
- Configuration versioning

### Practice

Build:

```

Code Push
|
CI Pipeline
|
Build Image
|
Deploy
|
Monitor

```

### Outcome

You can automate software delivery.

---

## Level 11 — Infrastructure as Code

### Prerequisites

Cloud fundamentals.

### Learn

#### Terraform

- Providers
- Resources
- State
- Modules
- Variables
- Outputs

### Practice

Build:

- Reproducible infrastructure
- Cloud environments

### Outcome

You can manage infrastructure programmatically.

---

## Level 12 — Databases & Backend Fundamentals

### Prerequisites

Basic application knowledge.

### Learn

#### Databases

- SQL fundamentals
- PostgreSQL
- Redis
- Indexing
- Backups
- Replication

#### Architecture

- Monoliths
- Modular monoliths
- Microservices
- Event-driven systems
- APIs

### Practice

Deploy:

- Application stack
- Database
- Cache
- Monitoring

### Outcome

You understand the systems DevOps engineers operate.

---

## Level 13 — Security

### Prerequisites

Linux + Networking.

### Learn

- Secure Linux configuration
- Authentication
- Authorization
- Secrets management
- Container security
- Network security
- Vulnerability management

### Practice

Perform:

- Security audits
- Hardening exercises

### Outcome

You can operate systems responsibly.

---

## Level 14 — Cloud & Platform Engineering

### Prerequisites

Infrastructure fundamentals.

### Learn

#### Cloud Concepts

- Compute
- Storage
- Networking
- IAM
- Load balancing

#### Providers

- AWS
- Azure
- Google Cloud

#### Advanced

- Platform engineering
- SRE concepts
- Reliability engineering

### Outcome

You understand production-scale infrastructure.

---

## Continuous Improvement

Every member should continuously improve:

- Documentation quality
- Automation
- Troubleshooting skills
- Communication
- System design thinking
- Open-source contribution

---

## Final Goal

By completing this path, the team should be able to:

- Operate Linux servers.
- Automate infrastructure.
- Build CI/CD pipelines.
- Deploy containerized applications.
- Manage Kubernetes workloads.
- Monitor production systems.
- Understand cloud infrastructure.
- Contribute professionally to DevOps teams.
