# Security Notes: Log4Shell

## Advisory identification

- GHSA identifier: GHSA-jfh8-c2jp-5v3q
- CVE identifier: CVE-2021-44228
- Severity: critical (CVSS 3.1 score 10.0, vector CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:C/C:H/I:H/A:H/E:H)
- Summary as reported by the GitHub advisory database: "Remote code injection in Log4j"

## Impact assessment

- Affected package: org.apache.logging.log4j:log4j-core (Maven ecosystem)
- Vulnerable version range (primary range for this CVE): >= 2.13.0, < 2.15.0
- Additional affected ranges reported by the advisory database:
  - org.apache.logging.log4j:log4j-core: >= 2.0-beta9, < 2.3.1 (fixed in 2.3.1)
  - org.apache.logging.log4j:log4j-core: >= 2.4, < 2.12.2 (fixed in 2.12.2)
- Impact: logging untrusted or user-controlled data with a vulnerable Log4j version may result in remote code execution (RCE), including via exception traces, authentication failures, and other vectors of user-controlled input.

## Remediation guidance

- First patched version: 2.15.0
- Recommended target: upgrade to Log4j 2.16.0, which disables JNDI by default and completely removes support for message lookups. Backports of the fix are also available in 2.3.1, 2.12.2, and 2.12.3.
- Mitigation if unable to upgrade: ensure no attacker-controlled JNDI lookups resolve, and ensure the JndiLookup class is not loaded.

## Follow-up advisory

- GHSA identifier: GHSA-7rjr-3q55-vv33
- CVE identifier: CVE-2021-45046
- Severity: critical (CVSS 3.1 score 9.0, vector CVSS:3.1/AV:N/AC:H/PR:N/UI:N/S:C/C:H/I:H/A:H)
- Summary as reported by the GitHub advisory database: "Incomplete fix for Apache Log4j vulnerability" - the Log4j 2.15.0 fix for CVE-2021-44228 was incomplete in certain non-default configurations, addressed by upgrading to 2.16.0.
