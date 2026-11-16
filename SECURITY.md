# Security Policy

## Reporting a Vulnerability

Please do not open a public issue, discussion, or pull request for a suspected vulnerability.

Use the **Report a vulnerability** button on the affected repository's **Security** tab. If the repository does not show that button, check whether a private reporting advisory is already available and contact the maintainers through that private channel.

Keep technical details in the private advisory. Do not include seed phrases, private keys, production credentials, live user data, or funds in a report. Do not test against accounts, funds, or deployments you do not own or have explicit permission to test.

We aim to acknowledge a new report within 2 business days. If you do not receive a response, add a comment to the private advisory. If private reporting is unavailable, email security@arklabs.to without technical details and ask for a private channel.

## Scope

This default policy applies to public repositories under Arkade OS and Ark Labs that do not provide their own SECURITY.md.

In scope are source, release artifacts, published packages, and services operated by Ark Labs or Arkade OS from an unmodified release. We welcome reports involving key safety, funds, VTXOs, settlement, payment state, contract compilation, signing, authentication, tenant isolation, release integrity, and infrastructure trust boundaries.

A custom fork or modified deployment that is not operated by Ark Labs or Arkade OS is out of scope. A third-party dependency should also be reported upstream, but it is in scope here when the issue creates an exploitable path through our code or a supported deployment. Feature requests, non-security bugs, social engineering, physical attacks, spam, and public disclosure before coordination are not vulnerability reports.

Documented alpha, testnet, or unaudited status is severity context, not a blanket exclusion when the issue can reach a supported mainnet or published release path.

## Threat Model

Assets include private keys and signing authority, funds and VTXOs, contract source and artifacts, settlement and payment state, service credentials, enclave or MPC material, user data, and release integrity.

Treat network traffic, RPC, HTTP, and gRPC input, invoices and webhook payloads, relay and peer messages, contract source and artifacts, repository metadata, build inputs, dependencies, and state created by another participant as attacker-controlled.

Users control their own keys. Servers, operators, solvers, plugins, peers, RPC providers, and relayed messages are untrusted unless a protocol step verifies them. A valid signature, successful response, relayed message, or quote is not authorization by itself.

## Security Invariants

- No spend may bypass the signatures, timelocks, asset rules, or other conditions required by the protocol.
- Private keys and credentials must not leave their intended trust domain or appear in logs or diagnostics.
- Clients must validate the exact network, transaction intent, amount, fee, destination, asset, and artifact before signing.
- Payment, swap, batch, renewal, settlement, and recovery transitions must be idempotent and resistant to replay or duplicate credit.
- A service must authorize before mutation and keep tenants, merchants, stores, wallets, and sessions isolated.
- Untrusted input must be bounded and parsed safely, and authority must fail closed when verification is unavailable.
- Enclave, MPC, KMS, and signing controls must bind authority to the expected code and configuration.
- Released code, packages, and deployment configuration must have verifiable provenance and must not silently gain authority from an untrusted update.

## Severity Context

- **Critical:** theft or loss of funds or keys at scale, unauthenticated signing or spending, a protocol or VM bypass across users, enclave or MPC secret extraction, or broad package compromise.
- **High:** practical loss of one user's or merchant's funds, repeatable double settlement, authorization bypass to a privileged operation, persistent production denial of service, or a supported-release supply-chain flaw.
- **Medium:** bounded denial of service, cross-user information disclosure, privilege escalation without direct fund impact, or a control bypass with realistic but limited preconditions.
- **Low:** a demonstrated information leak, missing hardening, or defense-in-depth gap without a practical path to meaningful impact.

## Remediation and Coordinated Disclosure

We aim to remediate a confirmed vulnerability within 90 business days from acknowledgement. Severity, dependency constraints, protocol compatibility, and coordinated testing can change that target; we will explain material delays in the private advisory.

We will coordinate a public disclosure date and credit with the reporter after remediation. If exploitation creates an immediate risk to users, we may publish mitigations before the full advisory.

## Reporting Template

```text
* Summary:
* Repository, release, commit, or deployment:
* Security impact:
* Preconditions and attacker capability:
* Steps to reproduce and proof of concept:
* Affected keys, funds, data, or transactions:
* Suggested severity and reasoning:
* Suggested mitigation:
* Credit preference:
```

Redact secrets, private keys, seed phrases, live credentials, addresses not controlled by the reporter, and personal data.

The companion organization is [ArkLabsHQ](https://github.com/ArkLabsHQ).
