# Public TUF transport pilot — Linux results

Executed on 2026-10-19 using disposable fixtures, without production keys.
Release: `v0.0.1`. The ZIP contains only `PILOT-ONLY.txt` (206 bytes).

| Check | Result |
| --- | --- |
| Real staging CLI over HTTPS | Exit 0, approved |
| Complete dependency inventory | 7 verified; 0 failed; 0 unattempted |
| Metadata branch before/after staging | Both `2c59fc000b2dc81ddbe26936c0923224470db7dc` |
| Expected Git reference intentionally wrong | Exit 1, rejected; all 7 dependencies unattempted |
| TUF client refresh with locally supplied pilot root | Passed over real HTTPS |
| TUF target download | Passed; exact 206 bytes and SHA-256 |
| One-byte-altered public probe | Rejected: SHA-256 digest mismatch |
| Metadata expiration | Rejected locally with simulated time after expiration |

Target SHA-256:
`45e3add8cb028b9de4ec978252c23d7192f342532dc28b743e64e3dae6c2cf7b`

Offline bundle SHA-256:
`bb9a55b5eff9007b77ac537a27f16aa663eb5b6153e06190de01045354de4897`

The signed pilot timestamp was published only after the successful staging gate,
in commit `b7581ae`. No production timestamp or product repository was changed.
Test private keys existed only in fixture-preparation process memory; they were
never serialized or uploaded. Root metadata contains public verification keys.

## Scope limits

- This is a disposable public transport pilot, not an application release.
- No Windows executable, installation, database migration or recovery was tested here.
- Expiration rejection used a simulated local clock, not an expired remote server.
- A live rollback/replay scenario was not executed in this pilot.
- Git reference reads are observations, not a lock on future remote publication.
- The pilot metadata expires at `2026-10-26T07:33:15+00:00`. Later rejection is
  expected and must not be bypassed by disabling expiration checks.
- The private product source, licenses, customer data and production keys are absent.

This pilot does not enable automatic updates in installed NODRA-WISP clients.
