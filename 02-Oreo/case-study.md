# SACS Oreo
## Executive Summary

SACS Oreo is a Python-based command-line application developed by SecureAfrica Cyber Solutions (SACS) to support authorized web application security assessments. The project was created to provide a lightweight, transparent, and extensible security assessment framework that emphasizes evidence quality, reproducibility, and responsible testing.

Unlike traditional vulnerability scanners that prioritize broad vulnerability coverage, Oreo was designed around a different philosophy: producing findings that are understandable, verifiable, and useful to both technical practitioners and decision-makers. Every identified issue includes structured evidence, confidence indicators, reproducibility information, remediation guidance, and business impact explanations tailored to organizations operating in Nigeria and broader African environments.

The current implementation represents the first Minimum Viable Product (MVP) of the platform. It performs safe reconnaissance, crawls authorized web applications, executes non-destructive security checks, and generates structured HTML and JSON reports suitable for technical review.

The project also serves as the architectural foundation for future development into a more comprehensive web application security assessment platform capable of supporting modular testing, evidence preservation, and advanced reporting workflows.

## The Problem

Many vulnerability scanners generate extensive lists of findings but provide limited context regarding the reliability, reproducibility, or operational significance of those results. This often leaves security practitioners spending considerable time validating false positives, correlating evidence, and translating technical findings into language that organizations can understand.

For smaller organizations, educational institutions, startups, and businesses across Africa, existing enterprise security assessment platforms may also be financially inaccessible or unnecessarily complex for routine security evaluations.

The objective behind Oreo was not to replace mature commercial security tools. Instead, the goal was to develop an investigator-oriented assessment framework that prioritizes transparency, evidence quality, and actionable reporting while remaining lightweight and extensible.

## Objectives

The project was developed with several primary objectives:

Provide a safe framework for authorized web application security assessments.
Produce structured findings supported by verifiable evidence.
Reduce false positives through confidence and reproducibility indicators.
Generate reports that are understandable to both technical and non-technical stakeholders.
Support secure software development and security review processes for organizations with limited security resources.
Establish an extensible architecture capable of supporting future security assessment modules.
