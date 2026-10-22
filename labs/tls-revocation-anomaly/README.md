# TLS Certificate Revocation Anomaly Detection Under Adversarial Network Conditions

## Project Metadata

* **Course:** Graduate Network Security
* **Milestone:** Milestone 1 - Topic Selection Proposal
* **Project Title:** TLS Certificate Revocation Anomaly Detection Under Adversarial Network Conditions
* **Topic Category:** TLS Certificate Anomaly Detection
* **Author / Student ID:** [Begüm Kunaç / 2834638]
* **Course Repository:** https://github.com/cengwins/Labtainers
* **Proposed Branch:** project/2834638-tls-revocation-anomaly
* **Planned Lab Path:** labs/tls-revocation-anomaly/

---

## Summary

This laboratory environment investigates TLS certificate revocation mechanisms under adverse network conditions and deliberate adversarial interference. When primary revocation services like Online Certificate Status Protocol (OCSP) responders become unreachable, clients are forced to choose between permissive soft-fail policies that risk accepting revoked certificates or strict hard-fail policies that cause service unavailability. 

This project implements an anomaly detection engine alongside a custom client validation engine within the Labtainers framework. The goal is to evaluate a validated OCSP-CRL fallback mechanism that maintains high availability for legitimate HTTPS traffic while detecting and preventing the acceptance of revoked certificates during network degradation, delays, or active blocking.

---

## Laboratory Topology

The lab operates using six isolated Docker containers connected across two virtual subnets:

* **tls-client:** Executes HTTPS requests and enforces soft-fail, hard-fail, or OCSP-CRL fallback verification policies.
* **net-gateway:** Routes traffic between subnets and simulates adverse network conditions (latency, packet loss, and selective blocking via tc netem and iptables).
* **https-server:** Serves legitimate HTTPS content and provides a switchable rogue mode presenting a revoked certificate.
* **ocsp-server:** Provides signed OCSP status responses for issued certificates.
* **crl-server:** Hosts signed Certificate Revocation Lists with controllable update delays.
* **revocation-ids:** Processes structured execution logs to correlate status check failures, serial numbers, and client decisions to generate security alerts.

Network layout: `client_net` (172.20.10.0/24) and `service_net` (172.20.20.0/24) connected through `net-gateway`.

---

## Commit Message Standards

This project follows the Conventional Commits standard. Commit messages must follow the format:

`<type>(<scope>): <short summary>`

### Reference Table

| Type | Description | Example Scopes | Example Commit Message |
| --- | --- | --- | --- |
| feat | A new feature or rule implementation | checker, ids, policy | feat(checker): implement OCSP-CRL fallback verification rule |
| fix | A bug fix in scripts or container configuration | gateway, ids, parser | fix(ids): resolve timestamp parsing error for stale CRL logs |
| docs | Documentation updates or lab instructions | readme, lab-docs | docs(readme): update network topology and parameter lists |
| style | Formatting changes that do not affect code execution | checker, runner | style(runner): format experiment scripts according to PEP8 |
| refactor | Code refactoring without changing functionality | ids, crypto | refactor(crypto): extract CRL signature validation to helper function |
| test | Adding or updating unit tests or assessment checks | assessment, ids | test(assessment): add automated check for soft-fail exploitation |
| chore | Maintenance, updates to Dockerfiles, or dependencies | docker, deps | chore(docker): update python cryptography package in client image |
| perf | Performance improvements or speed optimizations | checker, cache | perf(cache): optimize local CRL lookup in revocation checker |
| ci | Continuous integration or Labtainer build script edits | build, labtainer | ci(labtainer): add parameterization validation step to build pipeline |

---