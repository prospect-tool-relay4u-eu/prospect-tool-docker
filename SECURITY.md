# Security Policy

## Scope

This sandbox exists specifically so security researchers can test the Relay4U prospecting tool. Testing against the stack you run locally via this repo's `docker-compose.yml` is **welcome and encouraged**.

**Out of scope:**
- The real relay4u.eu staging and production environments, and any other infrastructure not started by this repo's `docker-compose.yml`
- Any GCP/cloud infrastructure belonging to `prospect-tool-relay4u-eu`
- Denial-of-service testing, even against your own local sandbox instance (no need — it's disposable, just restart it)
- Social engineering, phishing, or physical security testing

There is no data of any real value in this sandbox — it's a fresh, empty database until you (or another tester) put something in it via your own local instance.

## Reporting a finding

Please open a [GitHub issue](https://github.com/prospect-tool-relay4u-eu/prospect-tool-docker/issues/new/choose) on this repo using the pentest finding template. Include reproduction steps against the sandbox (image tag/version if relevant, request/response details, expected vs. actual behavior).

There is currently no bug bounty program — this is a community/educational sandbox, not a paid disclosure program.

## Responsible disclosure

If you find something that would be dangerous to disclose publicly before a fix ships (e.g. an auth bypass, injection vulnerability, or anything that could plausibly also affect the real deployed product, not just this sandbox), please don't open a public issue with exploit details. Instead, email **bartoszwojcik.java@gmail.com** with the details so it can be fixed, then follow up with a public issue for tracking once resolved.
