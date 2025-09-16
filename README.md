# 🐘 CloudNativePG Cluster

---
<p align="left">
  <img src="https://img.shields.io/badge/PostgreSQL-16.3-336791?style=flat-square&logo=postgresql&logoColor=white" alt="postgresql">
  <img src="https://img.shields.io/badge/CNPG-Latest-4285F4?style=flat-square&logo=kubernetes&logoColor=white" alt="cnpg">
  <img src="https://img.shields.io/badge/OpenBao-2.4.0-FF6B35?style=flat-square&logo=vault&logoColor=white" alt="openbao">
  <img src="https://img.shields.io/badge/RustFS-S3--Compatible-000000?style=flat-square&logo=rust&logoColor=white" alt="rustfs">
</p>

<em>Production-ready PostgreSQL cluster on Kubernetes with **CloudNativePG**, **OpenBao** secrets, **RustFS** backups, and **Pigsty** monitoring.</em>

---

## 🛠️ Stack

* **[CloudNativePG](https://cloudnative-pg.io/):** 3-node PostgreSQL 16.3 cluster with pgbouncer pooling
* **[OpenBao](https://openbao.org/):** Vault-compatible secrets with External Secrets Operator
* **[RustFS](https://github.com/rustfs/rustfs):** S3-compatible backup storage with Barman Cloud
* **[Pigsty](https://github.com/Vonng/pigsty):** PostgreSQL monitoring with VictoriaMetrics integration

---

## 📖 Complete Guide

**[📝 Supercharge Postgres on K8s: A CNPG + PostgreSQL + Pigsty + Observability Guide](https://medium.com/aws-in-plain-english/supercharge-postgres-on-k8s-a-cnpg-postgresql-pigsty-observability-guide-e6e0fa9b330d)**

---

## 📁 Structure

```
├── cnpg/                     # PostgreSQL cluster & backups
├── external-secret-operator/ # Secret management
├── openbao/                  # Vault setup
├── pigsty-exporter/          # Monitoring
└── rustfs/                   # S3 storage
```
