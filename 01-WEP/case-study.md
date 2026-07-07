---
Project: SACS WEP (SecureAfrica WhatsApp Evidence Processor)
Category: Digital Forensics • Mobile Device Forensics • SQLite Analysis
Status: Active Development
Role: Sole Designer, Architect, Developer, Tester, Technical Writer and Maintainer
Duration: 2025 – Present
Repository: https://github.com/p3n-c0/sacs-wep
Primary Technologies: Python, SQLite, HTML, CSV
Domain: Digital Forensics / Cybercrime Investigations
Last Updated: July 2026
---

# Case Study 01
# SACS WEP
## Building an Investigator-Focused WhatsApp Forensic Processing Utility

---

# Executive Summary

SACS WEP (SecureAfrica WhatsApp Evidence Processor) is a lightweight forensic support utility developed to automate the post-acquisition processing of extracted iOS WhatsApp databases. The project was born from practical experience supporting cybercrime investigations and legal forensic examinations, where repetitive manual analysis of WhatsApp SQLite databases often consumed significant investigative time.

Rather than attempting to replace commercial forensic suites, WEP was designed to complement them. It focuses on transforming extracted `ChatStorage.sqlite` databases into structured, investigator-friendly outputs such as CSV exports, HTML timeline reports, participant summaries, and integrity documentation while preserving evidence-safe workflows and examiner oversight.

The project reflects my broader philosophy that effective forensic software should reduce repetitive analytical work without replacing the professional judgement of the examiner. Throughout its development, particular emphasis has been placed on evidence integrity, transparency, repeatability, and practical usefulness within real investigative environments.

Today, WEP forms part of the growing ecosystem of investigator-focused technologies being developed under SecureAfrica Cyber Solutions (SACS).

---

# Background

My interest in digital forensics has always been closely tied to cybercrime investigations rather than traditional incident response alone. Over the past several years, I have supported criminal investigations involving suspected fraud, participated in forensic examinations supporting legal proceedings, and trained aspiring digital forensic practitioners.

A recurring observation during these engagements was that acquiring digital evidence represented only the beginning of the investigative process. Once an extraction had been completed, investigators still faced the labour-intensive task of manually examining application databases, reconstructing communications, correlating timestamps, identifying participants, organising evidence, and preparing findings suitable for investigative or legal review.

Among the applications encountered most frequently was WhatsApp. Modern WhatsApp databases contain thousands or tens of thousands of records distributed across multiple related SQLite tables. While commercial forensic suites provide extensive acquisition and examination capabilities, investigators often require additional flexibility when performing targeted reviews, custom analysis, or validation of extracted artefacts.

These experiences highlighted an opportunity to build a lightweight utility that could automate repetitive post-acquisition tasks while preserving transparency and allowing investigators to remain in full control of interpretation.

That idea ultimately became SACS WEP.

---

# Problem Statement

Digital forensic investigations frequently involve extensive manual interaction with WhatsApp SQLite databases following forensic acquisition. Investigators may need to reconstruct communication timelines, identify participants, correlate media references, classify message types, and organise evidence into formats suitable for review or reporting.

Although commercial forensic platforms perform many of these functions, investigators often require lightweight, transparent utilities that support repeatable workflows, customised analysis, and independent validation without modifying original evidence.

The absence of such tooling increases analytical effort, introduces opportunities for inconsistency, and slows investigative workflows.

SACS WEP was developed to address these challenges by automating common post-acquisition processing tasks while preserving evidential integrity and maintaining examiner oversight.

---

# Objectives

The primary objectives established at the beginning of the project were:

- Automate repetitive WhatsApp evidence processing tasks.
- Preserve evidence integrity through working-copy analysis.
- Produce structured investigator-friendly outputs.
- Improve communication timeline reconstruction.
- Support repeatable forensic workflows.
- Maintain transparency throughout processing.
- Complement rather than replace commercial forensic software.
- Reduce the amount of manual SQLite querying required during investigations.
- Provide a foundation for future investigator-focused forensic utilities.

---

# My Role

I independently conceived, designed, implemented, validated, documented, and continue to maintain SACS WEP.

Responsibilities included:

- Identifying the investigative problem.
- Defining project objectives.
- Designing the overall system architecture.
- Implementing the processing engine in Python.
- Developing evidence-safe workflows.
- Designing reporting formats.
- Creating HTML timeline reports.
- Implementing hashing and integrity verification.
- Performing validation against real forensic datasets.
- Writing technical documentation.
- Managing versioning and releases.
- Planning future development.

The project represents an integration of practical investigative experience with software engineering to produce a tool intended for real forensic workflows.

