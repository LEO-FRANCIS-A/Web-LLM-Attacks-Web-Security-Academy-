# Web LLM Attacks | PortSwigger Web Security Academy

## Overview

This repository documents my learning and hands-on exploration of **Web LLM Attacks** through PortSwigger Web Security Academy. It focuses on understanding security vulnerabilities that arise when Large Language Models (LLMs) are integrated into web applications.

As organizations increasingly integrate LLMs into their applications, they introduce new attack surfaces. These models may have access to sensitive data, internal APIs, plugins, and application functionality. Attackers can exploit these integrations to manipulate model behavior, access unauthorized information, or trigger unintended actions.

## What are Web LLM Attacks?

Web LLM attacks target vulnerabilities in applications that integrate Large Language Models. Rather than attacking the model alone, these attacks focus on how the application provides data, tools, APIs, and permissions to the LLM.

An attacker may exploit these integrations to:

- **Access sensitive information:** Retrieve confidential data available to the LLM, including system prompts, application data, or information exposed through connected APIs.
- **Manipulate model behavior:** Use prompt injection to influence the LLM into ignoring its intended instructions or performing unintended operations.
- **Exploit connected APIs:** Abuse the LLM's access to backend APIs, functions, and plugins to perform unauthorized actions.
- **Attack other systems:** Leverage the LLM as an intermediary to interact with internal services or other components that are not directly accessible.

## Key Concepts

This repository explores the following fundamental concepts:

| Concept | Description |
|---|---|
| Large Language Models (LLMs) | Understanding how LLMs process prompts and generate responses. |
| Prompt Injection | Manipulating model instructions through crafted user inputs. |
| LLM API Integration | Understanding how LLMs interact with external APIs and application functionality. |
| Excessive Agency | Exploiting LLMs that have excessive permissions or access to sensitive tools. |
| Information Disclosure | Extracting sensitive information accessible to the LLM. |
| Indirect Attacks | Using an LLM as an intermediary to attack other systems and components. |

## Learning Objectives

The primary objectives of this repository are to:

- Understand the architecture of LLM-integrated web applications.
- Identify and analyze the attack surface introduced by LLM integrations.
- Understand different prompt injection techniques and their security implications.
- Investigate how LLMs interact with APIs, functions, and plugins.
- Explore how attackers can abuse excessive permissions and capabilities.
- Develop a security-oriented understanding of LLM-integrated applications.

## Why Web LLM Security Matters

Traditional web application security focuses on vulnerabilities in application logic, APIs, authentication, and data handling. LLM integrations introduce an additional layer of complexity because models can interpret natural-language instructions and interact with application functionality.

An insecure LLM integration can become a gateway to sensitive data and backend functionality. Therefore, securing the integration between the LLM, the application, and its connected tools is just as important as securing the model itself.

## Resources

- [PortSwigger Web Security Academy – Web LLM Attacks](https://portswigger.net/web-security/llm-attacks)
- [OWASP Top 10 for LLM Applications](https://genai.owasp.org/llm-top-10/)

## Disclaimer

This repository is intended for educational and cybersecurity research purposes. All security testing and exploitation activities are performed within authorized environments, including PortSwigger Web Security Academy labs.
