# Postmortem

A skill for evidence-grounded session, incident, deployment, and project retrospectives. It turns findings into root causes, priced impact, scorecard continuity, and executable changes intended to prevent recurrence.

## Install

```bash
git clone https://github.com/PSkinnerTech/postmortem-skill.git ~/.codex/skills/postmortem
```

The Nessie skill and an accessible local Nessie runtime are required for reading or publishing Nessie material. The bundled standing prompt supplies the contract when its canonical Nessie version is unavailable.

## Use

> Use $postmortem to produce a draft-only postmortem for this completed session.

Read [SKILL.md](SKILL.md) and the complete [standing prompt](references/standing-prompt-v1.1.md). Supply or identify the session boundary, repository, primary evidence, and predecessor report where applicable. The workflow uses a 20-gate publication check and normally saves a Nessie context and repository report; an explicit draft-only or read-only request limits those side effects.

This repository stores the reusable skill and contract. Keep session transcripts, credentials, and generated incident reports in the destinations chosen for each investigation.
