# SACS Oreo
# Executive Summary

SACS Oreo is a Python-based command-line application developed by SecureAfrica Cyber Solutions (SACS) to support authorized web application security assessments. The project was created to provide a lightweight, transparent, and extensible security assessment framework that emphasizes evidence quality, reproducibility, and responsible testing.

Unlike traditional vulnerability scanners that prioritize broad vulnerability coverage, Oreo was designed around a different philosophy: producing findings that are understandable, verifiable, and useful to both technical practitioners and decision-makers. Every identified issue includes structured evidence, confidence indicators, reproducibility information, remediation guidance, and business impact explanations tailored to organizations operating in Nigeria and broader African environments.

The current implementation represents the first Minimum Viable Product (MVP) of the platform. It performs safe reconnaissance, crawls authorized web applications, executes non-destructive security checks, and generates structured HTML and JSON reports suitable for technical review.

The project also serves as the architectural foundation for future development into a more comprehensive web application security assessment platform capable of supporting modular testing, evidence preservation, and advanced reporting workflows.

# The Problem

Many vulnerability scanners generate extensive lists of findings but provide limited context regarding the reliability, reproducibility, or operational significance of those results. This often leaves security practitioners spending considerable time validating false positives, correlating evidence, and translating technical findings into language that organizations can understand.

For smaller organizations, educational institutions, startups, and businesses across Africa, existing enterprise security assessment platforms may also be financially inaccessible or unnecessarily complex for routine security evaluations.

The objective behind Oreo was not to replace mature commercial security tools. Instead, the goal was to develop an investigator-oriented assessment framework that prioritizes transparency, evidence quality, and actionable reporting while remaining lightweight and extensible.

# Objectives

The project was developed with several primary objectives:

* Provide a safe framework for authorized web application security assessments.
* Produce structured findings supported by verifiable evidence.
* Reduce false positives through confidence and reproducibility indicators.
* Generate reports that are understandable to both technical and non-technical stakeholders.
* Support secure software development and security review processes for organizations with limited security resources.
* Establish an extensible architecture capable of supporting future security assessment modules.

# Solution Overview

SACS Oreo was designed as a lightweight, authorization-gated web application security assessment framework that combines automated reconnaissance, safe security validation, and structured reporting within a single command-line interface.

The assessment workflow begins with a user-supplied target URL and an explicit acknowledgement that the operator has authorization to assess the target. This authorization gate is a deliberate design decision intended to reinforce responsible and ethical security testing.

Once authorized, Oreo performs controlled crawling of the target application, collecting pages, forms, response headers, cookies, HTTP status codes, content types, and basic technology indicators. These observations form the evidence base used by subsequent security checks.

The current MVP focuses exclusively on non-destructive security assessments. Checks are intentionally designed to avoid modifying application data, bypassing authentication mechanisms, overwhelming target systems, or exploiting discovered vulnerabilities. Instead, the framework identifies indicators of common security weaknesses through safe validation techniques.

Identified findings are normalized into a structured data model containing severity, confidence, reproducibility, evidence, remediation guidance, business impact, and applicable OWASP Top 10 references. Reports are then generated in both JSON and HTML formats to support technical review, documentation, and future automation.

This architecture establishes a foundation that can be extended with additional assessment modules while maintaining consistency in reporting, evidence collection, and finding interpretation.

# System Architecture

The current Oreo MVP follows a modular pipeline architecture in which each component performs a clearly defined responsibility within the assessment process.

Assessment workflow:

User Input
        │
        ▼
Authorization Confirmation
        │
        ▼
Target Validation
        │
        ▼
Crawler
        │
        ▼
Evidence Collection
        │
        ▼
Security Checks
        │
        ▼
Finding Normalization
        │
        ▼
Report Generation
        │
        ▼
HTML / JSON Reports

Core Features

Although currently implemented as a Minimum Viable Product, Oreo incorporates several features intended to support professional security assessment workflows.

## Authorization-Gated Assessments

Every assessment requires explicit confirmation that the operator has authorization to test the target environment. This reinforces responsible security testing practices and clearly separates legitimate assessment activities from unauthorized scanning.

## Safe Assessment Modes

Oreo currently supports multiple operational modes that determine the level of interaction performed during an assessment.

Passive mode focuses exclusively on observation and analysis of responses obtained during crawling.

Safe mode supplements passive analysis with carefully controlled validation requests that do not modify application state.

Active mode has been reserved for future expansion while remaining constrained to non-destructive behavior in the current implementation.

## Structured Finding Model

Rather than producing simple vulnerability lists, Oreo generates structured findings that include:

- Severity
- Confidence
- Reproducibility
- Supporting evidence
- Business impact
- Recommended remediation
- Applicable OWASP references

This model improves the usefulness and interpretability of assessment results.

## Evidence-Oriented Reporting

Each finding is supported by evidence gathered during assessment, allowing reviewers to understand how conclusions were reached and facilitating manual validation where necessary.

## Multiple Report Formats

Assessment results are generated as both HTML and JSON outputs.

HTML reports provide a human-readable summary suitable for reviewers, while JSON reports support future integrations with dashboards, automation pipelines, and other tooling.

## Business-Oriented Risk Communication

In addition to technical descriptions, findings include business impact statements written for decision-makers rather than exclusively for security engineers. This approach helps bridge the communication gap between technical assessments and organizational risk management.

## Extensible Architecture

The modular design allows new assessment modules, reporting formats, and evidence collection capabilities to be incorporated without requiring fundamental architectural changes.

