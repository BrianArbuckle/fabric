# Python TLS trust warning (2026-10-23)

This checkout has legacy Python tooling or stale dependency/bootstrap inputs that need review before reuse. An installed environment may already be patched; restoring old requirements, lockfiles, cached wheels, or ensurepip seeds can reintroduce the affected certificate.

The [Python security announcement](https://discuss.python.org/t/information-for-python-users-regarding-emudhra-emsign-ca-certificate-security-incident/109576) describes the eMudhra/emSign incident and possible TLS interception, including package downloads. The affected root certificate SHA256 is:

`86a1ecba089c4a8d3bbe2734c612ba341d813e043cf9e8a862cd5c57a36bbe6b`

Finding this certificate or an old dependency does not prove exploitation.

Before reuse:

1. Rebuild and test with a supported Python runtime. pip 26.2.2 requires Python 3.10 or newer, so a Python 3.8/3.9 environment cannot take that fix in place.
2. Use pip >=26.2.2, certifi >=2026.10.19, and uv >=0.13.4 where applicable. Updating application certifi or system trust alone does not replace pip's vendored bundle.
3. Avoid ordinary network installs with old pip. Bootstrap patched tooling using a trusted download and independently verified published checksum, or verified offline wheels, as described in the announcement.
4. Review dependency pins, lockfiles, container images, caches and bootstrap seeds before rebuilding. Verify the affected fingerprint is absent from the bundles actually used, then run the project's tests.

This warning records a deferred compatibility/remediation task. It does not upgrade the application or certify its current runtime.

## Evidence in this checkout

- `poetry.lock` records `certifi==2024.2.2`.
