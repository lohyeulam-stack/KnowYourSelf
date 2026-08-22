# Security Policy

KnowYourSelf is a public methodology repository. It is intentionally designed so that private personal and company information stays outside the public repository.

## Do not publish secrets

Never commit:

- API keys
- access tokens
- passwords
- cookies
- private keys
- cloud credentials
- private customer data
- private company documents
- private chat exports
- secret-bearing URLs

If a secret was accidentally published, rotate or revoke it first, then report the incident. Do not rely on deleting the commit alone.

## Reporting a security issue

For a suspected security or privacy issue in the repository itself, please open a GitHub Security Advisory when available. If that channel is not available, use a private GitHub contact method rather than publishing sensitive details in an issue.

Do not include credentials, customer records, private source code, or exploit details that would create additional risk in a public issue.

## Scope

This policy covers the public materials in this repository, including prompts, schemas, examples, documentation, and automation guidance.

It does not grant permission to inspect or disclose private systems, company environments, or third-party services referenced by users of the methodology.

## Design expectation

The Knowledge OS design itself follows a deny-by-default approach:

- Security Domain first, topic second;
- cross-domain access denied by default;
- Project context isolated from unrelated projects;
- public methodology separated from private implementation data;
- long-term memory must not become an uncontrolled channel for sensitive information.
