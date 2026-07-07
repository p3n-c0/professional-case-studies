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


 # Engineering Decisions

The development of SACS Oreo was guided by a number of engineering decisions intended to maximize reliability, transparency, extensibility, and responsible use. Rather than optimizing solely for the number of detectable vulnerabilities, the project prioritizes trustworthy findings, reproducible assessments, and maintainable software architecture.

## Authorization Before Assessment

One of the earliest architectural decisions was to require explicit operator confirmation that the target system is authorized for testing before an assessment begins.

Many security tools can be executed with minimal safeguards, creating opportunities for accidental misuse. Oreo intentionally introduces an authorization gate to reinforce ethical security practices and remind operators that the framework is designed exclusively for legitimate security assessments.

Although this mechanism cannot technically verify authorization, it establishes responsible operational expectations and aligns with the project's emphasis on ethical security engineering.

---

## Modular Assessment Architecture

Instead of implementing all functionality within a single scanning routine, Oreo separates major responsibilities into distinct components.

These include:

- Target validation
- Crawling
- Evidence collection
- Security checks
- Finding normalization
- Report generation

This modular architecture offers several advantages:

- easier maintenance
- improved testing
- simplified debugging
- future feature expansion
- independent enhancement of assessment modules

As the platform grows, new security checks can be introduced without requiring significant changes to existing components.

---

## Safe-by-Default Assessment Philosophy

A deliberate decision was made to avoid destructive testing techniques during the MVP stage.

The framework currently performs only non-destructive assessments designed to identify indicators of security weaknesses without modifying application state or affecting service availability.

Examples include:

- HTTP header analysis
- cookie inspection
- response analysis
- harmless validation requests
- exposure checks

Capabilities such as authentication bypass, exploit chaining, denial-of-service testing, brute-force attacks, or payload execution are intentionally excluded.

This design reflects the project's objective of supporting routine security reviews while minimizing operational risk.

---

## Structured Evidence Model

Each finding generated by Oreo is supported by evidence collected during the assessment process.

Rather than reporting only that a vulnerability exists, findings include observable artifacts that explain how the conclusion was reached.

This approach provides several benefits:

- improved transparency
- easier manual verification
- reduced false positives
- stronger technical documentation
- greater confidence during report review

The evidence-oriented design also prepares the framework for future preservation of HTTP request and response artifacts.

---

## Confidence and Reproducibility

Security assessment results are not equally reliable.

For this reason, every finding includes confidence and reproducibility indicators.

Confidence reflects how strongly the available evidence supports the conclusion.

Reproducibility indicates whether the observed condition can be consistently demonstrated.

Separating these concepts provides reviewers with additional context when prioritizing findings and planning manual verification.

---

## Standardized Finding Schema

All findings are normalized into a consistent structure regardless of the originating assessment module.

Each finding contains:

- identifier
- title
- severity
- category
- confidence
- reproducibility
- affected resource
- supporting evidence
- business impact
- remediation guidance
- OWASP mapping
- references

Maintaining a consistent schema simplifies report generation while supporting future integrations with dashboards, APIs, and security management platforms.

---

## Business-Oriented Reporting

Traditional vulnerability scanners often assume that reports will be consumed exclusively by security engineers.

Oreo adopts a different approach by including business impact explanations alongside technical findings.

These descriptions explain how identified weaknesses may affect organizations in practical terms, including customer trust, operational continuity, regulatory exposure, and organizational risk.

Special consideration is given to organizations operating within Nigerian and broader African business environments, where cybersecurity maturity and available security resources can vary significantly.

---

## Human-Readable Reports

While JSON outputs provide structured machine-readable data, HTML reports were designed to support investigators, consultants, developers, and business stakeholders who require accessible documentation.

The objective is to reduce the effort required to communicate technical assessment results across multidisciplinary teams.

---

## Extensibility

The project was intentionally designed with future expansion in mind.

Planned capabilities include:

- plugin-based assessment modules
- authenticated assessments
- API testing
- preserved HTTP evidence
- additional reporting formats
- dashboard integration
- continuous assessment workflows

The current architecture minimizes the amount of redesign required to incorporate these capabilities in future releases.

---

## Maintainability

Code organization was prioritized throughout development.

Responsibilities are separated across dedicated modules to improve readability and facilitate long-term maintenance.

Unit testing accompanies core functionality to reduce regression risk as new assessment capabilities are introduced.

# Validation & Testing

The current MVP was validated to confirm that core assessment workflows operate reliably across supported scan modes while producing consistent and structured outputs.

Testing focused on correctness of functionality rather than vulnerability coverage, reflecting the project's objective of establishing a stable assessment foundation before expanding the range of supported security checks.

## Validation Objectives

Testing was performed to verify:

- target validation
- URL normalization
- crawler behaviour
- page discovery
- response handling
- finding generation
- report generation
- JSON serialization
- HTML report rendering
- command-line behaviour

## Unit Testing

Unit tests were implemented for core framework components, including:

- URL utilities
- crawler functionality
- security checks
- reporting components

Testing each component independently helps ensure that future enhancements do not unintentionally affect existing functionality.

## Report Validation

Generated HTML and JSON reports were manually reviewed to confirm:

- consistent finding structure
- correct severity assignment
- accurate evidence presentation
- valid JSON formatting
- readable HTML layout

## Scan Validation

Representative assessments were conducted against authorized test targets to confirm:

- successful crawling
- controlled request behaviour
- proper discovery of pages and resources
- execution of implemented security checks
- generation of structured findings

## Safety Validation

Particular attention was given to verifying that current assessment modes remain non-destructive.