# Design Philosophy

From the outset, SACS WEP was never intended to compete with comprehensive commercial forensic platforms. Instead, it was designed to address a specific stage of the digital forensic workflow: the period immediately after forensic acquisition, where investigators must manually transform raw application data into information that can be reviewed, interpreted, and correlated with other evidence.

Several design principles guided every technical decision throughout the project.

## Preserve Evidence Integrity

The integrity of digital evidence is fundamental to any forensic examination. Consequently, WEP was designed around the principle that original evidence should never be modified during analysis.

Rather than interacting directly with the original database, the tool creates and processes a dedicated working copy. Hashes are generated to document the integrity of both the original evidence and the working copy, allowing investigators to demonstrate that analytical processing occurred without altering the original artefacts.

## Automate Repetitive Tasks, Not Investigative Judgement

Digital forensic investigations involve many repetitive technical activities, including extracting messages, converting timestamps, organising conversations, resolving participant information, and generating timelines.

These activities are ideal candidates for automation.

Interpretation, however, is not.

WEP intentionally avoids drawing investigative conclusions or making assumptions about authorship, intent, or evidential significance. Those responsibilities remain with the examiner.

## Transparency Over Complexity

Every processing step performed by WEP is designed to be understandable and reproducible.

Rather than operating as a "black box," the project generates logs, structured exports, integrity manifests, and intermediate outputs that allow investigators to understand how information was produced.

Transparency improves confidence in the results and makes independent verification significantly easier.

## Investigator-Centred Design

The primary users of WEP are investigators, forensic analysts, and researchers rather than software developers.

Accordingly, outputs were designed to prioritise readability and investigative usefulness.

HTML reports, structured CSV exports, participant summaries, and timeline reports allow evidence to be reviewed quickly without requiring direct interaction with the underlying SQLite database.

## Incremental Development

WhatsApp continually evolves its database schema.

Attempting to build a comprehensive forensic platform in a single release would have introduced unnecessary complexity and reduced confidence in the software.

Instead, WEP has followed an incremental development strategy.

Each version introduces a small number of carefully validated capabilities while preserving compatibility with previous functionality.

This approach supports continuous improvement without compromising reliability.

---

# Solution Overview

SACS WEP processes extracted iOS WhatsApp evidence following forensic acquisition.

The workflow begins after investigators have already obtained the relevant WhatsApp artefacts, including `ChatStorage.sqlite` and any associated database files.

Once provided with an evidence folder, WEP performs a structured sequence of operations designed to prepare investigator-friendly outputs while maintaining evidential integrity.

At a high level, the processing workflow consists of:

1. Evidence identification.
2. Integrity hashing.
3. Working-copy creation.
4. SQLite database inspection.
5. Message extraction.
6. Entity resolution.
7. Timeline reconstruction.
8. Report generation.
9. Output hashing.
10. Processing documentation.

Rather than producing a single output file, the utility generates a collection of complementary artefacts that support different investigative activities, including timeline review, participant analysis, reporting, validation, and further examination.

This modular workflow allows future capabilities to be incorporated without requiring substantial architectural redesign.

---

# System Architecture

Although WEP currently operates as a command-line utility, its internal workflow follows a modular processing pipeline.

```text
Evidence Folder
        │
        ▼
Evidence Identification
        │
        ▼
SHA-256 Integrity Verification
        │
        ▼
Working Copy Creation
        │
        ▼
SQLite Inspection
        │
        ▼
Message Extraction
        │
        ▼
Entity Resolution
        │
        ▼
Timeline Processing
        │
        ▼
Report Generation
        │
        ▼
Output Hashing
        │
        ▼
Investigator Outputs
```

Each stage performs a specific responsibility before passing structured data to the next stage.

Separating responsibilities in this manner improves maintainability, simplifies debugging, and supports future expansion into additional evidence types.

---

# Key Features

At the time of writing, SACS WEP provides the following capabilities.

## Evidence-Safe Processing

- Processes forensic working copies rather than original evidence.
- Generates SHA-256 hashes for integrity verification.
- Maintains repeatable analytical workflows.

## WhatsApp Database Analysis

- Reads extracted iOS ChatStorage.sqlite databases.
- Supports associated WAL and SHM files.
- Performs read-only SQLite analysis.

## Message Processing

- Extracts WhatsApp message records.
- Converts timestamps into investigator-friendly formats.
- Categorises messages into logical groups.
- Associates messages with conversations where possible.

## Entity Resolution

Entity resolution significantly improves report readability by resolving identifiers into meaningful information wherever available.

Current capabilities include:

