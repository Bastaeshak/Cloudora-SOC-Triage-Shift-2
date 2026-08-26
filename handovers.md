# End-of-shift handovers · Cloudora


## Shift 2 · 2026-08-26

SHIFT 2 HANDOVER

CLD-0205 - Confirmed credential-harvesting phishing email targeting Marcus Oje. One recipient tenant-wide. Marcus reported no credential submission and no downstream compromise identified. docusign-verify.example and 192.0.2.203 documented as malicious indicators. Recommend blocking the domain, IP, and malicious URL at appropriate controls. CLD-0205 remains the incident of record.

CLD-0206 - Atypical travel for Helen Dray determined to be legitimate. HD-5102 documented Lisbon travel Oct 6-10 with expected mobile-only access. Lisbon sign-in matched the documented dates/location, used Helen's registered iOS device, and satisfied MFA.

CLD-0207 - Outbound marketing send determined to be authorized. 640-message October newsletter matched HD-5138, including expected Tuesday timing, mailflow-platform.example connector, and approximately 640 recipients.

CLD-0208 - Duplicate of CLD-0205. Post-delivery sandbox detonation independently confirmed 192.0.2.203 as credential harvesting and established one recipient tenant-wide. New evidence incorporated into CLD-0205.

WATCH NEXT SHIFT:
- Monitor for additional activity involving docusign-verify.example or 192.0.2.203.
- Re-raise CLD-0205 if another user/host is affected, credential compromise is identified, or client/payroll data access is discovered.
- Bexley integration remains active, so continue treating related phishing lures seriously while verifying them against evidence.
- CLD-0205 and CLD-0208 were not present in the available ServiceNow instance, so their ServiceNow cross-reference/duplicate closure could not be completed.
