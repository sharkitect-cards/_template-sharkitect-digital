# Sharkitect Digital — Card Template

Company-locked template for Sharkitect Digital premium card builds (Tier-based per-client cards starting with Chris's premium card). **Only person-level fields are tokenized at v1 (token-replace).** Company assets (logo, accent color, manifest) are baked in here. Phase 3B introduces the dynamic field schema so multi-block, widget-driven cards build from `card_configs` in Supabase.

> **Phase 3A status (2026-04-29):** scaffold cloned from `_template-fantastic-floors`. Brand color (`--accent: #29ABE2` Electric Blue), logo placeholder, manifest, and visible company-name text are Sharkitect. **Hardcoded FF copy still inside `index.html`** (website URL line ~329/331/396, tagline, descriptor, office phone, address) is Phase 3B M3B.5+ work — replaced when the new field schema lands.

## How to spawn a new Sharkitect Digital card

```bash
gh repo create sharkitect-cards/{person-slug} \
  --template sharkitect-cards/_template-sharkitect-digital \
  --public
```

Then fill the 4 person tokens in the spawned repo's `index.html` and `manifest.json`. (After Phase 3B, n8n's Card Intake workflow handles spawn + token-fill end-to-end from a Supabase `card_configs` row.)

## Tokens

Person-level placeholders that need to be replaced per-card:

| Token | Example | Notes |
|---|---|---|
| `{{PERSON_FULL_NAME}}` | `Chris Estrada` | Display + meta + vCard FN |
| `{{PERSON_FIRST_NAME}}` | `Chris` | vCard N field |
| `{{PERSON_LAST_NAME}}` | `Estrada` | vCard N field |
| `{{PERSON_TITLE}}` | `Founder` | Display + meta + vCard TITLE |
| `{{PERSON_PHONE_DISPLAY}}` | `(816) 555-1212` | Span + vCard TEL |
| `{{PERSON_PHONE_E164}}` | `+18165551212` | `tel:` href |
| `{{PERSON_EMAIL}}` | `solutions@sharkitectdigital.com` | `mailto:` href + span + vCard EMAIL |
| `{{PERSON_PHOTO_B64}}` | (optional) | JPEG base64 headshot — leave empty if none |

That's it. Four inputs (name, title, phone, email) produce all seven display tokens. Photo is optional.

## What is NOT a token (baked in v1; promoted to dynamic fields in Phase 3B)

- Company name: `Sharkitect Digital`
- Office phone: TBD (Phase 3B M3B.5+)
- Office address: TBD (Phase 3B M3B.5+)
- Website: TBD (Phase 3B M3B.5+) — currently still shows FF URLs at lines ~329/331/396 of `index.html` from the original FF clone; replace when 3B field schema lands.
- Tagline: TBD (Phase 3B M3B.5+) — FF's `We're All You Need` still shown until 3B
- Descriptor: TBD (Phase 3B M3B.5+)
- Logo: `logo.svg` (512×512 square placeholder, chrome triangle + "S" + Electric Blue accent ring; replace with chrome-metallic master in Phase 3B M3B.5+)
- Accent: Electric Circuit Blue `#29ABE2`
- Background: Sophisticated Charcoal `#1A1A1A`

If any baked field changes after Phase 3B, the propagation tool (`tools/propagate-template.py`, shipped Phase 2) flows the update to every spawned card on the next sync.

## Files

- `index.html` — card HTML with 8 person tokens
- `logo.svg` — Sharkitect Digital placeholder, 512×512 square (Phase 3A; chrome-metallic master replaces in Phase 3B M3B.5+)
- `manifest.json` — PWA manifest with 2 person tokens (name, description); `short_name` is `"Sharkitect"`, apple-title `"My Card"` per the owner-phone-perspective rule
- `README.md` — this file

## Do not serve this repo directly

This repo is the template. GitHub Pages is NOT enabled on it — it would render with literal `{{TOKENS}}` visible to users. Always spawn via `--template`, fill the tokens, enable Pages on the spawned repo.