- Chat JID resolution.
- Chat name resolution.
- Sender JID resolution.
- Sender name resolution.
- Push name resolution.
- Group member resolution.

## Timeline Reconstruction

Generates chronological communication timelines suitable for investigative review.

Timeline outputs include:

- Message timestamps.
- Message direction.
- Participant information.
- Message categories.
- Media references.
- Conversation context.

## Reporting

Generated outputs currently include:

- CSV exports.
- HTML timeline reports.
- Chat summaries.
- Participant summaries.
- Processing logs.
- Database structure reports.
- Hash manifests.
- Run summaries.

These outputs are intended to support review, validation, documentation, and evidence organisation rather than replace examiner interpretation.



# Engineering Decisions

Developing WEP required balancing forensic best practices with practical investigative workflows. Rather than simply implementing features, each significant component of the project was guided by deliberate engineering decisions intended to maximise reliability, transparency, and usability.

## Working Copies Instead of Original Evidence

One of the earliest design decisions was to ensure that WEP never processes the original evidence database directly.

Although SQLite allows databases to be opened in read-only mode, relying solely on file access modes was considered insufficient from an evidential perspective. Investigators should always be able to demonstrate that analytical processing occurred independently of the original evidence.

For this reason, WEP creates a dedicated working copy before any analysis begins.

This approach offers several advantages:

- preserves the original evidence in an untouched state
- supports repeatable examinations
- aligns with accepted forensic handling practices
- reduces the risk of accidental evidence modification

This decision reflects the principle that protecting evidence integrity is more important than reducing processing time.

---

## SHA-256 Integrity Verification

Integrity verification is integrated throughout the workflow.

Rather than hashing only the original evidence, WEP also generates integrity hashes for generated outputs.

This provides investigators with an audit trail demonstrating:

- evidence authenticity
- processing consistency
- report integrity
- repeatability of generated outputs

The inclusion of output hashes was intended to improve documentation quality and simplify future validation exercises.

---

## Read-Only SQLite Processing

SQLite databases are central to modern mobile forensic examinations.

Instead of exporting database contents into proprietary intermediate formats, WEP performs direct read-only analysis of the original SQLite structures.

This preserves transparency because investigators can directly relate extracted information back to database tables and records.

It also makes troubleshooting considerably easier whenever WhatsApp modifies its schema.

---

## Structured Output Rather Than Raw Queries

Many investigators perform repeated SQL queries throughout an examination.

Although SQL provides flexibility, repeatedly constructing queries can become time-consuming and inconsistent between investigations.

WEP therefore transforms raw database records into structured investigative outputs that are immediately usable.

Examples include:

- chronological timelines
- participant summaries
- chat summaries
- HTML reports
- CSV exports

These outputs reduce repetitive manual work while remaining fully traceable to the underlying evidence.

---

## HTML Reporting

One deliberate decision was to generate HTML reports rather than limiting outputs to spreadsheets.

Investigative timelines often need to be reviewed by individuals with varying technical backgrounds, including investigators, supervisors, legal professionals, and occasionally courts.

HTML provides several advantages:

- readable formatting
- chronological presentation
- simple navigation
- portability
- compatibility across operating systems

It also allows future versions to incorporate richer visualisations without fundamentally changing the reporting workflow.

---

## Entity Resolution

Raw WhatsApp databases frequently contain identifiers that are meaningful to software but not necessarily to investigators.

A timeline containing only JIDs and internal identifiers is considerably more difficult to interpret.

Entity resolution was therefore introduced to translate available database information into investigator-friendly names wherever possible.

This significantly improves report readability while preserving underlying identifiers for verification purposes.

---

## Incremental Feature Development

Instead of attempting to implement every possible capability from the beginning, WEP has followed an incremental release strategy.

Each release introduces carefully validated functionality.

Examples include:

- message categorisation
- entity resolution
- participant analytics

This approach reduces technical debt, simplifies validation, and provides opportunities to refine architectural decisions as the project evolves.

---

## Explicit Recognition of Limitations

Another deliberate engineering decision was to clearly document what WEP does not do.

For example, the software does not attempt to determine:

- authorship
- intent
- legal attribution
- ownership of a device
- evidential significance

Those determinations remain the responsibility of trained investigators.

Making these limitations explicit reduces the risk of inappropriate reliance on automated outputs and reinforces the software's role as an investigative support utility rather than an autonomous forensic examiner.

---

# Technical Challenges

Developing WEP presented several technical and investigative challenges beyond ordinary software engineering.

Many of these challenges arose from the nature of forensic evidence itself, where accuracy, repeatability, and transparency are often more important than speed.

