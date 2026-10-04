# Guardrail catalogue and compliance flags

## Guardrail groups

Propose only what this POC needs, from six groups:

- **Input:** file type and size checks, prompt-injection screening (customer content such as emails or documents can contain instructions aimed at the AI), masking personal data before a model sees it
- **Output:** schema validation, confidence thresholds with low-confidence cases sent to a human, grounding answers in the source, no medical, legal or financial advice unless the brief requires it and a qualified person reviews it
- **Actions:** allow-listed tools only, read-only access by default, human approval for anything irreversible
- **Cost and runtime:** step and token caps per transaction, daily budget alerts, timeouts, fallbacks when a model is unavailable
- **Data:** approved region only, retention limits, encryption, an audit trail that does not store sensitive content
- **Operations:** monitoring, error alerts, a kill switch, a named escalation contact

For each guardrail, state the risk it addresses, its risk level (High, Medium or Low), how it will be tested and its cost impact.

## Compliance flags

Raise these as flags to check with the right person. They are not legal advice.

Ask which countries and sectors the POC involves, if the house rules or the handover pack don't say. Then flag the main rules for them, for example:

- **European Union and UK:** GDPR and UK GDPR; the EU AI Act for some uses of AI
- **United States:** HIPAA for health data; state privacy laws such as California's CCPA
- **United Arab Emirates:** the Personal Data Protection Law; health-data rules in some emirates
- **Saudi Arabia:** the Personal Data Protection Law; national cybersecurity and cloud controls
- **India:** the Digital Personal Data Protection Act
- **Australia:** the Privacy Act
- **Sector rules:** health, finance, education and children's data often carry extra obligations

Flag other regimes you know apply. Say clearly when you are unsure.
