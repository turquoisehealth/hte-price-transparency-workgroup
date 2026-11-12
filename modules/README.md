# Modules

One folder per module on the [HTE workgroup module map](https://open.forpatients.health/docs/resources/hte-workgroup).
Each folder is a placeholder until its code lands.

| ID | Module | Purpose |
|---|---|---|
| M0 | [Directory & endpoints](m00-directory-endpoints/) | Finds providers and plans, and where to send each request. |
| M1 | [Status & audit trail](m01-status-audit-trail/) | Tracks the state of an estimate across every step and keeps a record of what happened. |
| M2 | [Trigger & intake](m02-trigger-intake/) | Starts an estimate from any app and turns the request into a standard GFE Information Bundle. |
| M3 | [Service packages](m03-service-packages/) | Names a service and lists the parts that usually come with it (roles, codes, modifiers). |
| M4 | [Provider pricing](m04-provider-pricing/) | Gets each provider's expected charge for each line from a swappable price source. |
| M5 | [Convening & coordination](m05-convening-coordination/) | Gathers every provider's piece into one estimate for the whole episode of care. |
| M6 | [GFE packet & patient copy](m06-gfe-packet/) | Produces a compliant GFE Packet and a copy the patient can read. |
| M7 | [Submission & routing](m07-submission-routing/) | Sends the finished estimate to the patient's plan. |
| M8 | [Allowed amount & network](m08-allowed-amount-network/) | Checks network status and the allowed amount for each line. |
| M9 | [Benefits & accumulators](m09-benefits-accumulators/) | Shows the member's coverage today: deductible, copays, coinsurance, prior auth. |
| M10 | [Adjudication & AEOB](m10-adjudication-aeob/) | Works out who pays what before care and issues the Advanced EOB. |
| M11 | [Patient experience SDK](m11-patient-experience-sdk/) | Shows the patient a clear estimate and lets them compare options. |
| M12 | [Conformance & sandbox](m12-conformance-sandbox/) | Proves each module works, using synthetic data and validators. |
