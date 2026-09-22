# CLAUDE.md, laposta-skill: de Laposta-skill en zijn marketplace

<!-- LET OP: deze repo is publiek. Alles in dit bestand is openbaar, net als de commit-berichten
     en de PR-titels. Geen interne paden, repo-namen, accountnummers of werkwijze. -->

An Agent Skill that lets an AI assistant work with the Laposta API (lists, subscribers, custom
fields, segments, campaigns, results, webhooks), plus the marketplace definition that makes it
installable in Claude Code.

## Leesvolgorde

1. Dit bestand.
2. `plugins/laposta/skills/laposta/SKILL.md`: de skill zelf. Dat is het bestand dat telt.
3. Alleen de `references/`-pagina die je fix raakt: `endpoints.md`, `schemas.md`, `tasks.md`,
   `errors-and-limits.md`, `pitfalls.md`.

Niet inlezen: `spec/openapi-en.yml` in zijn geheel. Grep erin.

## Hoe het in elkaar zit

| wat | waar |
| --- | --- |
| marketplace | `.claude-plugin/marketplace.json`, verwijst naar `./plugins/laposta` |
| de plugin | `plugins/laposta/.claude-plugin/plugin.json` |
| de skill | `plugins/laposta/skills/laposta/SKILL.md` |
| naslag | `references/`, **gegenereerd** uit `spec/` door `scripts/generate-reference.py` |

Er is geen dienst en geen deploy. De repo wordt door Claude Code zelf gelezen bij het starten
van een sessie.

## De commando's

| wat | commando |
| --- | --- |
| naslag opnieuw genereren | `python3 scripts/generate-reference.py` |
| de JSON controleren | `jq . .claude-plugin/marketplace.json plugins/laposta/.claude-plugin/plugin.json` |
| een wijziging uitproberen | nieuwe Claude-sessie starten; de plugin laadt bij het starten |

## Wat je niet aan de mappen ziet

- **`references/` is gegenereerd, niet met de hand geschreven.** Bewerk je die bestanden los,
  dan is je wijziging weg bij de volgende generatie. Pas `spec/` aan en genereer opnieuw.
- **De taal van de skill is Engels**, omdat hij voor iedereen is en niet alleen voor Nederlandse
  gebruikers. Dat geldt voor `SKILL.md` en voor `references/`.
- **Er staat geen API-sleutel in deze repo en die mag er ook nooit in.** De skill beschrijft hoe
  een gebruiker zijn eigen `LAPOSTA_API_KEY` meegeeft; hij bevat er zelf geen.
- **Deze repo is publiek**, inclusief de commit-historie, de commit-berichten, de PR-titels en
  de reviewopmerkingen. Lees voor je commit je eigen tekst terug met de vraag: kan een
  buitenstaander dit lezen zonder dat het gek staat? Zo niet, herschrijf.

## Werkwijze

1. Werk op een feature-branch; `main` is beschermd, dus altijd via een pull request.
2. Zet in de PR de uitslag van `jq` op beide JSON-bestanden, en als je `SKILL.md` of
   `references/` raakt: één echte vraag aan een verse sessie met de skill geladen, met het
   antwoord erbij. Niet alleen de code gelezen.

Actueel per: 22 september 2026

## Waar de geschiedenis staat

Deze repo had geen open of gesloten pull requests toen hij op 22 september 2026 naar
de organisatie `laposta` ging, dus er is geen archiefrepo naast. De commit-historie is
compleet.
