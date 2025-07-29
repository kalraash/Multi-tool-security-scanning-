# Multi-tool-security-scanning
We implemented a multi-tool security scanning pipeline targeting GitHub repositories associated with the Pearl. Each tool addressed a different layer of potential risk

1. Snyk – Dependency & Configuration Vulnerability Scanning

Scope: Scanned for known vulnerabilities in third-party dependencies (e.g., package.json, pyproject.toml, code analysis) and misconfigurations in the code 

Execution:

Integrated as a GitHub Action.

Triggered automatically on push and pull requests.

Output: Identified CVEs, outdated packages, insecure configuration (e.g., hardcoded secrets, server information exposure, overly permissive access and path traversal vulnerabilities).

2. Semgrep – Static Code Analysis (SAST)
Scope: Performed customizable static code scanning for security anti-patterns, logic flaws, and insecure coding practices in application code (JavaScript, Python, etc.).

Execution:

Ruleset customized to the application’s threat model (e.g., secrets in code, unsafe deserialization, insecure regex).

CI/CD integrated scan with GitHub Actions.

Output: Flagged issues like: Detected child processes, lack of http usage, path traversal, wildcard-cors

3. CodeQL – Semantic Code Analysis
Scope: Used for deep semantic code analysis, focusing on security vulnerabilities (e.g., injection, flow analysis).

Execution:

GitHub-native scanning via codeql-analysis.yml.

Supports automatic PR checks.

Output:

Detected dataflow issues (e.g., clear text logging of sensetive information, information exposure, untrusted user input reaching sensitive sinks).

4. OWASP ZAP – Dynamic Application Security Testing (DAST)
Scope: Performed runtime analysis of the desktop app’s web components (if exposed via a local server ).

Execution:

Local instance or CI container deployed with test environment.

Active scanning used to simulate attacker behavior (XSS, SQLi, etc.).

Output:

Detected missing security headers, reflected inputs, CORS misconfigurations.

Verified actual exploitability of flagged issues with the development team to get their opinion and analyze the issue.
