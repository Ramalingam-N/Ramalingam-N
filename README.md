<div align="center">

<img src="assets/banner.svg" alt="Ramalingam N, Software Engineer. Backend and Azure integrations." width="100%">

<br>

[![Portfolio](https://img.shields.io/badge/Portfolio-3ECF8E?style=for-the-badge&logo=githubpages&logoColor=0d1117&labelColor=0d1117)](https://ramalingam-n.github.io/portfolio/)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0d1117?style=for-the-badge&logo=linkedin&logoColor=3ECF8E)](https://linkedin.com/in/n-ramalingam)
[![Email](https://img.shields.io/badge/Email-0d1117?style=for-the-badge&logo=gmail&logoColor=3ECF8E)](mailto:ramalingamn4977@gmail.com)
[![LeetCode](https://img.shields.io/badge/LeetCode-0d1117?style=for-the-badge&logo=leetcode&logoColor=3ECF8E)](https://leetcode.com/u/Ramalingam_N/)

**I build event-driven backend systems and make them fail safely.**<br>
Nearly 2 years at Accenture running production Azure integrations (C#, .NET 8). Chennai, India.

<br>

<img src="assets/stats.svg" alt="2 production Azure integrations owned. 47 lost invoices traced to root cause. Zero downtime on an SFTP upgrade across 5 integrations. 720 plus LeetCode problems." width="100%">

</div>

<br>

## About

Since November 2024 I have worked at Accenture on two production event-driven integrations for a grocery-retail client. One delivers customer events to a data lake. The other delivers order documents to SAP S/4HANA. I own implementation, releases and production support, and most of what I know about distributed systems comes from debugging them in production.

Outside work I build a Java and Spring Boot platform to study the same problems in depth: delivery guarantees, deduplication, failure isolation and recovery.

<br>

## Production work

*C# / .NET 8 on Azure, for a grocery-retail client.*

<details open>
<summary><b>Case study: 47 lost invoices</b></summary>
<br>

| | |
|:--|:--|
| **Problem** | 47 invoices went missing in the pipeline. |
| **Cause** | Blob filenames collided when two invoices were written in the same millisecond, so one overwrote the other. |
| **Fix** | Unique per-invoice filenames, plus concurrency limits aligned with what the receiver can handle. |
| **Verified** | Validated with 5,002 files and zero overwrites. |

</details>

<details open>
<summary><b>Case study: SFTP security upgrade with zero downtime</b></summary>
<br>

| | |
|:--|:--|
| **Scope** | Four Function Apps and five integrations. |
| **Approach** | Configurable host-key prioritisation. |
| **Coordination** | I coordinated QA validation with the partner before cutover. |
| **Verified** | Cutover completed with zero downtime. |

</details>

**Also shipped**

- **Per-store assortment delivery.** Replaced a splitter/timer pipeline with a Service Bus-triggered Azure Function. SHA-256 content-hashed blob markers keep retries idempotent, and Polly handles backoff.
- **Alerting as code.** KQL alert rules deployed through ARM across three environments, routed to source-system owners, with knowledge-transfer sessions on the triage workflow.
- **Duplicate-detection tool.** A .NET tool that normalises XML before hashing and flags repeated transaction and handling-unit IDs across Blob Storage during production investigations.
- **Internal blob tooling.** Console tools for date-range counts, cross-container comparison, duplicate detection and Service Bus claim-check message generation.

<br>

## Flagship project: Reliable Webhook Delivery Platform

A personal project in **Java 17 and Spring Boot 3.2**, built to explore what reliable delivery takes when processes crash, endpoints fail and brokers redeliver. Three services: ingestion, dispatcher and admin.

<div align="center">

[![Source](https://img.shields.io/badge/Source-0d1117?style=for-the-badge&logo=github&logoColor=3ECF8E)](https://github.com/Ramalingam-N/webhook-platform)
[![Live](https://img.shields.io/badge/Live_admin_service-3ECF8E?style=for-the-badge&logo=render&logoColor=0d1117&labelColor=0d1117)](https://admin-service-y0wm.onrender.com/)

<img src="assets/architecture.svg" alt="Architecture: producer, ingestion with Redis dedupe, transactional outbox in PostgreSQL, Kafka fast and slow lanes, dispatcher with circuit breakers and inbox claim, dead-letter store, admin replay and an outbox sweeper." width="100%">

</div>

<br>

| Decision | Why |
|:--|:--|
| **Transactional outbox with a sweeper** | The event and its outbox row commit together. An after-commit fast path publishes immediately. A `FOR UPDATE SKIP LOCKED` sweeper recovers anything left unpublished after a restart. |
| **Two layers of deduplication** | Redis rejects duplicates at ingestion. A PostgreSQL inbox claim on unique `(event_id, endpoint_id)` with `ON CONFLICT DO NOTHING` absorbs Kafka redeliveries. |
| **Fast and slow Kafka lanes** | Failing endpoints move to the slow lane with non-blocking backoff, so they cannot hold up healthy ones. Per-endpoint circuit breakers add further isolation. The cost is best-effort ordering instead of strict FIFO. |
| **Queryable dead-letter store** | Failed deliveries can be inspected in PostgreSQL and replayed through the outbox, so replay follows the same safe path as new events. |
| **Secure by default** | HMAC-SHA256 payload signing, API-key authorisation and SSRF validation of resolved IPs. |
| **Layered tests** | Unit, persistence, service, web and end-to-end tests using Testcontainers and WireMock. |

<br>

## Other projects

<table>
<tr>
<td width="33%" valign="top">

**Blog-Zone**<br>
Blogging platform built on a custom Spring Security filter chain with role-based access.<br><br>
<sub>Spring Boot · Spring Security · JPA/Hibernate · MySQL · AJAX</sub>

</td>
<td width="33%" valign="top">

**WeatherSpot**<br>
Weather service that wraps external weather APIs behind a Spring Boot backend.<br><br>
<sub>Spring Boot · Thymeleaf · Docker</sub>

</td>
<td width="33%" valign="top">

**PushNPull**<br>
API testing tool with custom headers, Basic and Bearer auth, and request history.<br><br>
<sub>Node.js · Express · JavaScript</sub>

</td>
</tr>
</table>

<br>

## Stack

**Used in production** (C# / .NET 8 on Azure)

<img src="https://skillicons.dev/icons?i=cs,dotnet,azure,docker,git&theme=dark" alt="C#, .NET, Azure, Docker, Git" height="48">

<sub>Azure Functions · Service Bus · Blob and Table Storage · API Management · Application Insights · ARM · Azure DevOps · OAuth2/JWT · Polly · xUnit · Moq · SQL</sub>

**Projects and training** (Java and Spring Boot)

<img src="https://skillicons.dev/icons?i=java,spring,kafka,postgres,redis,mysql,nodejs,js&theme=dark" alt="Java, Spring, Kafka, PostgreSQL, Redis, MySQL, Node.js, JavaScript" height="48">

<sub>Spring Security · Spring Data JPA · Hibernate · Resilience4j · Testcontainers · WireMock · JUnit 5 · Maven</sub>

**Fundamentals:** data structures and algorithms, operating systems, computer networks, and NASM x86 assembly.

<br>

## Background

- **Accenture**, Software Engineer (since Nov 2024). Completed the three-month Cloud-Native Microservices residency covering Java, Spring Boot and Docker.
- **Education:** B.E. Computer Science, SNS College of Engineering, 2024.
- **Problem solving:** 720+ LeetCode problems in Java and SQL.
- **Mentoring:** one of three senior mentors in a college coding bootcamp, teaching Java, OOP and DSA.

<br>

<div align="center">

**Open to backend and SDE roles at product companies.**

[![Email](https://img.shields.io/badge/ramalingamn4977@gmail.com-3ECF8E?style=for-the-badge&logo=gmail&logoColor=0d1117&labelColor=0d1117)](mailto:ramalingamn4977@gmail.com)
[![LinkedIn](https://img.shields.io/badge/n--ramalingam-0d1117?style=for-the-badge&logo=linkedin&logoColor=3ECF8E)](https://linkedin.com/in/n-ramalingam)

</div>