## WhatsApp Schema Evolution

WhatsApp's internal database structure changes periodically.

Fields may be renamed, relationships altered, and new message types introduced without public documentation.

Designing software capable of accommodating these changes required careful inspection of real datasets and an architecture that could evolve incrementally rather than depending on rigid assumptions.

---

## Timestamp Conversion

WhatsApp stores timestamps using Apple's reference date rather than standard Unix time.

Correctly converting these timestamps into investigator-readable formats was essential for accurate timeline reconstruction.

Small conversion errors could significantly affect investigative interpretation, particularly when correlating events across multiple evidence sources.

---

## Message Categorisation

WhatsApp message types are represented numerically within the database.

Interpreting these values required empirical analysis of real-world datasets.

The categorisation model currently implemented within WEP was developed through repeated validation and remains intentionally conservative, recognising that future WhatsApp versions may introduce additional message types.

---

## Entity Resolution

Resolving participants proved considerably more complex than initially anticipated.

Information relating to chats, group members, push names, and sender identifiers is distributed across multiple database tables.

Successfully reconstructing meaningful participant information required correlating records across these tables while gracefully handling incomplete or missing data.

---

## Large Dataset Processing

Real forensic datasets frequently contain tens of thousands of messages.

The validation dataset used during development exceeded forty-four thousand records.

Design decisions therefore needed to account for memory usage, processing efficiency, and report generation performance while preserving readability.

---

## Balancing Automation with Transparency

Perhaps the most significant challenge involved determining how much automation was appropriate.

Increasing automation improves efficiency but may reduce transparency if investigators cannot understand how results were generated.

Throughout development, preference was consistently given to approaches that maintained visibility into processing decisions, even where more complex automation might have been possible.

# Validation & Testing

A core design objective of SACS WEP was ensuring that every processing stage could be verified and reproduced. Rather than assuming correctness, each major feature was validated against a real iOS WhatsApp dataset containing 44,834 message records.

Validation focused on confirming that extracted data accurately reflected the underlying SQLite database while preserving forensic integrity.

## Validation Dataset

The primary validation dataset contained:

* 44,834 WhatsApp records
* Individual and group conversations
* Text messages
* Media messages
* System events
* Multiple participants
* Associated chat metadata

This dataset was intentionally selected because it represented a realistic forensic workload rather than a synthetic sample.

## Validation Objectives

The validation process sought to confirm that WEP could:

- Process extracted WhatsApp databases without modifying original evidence.
- Correctly extract message records.
- Convert timestamps into investigator-readable formats.
- Categorise supported message types accurately.
- Resolve chat and participant information where available.
- Generate structured CSV exports.
- Produce HTML timeline reports.
- Create integrity hashes for evidence and generated outputs.
- Generate processing documentation for examiner review.

## Validation Areas

The following capabilities were validated:

* Evidence-safe working copy creation
* Read-only SQLite processing
* SQLite schema inspection
* Message extraction
* Message categorization
* Entity resolution
* Timeline reconstruction
* HTML report generation
* CSV exports
* Chat summaries
* Participant summaries
* SHA-256 integrity verification
* Processing logs
* Run summaries

## Validation Results

Testing confirmed that the implemented functionality performed as expected across the validation dataset.

Key observations included:

| Metric | Result |
|--------|--------|
|Total Records Processed | 44,834 |
|Chat Records Resolved | 44,799 |
| Sender Records Resolved | 44,833 |
| Chats Summarized | 1,600 |
| Participants Summarized | 2,791 |
| HTML Timeline Records Generated | 44,834|

No write operations were performed against the evidence database during processing.

- Successful extraction of message records.
- Reliable timeline reconstruction.
- Correct generation of CSV exports.
- Successful HTML report generation.
- Accurate SHA-256 hash generation.
- Effective entity resolution for the majority of records.
- Consistent report generation across repeated executions.

Entity resolution statistics demonstrated substantial improvements in report readability by resolving both chat information and participant information wherever corresponding database records were available.

## Testing Philosophy

Rather than attempting to maximise the number of implemented features in early releases, development prioritised correctness and reliability.

Each new capability introduced into WEP is expected to undergo practical validation before being considered stable. This incremental validation strategy helps ensure that future functionality builds upon a reliable foundation rather than increasing technical complexity prematurely.

---

# Results & Impact

Although SACS WEP is currently an investigator-support utility rather than a complete forensic suite, it significantly reduces the amount of manual effort required when reviewing WhatsApp evidence.

Instead of manually navigating thousands of SQLite records, investigators receive structured outputs that are easier to review, search, filter, and correlate.

