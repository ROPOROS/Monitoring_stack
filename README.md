# 📈 Observability & Monitoring – UWAS

> Internship project focused on implementing end-to-end observability for Coral-IO’s UWAS production platform using New Relic, Kubernetes, and Ansible automation.

---

## 🚫 Repository Notice
> ⚠️ Due to confidentiality, the original source code and dashboards are private under Coral-IO’s internal GitLab environment.  
> This repository serves as a **case study** summarizing the project architecture, objectives, and outcomes.

---

## 🧩 Tech Stack
![New Relic](https://img.shields.io/badge/New%20Relic-008C99?logo=newrelic&logoColor=white)
![Ansible](https://img.shields.io/badge/Ansible-EE0000?logo=ansible&logoColor=white)
![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?logo=kubernetes&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?logo=linux&logoColor=black)
![Grafana](https://img.shields.io/badge/Grafana-F46800?logo=grafana&logoColor=white)

---

## 📚 Table of Contents
1. [Overview](#overview)
2. [Objectives](#objectives)
3. [Architecture](#architecture)
4. [Automation](#automation)
5. [Challenges & Achievements](#challenges--achievements)
6. [Author](#author)

---

## Overview
During my internship at **Coral-IO **, I implemented an observability strategy for the **UWAS** web application — a cloud-native production system.

The goal was to enhance monitoring, tracing, and alerting across multiple microservices using **New Relic**, **Ansible**, and **Kubernetes**.

---

## Objectives
- Assess existing monitoring maturity using the **Observability Maturity Model (OMM)**  
- Establish unified **observability pipelines** for infrastructure, applications, and user experience  
- Automate **New Relic agent installation** and configuration via Ansible  
- Integrate **metrics, logs, and distributed tracing**  
- Create custom dashboards and performance KPIs for engineering teams  

---

## Architecture
The implemented observability stack included:

| Layer | Tool | Purpose |
|-------|------|----------|
| Infrastructure | Kubernetes + Linux | Application hosting and orchestration |
| Monitoring | New Relic | Full-stack observability (APM, metrics, logs) |
| Automation | Ansible | Agent provisioning and configuration |
| Visualization | New Relic Dashboards | Metrics and KPI visualization |
| Alerting | New Relic Alerts | SLA and performance-based alert rules |

### 🔧 High-Level Flow
1. Ansible deploys and configures New Relic agents on Kubernetes nodes.  
2. Agents collect application performance data, traces, and logs.  
3. Data is pushed to New Relic’s APM platform.  
4. Dashboards display live metrics, errors, and throughput.  
5. Alerts trigger based on pre-defined thresholds (response time, CPU, memory).

<p align="center">
  <img src="/nr.png" alt="CI/CD Architecture" width="750">
</p>


---

## Automation
All setup was **fully automated using Ansible**, including:
- Installing New Relic infrastructure and APM agents  
- Registering services automatically with New Relic  
- Applying standardized dashboard templates per environment  

Example playbook snippet:
```yaml
- hosts: k8s_nodes
  become: true
  tasks:
    - name: Install New Relic infrastructure agent
      ansible.builtin.shell: |
        curl -Ls https://download.newrelic.com/install/newrelic-cli/scripts/install.sh | bash
    - name: Apply license key configuration
      ansible.builtin.copy:
        content: |
          license_key: "{{ newrelic_license }}"
        dest: /etc/newrelic-infra.yml