Validation confirmed that implemented checks do not intentionally modify application data, perform authentication attacks, execute exploits, or introduce denial-of-service behaviour.

This aligns with the project's safe-by-default assessment philosophy.

## Continuous Improvement

Validation will continue as new assessment modules are introduced.

Future releases will expand automated testing coverage while incorporating additional validation datasets and representative application environments.

# Results & Impact

Although SACS Oreo is currently in its first Minimum Viable Product (MVP) stage, the project successfully demonstrates the viability of a lightweight, evidence-oriented web application security assessment framework.

The current implementation provides a complete assessment workflow, beginning with authorized target validation and progressing through controlled crawling, security analysis, finding normalization, and structured report generation.

Rather than focusing solely on identifying vulnerabilities, Oreo emphasizes producing findings that are understandable, reproducible, and actionable. The inclusion of confidence ratings, reproducibility indicators, evidence summaries, remediation guidance, and business impact explanations provides reviewers with significantly more context than traditional scanner outputs.

The project has also established a reusable architectural foundation for future development. New assessment modules, reporting capabilities, and evidence preservation mechanisms can be incorporated without fundamental redesign of the existing framework.

Beyond its immediate functionality, Oreo serves as an important demonstration of secure software engineering, responsible vulnerability assessment practices, and practical security tooling development.

Current project outcomes include:

- Safe authorization-gated assessment workflow
- Modular scanning architecture
- Structured evidence collection
- Standardized finding schema
- HTML and JSON reporting
- OWASP Top 10 mapping
- Business-oriented risk communication
- Unit-tested core components
- Extensible project architecture

While the current feature set remains intentionally conservative, the project provides a strong platform for iterative enhancement into a more comprehensive security assessment solution.

# Lessons Learned

Developing Oreo provided valuable experience in balancing technical capability with responsible security engineering.

One of the most significant lessons was that producing trustworthy findings is often more valuable than producing a larger number of findings. Security practitioners ultimately spend considerable time validating automated scanner results, making transparency and evidence quality essential design considerations.

The project also reinforced the importance of modular software architecture. Separating crawling, evidence collection, assessment logic, and reporting simplifies maintenance while making future enhancements significantly easier to implement.

Another important lesson involved communicating security findings to different audiences. Security reports are frequently consumed not only by engineers but also by project managers, executives, consultants, and business owners. Incorporating business-oriented impact descriptions helps bridge this communication gap and improves the practical usefulness of assessment reports.

Finally, developing Oreo strengthened my understanding of responsible security testing. Effective security tools must balance thoroughness with operational safety, ensuring that assessments support defensive objectives without introducing unnecessary risk to target environments.

These lessons will continue to guide the project's future development.

# Future Roadmap

SACS Oreo has been designed as an extensible platform intended to evolve beyond its current MVP implementation.

Planned development areas include:

## Assessment Capabilities

- Expanded OWASP Top 10 coverage
- Additional security header analysis
- Authentication-aware assessments
- API security testing
- GraphQL assessment support
- File upload security checks
- Session management analysis
- Business logic testing modules

## Evidence Collection

- HTTP request preservation
- HTTP response preservation
- Screenshot capture
- Response diffing
- Evidence packaging for reporting

## Reporting

- Interactive HTML dashboards
- PDF report generation
- Executive summaries
- Risk prioritization
- Compliance mappings
- SARIF export
- CVSS scoring support

## Framework Enhancements

- Plugin architecture
- Parallel scanning
- Improved technology fingerprinting
- Configuration profiles
- Custom rule support
- API integrations

## Workflow Integration

- CI/CD integration
- Scheduled assessments
- REST API
- Team collaboration
- Finding history
- Scan comparison

Long-term development aims to establish Oreo as a practical security assessment platform that complements professional penetration testing workflows while maintaining its emphasis on transparency, evidence quality, and responsible security assessment.

# Technologies Used

## Programming Language

- Python

## Core Technologies

- Requests
- BeautifulSoup
- HTML Parsing
- JSON
- Regular Expressions

## Security Concepts

- HTTP Security Headers
- Cookie Security
- Cross-Origin Resource Sharing (CORS)
- OWASP Top 10
- Secure Configuration Review
- Web Application Reconnaissance

## Development Tools

- Git
- GitHub
- unittest
- Markdown

## Reporting

- HTML
- JSON

## Engineering Principles

- Modular Architecture
- Evidence-Oriented Design
- Responsible Security Assessment
- Structured Reporting
- Defensive Programming
- Unit Testing

# Closing Reflection

SACS Oreo represents an important milestone in my progression as a cybersecurity engineer.

While my professional experience has primarily focused on digital forensics and cybercrime investigations, developing Oreo provided an opportunity to deepen my understanding of offensive security engineering and secure software assessment. The project challenged me to think beyond vulnerability detection and instead focus on designing a framework that produces transparent, reproducible, and meaningful security findings.

Throughout development, I intentionally prioritized responsible assessment practices, maintainable architecture, and evidence quality over feature quantity. This reflects my broader engineering philosophy: security tools should help practitioners make better decisions rather than simply generate larger volumes of data.

The experience also reinforced the close relationship between offensive and defensive security. Understanding how web applications are assessed enables stronger defensive strategies, more informed investigations, and better communication between security engineers, developers, and organizational stakeholders.

As Oreo continues to evolve, my objective is not simply to build another vulnerability scanner, but to develop a practical assessment framework that combines sound engineering, responsible security practices, and high-quality reporting. Together with SACS WEP, CyberSafe, and Audex, the project forms part of a broader vision to create technologies that strengthen cybersecurity capabilities across Africa while supporting investigators, defenders, and security professionals in their work.