The project introduced several workflow improvements:

* Automated extraction of WhatsApp message records
* Structured CSV exports suitable for spreadsheet analysis
* Human-readable HTML timeline reports
* Automatic participant aggregation
* Timeline reconstruction
* Chat-level summaries
* Output integrity verification
* Repeatable processing workflow

For larger investigations involving tens of thousands of messages, these outputs substantially reduce repetitive manual database inspection.

The project also served as the practical foundation for the author's broader work in digital forensic automation and investigator tooling.

## Improved Investigative Efficiency

Investigators can rapidly obtain:

- chronological communication timelines
- participant summaries
- chat summaries
- structured exports
- integrity documentation

without manually reconstructing these outputs from raw database tables.

## Increased Report Readability

Entity resolution transforms internal database identifiers into meaningful participant and conversation information wherever possible.

This substantially improves the readability of generated reports while preserving traceability back to the original evidence.

## Repeatable Workflows

By standardising common analytical steps, WEP promotes greater consistency between examinations.

Investigators performing similar analyses are more likely to produce comparable outputs using a documented workflow rather than relying on individually developed SQL queries.

## Foundation for Future Development

Perhaps the most important outcome is that WEP has established a reusable architecture for future forensic utilities within SecureAfrica Cyber Solutions.

Rather than representing an isolated project, WEP forms part of a broader vision of investigator-focused software designed to support digital forensic examinations and cybercrime investigations.

---

# Lessons Learned

Developing WEP provided valuable technical and professional lessons extending beyond software development itself.

## Real Investigations Drive Better Software

The project reinforced the importance of building software around genuine investigative needs rather than hypothetical feature lists.

Many of the most valuable capabilities emerged directly from practical forensic work rather than from initial planning.

## Simplicity Improves Reliability

Adding features is relatively straightforward.

Maintaining reliability, transparency, and evidential defensibility is considerably more difficult.

Several design decisions favoured simpler, more understandable solutions over more complex implementations.

## Documentation Is Part of the Product

In forensic software, documentation is not merely supplementary.

Processing logs, integrity manifests, technical documentation, and validation reports all contribute to the trustworthiness of the software.

Producing clear documentation proved just as important as writing functional code.

## Engineering Never Truly Ends

Every validated release exposed opportunities for further refinement.

Rather than viewing unfinished functionality as failure, the project embraced continuous improvement through carefully planned iteration.

---

# Future Roadmap

WEP continues to evolve based on practical investigative requirements and lessons learned during development.

Planned areas of future development include:

- Expanded support for Android WhatsApp databases.
- Improved media awareness and media correlation.
- Richer participant analytics.
- Enhanced timeline intelligence.
- Additional reporting formats.
- Improved filtering and search capabilities.
- Case management enhancements.
- Plugin architecture for future artefact processing.
- Greater support for investigator customisation.
- Additional validation across a wider range of WhatsApp versions and acquisition methods.

Longer term, WEP is intended to become one component within a broader ecosystem of investigator-focused forensic tools developed under SecureAfrica Cyber Solutions.

---

# Technologies Used

| Category | Technologies |
|----------|--------------|
| Programming Language | Python |
| Database Processing | SQLite |
| Reporting | HTML, CSV |
| Integrity Verification | SHA-256 |
| Version Control | Git, GitHub |
| Development Environment | Visual Studio Code |
| Target Platform | Windows (primary), cross-platform compatible |
| Domain | Mobile Device Forensics |

---

# Repository

Source code, documentation, releases, and future development are maintained within the public project repository.

**Repository:**

https://github.com/p3n-c0/sacs-wep

---

# Closing Reflection

SACS WEP began as an effort to solve a practical investigative challenge encountered during digital forensic examinations. What started as a utility for reducing repetitive SQLite analysis gradually evolved into a broader exercise in forensic software engineering, where evidential integrity, transparency, repeatability, and investigator usability became the defining priorities.

Developing the project reinforced my belief that effective forensic software should assist investigators rather than replace them. Automation can significantly reduce repetitive technical work, but the interpretation of evidence, the evaluation of context, and the formation of investigative conclusions remain fundamentally human responsibilities.

Beyond its technical capabilities, WEP represents my broader commitment to developing practical technologies that strengthen cybercrime investigations within African digital environments. As SecureAfrica Cyber Solutions continues to expand its portfolio of investigative and cybersecurity products, WEP serves as an important foundation for future research, engineering, and innovation.

While the project remains under active development, each iteration reflects an ongoing commitment to continuous learning, careful engineering, and the responsible application of technology in support of digital investigations.
