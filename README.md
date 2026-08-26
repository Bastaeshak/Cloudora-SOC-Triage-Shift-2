# Cloudora SOC Triage - Shift 2

## Overview

This repository documents my second SOC analyst shift in the Cloudora security environment.

During this shift, I investigated four alerts involving phishing, identity activity, outbound email, and duplicate detection paths. I used KQL, email header analysis, Help Desk records, shift intelligence, and alert telemetry to determine what actually happened and document a defensible verdict for each alert.

All activity and data in this engagement are synthetic, but I approached each investigation as I would during an actual SOC shift.

---

## How I Worked

For each alert, I followed a seven-part triage process:

1. **Alert** - Identified what triggered and which users, systems, or infrastructure were involved.
2. **Hypothesis** - Developed both malicious and benign explanations.
3. **Evidence Checked** - Reviewed the available logs, email headers, KQL results, Help Desk records, and shift context.
4. **Verdict** - Classified the alert as True Positive, False Positive, Duplicate, Escalate, or Insufficient Data.
5. **Severity** - Assigned Informational, Low, Medium, or High based on the evidence and context.
6. **Action** - Determined what response was appropriate.
7. **Justification** - Documented the evidence supporting my decision.

I focused on verifying business context against the raw evidence instead of assuming an alert or handover note was correct.

---

## Investigations

### CLD-0205 - Bexley Credential-Harvesting Email

Marcus Oje received an email titled **"DocuSign: Bexley integration contract ready for signature."**

I analyzed the raw email and identified failed SPF and DMARC authentication, no DKIM signature, a suspicious lookalike domain, and a link leading to `192.0.2.203`.

A related sandbox detection later confirmed that the landing page was credential harvesting. Scope analysis showed only one recipient, and Marcus did not submit credentials.

The phishing theme was especially significant because the attacker referenced the active Bexley integration project.

**Verdict:** True Positive  
**Severity:** Medium  
**QA Review:** Satisfactory

My original severity was Low. QA corrected this to Medium because the company-specific Bexley targeting had threat-intelligence value even though the attack was contained.

---

### CLD-0206 - Atypical Travel

An atypical-travel alert fired for `helen.dray@cloudora.io` after sign-ins from Manchester and Lisbon.

I used KQL to review Helen's available sign-in activity and determine whether the Lisbon IP appeared on other Cloudora accounts.

The Lisbon authentication used Helen's registered iOS device, succeeded on the first attempt, and satisfied MFA.

Help Desk ticket `HD-5102`, created before the event, documented that Helen would be in Lisbon from October 6-10 and expected to use mobile access.

The location, date, device, and access method all matched the documented travel.

**Verdict:** False Positive  
**Severity:** Informational  
**QA Review:** Excellent

---

### CLD-0207 - Outbound Marketing Mail Surge

An outbound send-rate alert fired after `marketing@cloudora.io` sent 640 external messages through `mailflow-platform.example`.

I correlated the alert with Help Desk ticket `HD-5138`, which documented an approved Tuesday morning October newsletter campaign through the same platform to approximately 640 recipients.

The volume, timing, connector, and content matched the documented campaign. The activity also originated from the marketing platform connector rather than an interactive user session.

**Verdict:** False Positive  
**Severity:** Informational  
**QA Review:** Excellent

---

### CLD-0208 - Post-Delivery Malicious URL Detection

A second alert was generated after sandbox detonation classified the URL from CLD-0205 as credential harvesting.

I correlated the recipient, subject, timestamp, and URL with CLD-0205 and determined that both alerts represented the same phishing event.

CLD-0208 added new evidence by confirming the credential-harvesting landing page and the one-recipient scope. That evidence was incorporated into CLD-0205 rather than creating a separate incident trail.

**Verdict:** Duplicate of CLD-0205  
**Severity:** Informational  
**QA Review:** Excellent

---

## What I Learned

The biggest lesson from this shift was that **contained does not automatically mean Low severity**.

I initially rated CLD-0205 Low because no credentials were entered and no compromise occurred. QA showed that Medium was more appropriate because the attacker demonstrated knowledge of Cloudora's active Bexley project.

I learned to consider not only impact, but also confidence, targeting, business context, and intelligence value when assigning severity.

I also learned that **formal escalation and intelligence notification are different**. An incident may not meet the SOP threshold for an Escalate verdict while still containing targeted activity worth flagging to the vCISO.

CLD-0206 reinforced another important lesson: a detection rule accurately identifying unusual activity does not automatically make the security verdict a True Positive. The underlying activity must actually be malicious.

Finally, CLD-0208 reinforced the importance of correlating duplicate detection paths and maintaining one incident of record rather than splitting evidence across multiple tickets.

---

## Skills Practiced

- SOC alert triage
- Phishing investigation
- Email header analysis
- SPF, DKIM, and DMARC analysis
- KQL investigation
- Identity and authentication analysis
- User and IP baselining
- Help Desk correlation
- Business-context analysis
- Severity assessment
- Threat-intelligence identification
- Duplicate alert correlation
- ServiceNow incident documentation
- Shift handover documentation
- Evidence-based incident closure

---

## Shift Results

- **4 alerts investigated**
- **1 True Positive**
- **2 False Positives**
- **1 Duplicate**
- **3 Excellent QA reviews**
- **1 Satisfactory QA review**

---

## Repository Contents

**`verdicts/`** - Detailed investigation notes for CLD-0205 through CLD-0208, including evidence checked, verdicts, severity, actions, and justification.

**`handover.md`** - End-of-shift handover documenting the phishing incident, completed investigations, and monitoring recommendations.

---

## Disclaimer

All data in this engagement is synthetic, including reserved IP ranges and domains. No real Cloudora systems, users, credentials, or customer information are represented.

The investigation decisions, verdict reasoning, documentation, and analysis in this repository are my own work.
