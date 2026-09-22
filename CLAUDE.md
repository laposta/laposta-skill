# CLAUDE.md, laposta-skill: de publieke Laposta-skill en zijn marketplace

Een Agent Skill waarmee een AI-assistent met de Laposta-API kan werken (lijsten, relaties,
velden, segmenten, campagnes, resultaten, webhooks), plus de marketplace-definitie waarmee
Claude Code hem kan installeren. De serverregels (`/srv/laposta-infra/AGENTS.md`) laden vanzelf
en winnen.

## Leesvolgorde, dit is het maximum

1. Dit bestand.
2. `plugins/laposta/skills/laposta/SKILL.md`: de skill zelf. Dat is het bestand dat telt.
3. Alleen de `references/`-pagina die je fix raakt: `endpoints.md`, `schemas.md`, `tasks.md`,
   `errors-and-limits.md`, `pitfalls.md`.

Niet inlezen: de `spec/`-map in zijn geheel (`openapi-en.yml` is groot). Grep erin.

## Wat er draait en waar

Niets. Dit is geen dienst en er is geen deploy. De repo wordt gelezen door Claude Code zelf:

| wat | waar |
| --- | --- |
| marketplace | `.claude-plugin/marketplace.json`, verwijst naar `./plugins/laposta` |
| installatie bij Mees | `~/.claude/settings.json`, `extraKnownMarketplaces` op `laposta/laposta-skill` |
| gegenereerde naslag | `references/` komt uit `scripts/generate-reference.py` plus `spec/` |

## De commando's

| wat | commando |
| --- | --- |
| naslag opnieuw genereren | `python3 scripts/generate-reference.py` |
| controleren dat de JSON klopt | `jq . .claude-plugin/marketplace.json plugins/laposta/.claude-plugin/plugin.json` |
| skill opnieuw laden na een wijziging | nieuwe Claude-sessie starten; de plugin laadt bij het starten |

## Wat je niet aan de mappen ziet

- **Deze repo is PUBLIEK.** Dat is de bedoeling (het is een skill die anderen mogen gebruiken),
  maar het betekent dat álles openbaar is, ook de commit-berichten, de PR-titels en de
  reviewopmerkingen. Zet er nooit interne notities in: geen werkwijze, geen feedbackrondes, geen
  namen van interne repo's, geen accountnummers, geen klantnamen. Dit is een harde regel van
  Mees.
- **De taal is Engels.** `SKILL.md` en de `references/` zijn Engels omdat de skill voor iedereen
  is, niet alleen voor Laposta. De commit-berichten mogen Nederlands zijn (`AGENTS.md` §1), maar
  de PR-titel is ook publiek: houd die neutraal.
- **`references/` is gegenereerd, niet met de hand geschreven.** Bewerk je ze los, dan is je
  wijziging weg bij de volgende generatie. Pas `spec/` aan en genereer opnieuw.
- **Er staat geen API-sleutel in deze repo en die mag er ook nooit in.** De skill beschrijft hoe
  een gebruiker zijn eigen `LAPOSTA_API_KEY` meegeeft; hij bevat er zelf geen.

## Werkwijze per ronde

1. Worktree van `origin/main` (`AGENTS.md` §2). `main` is beschermd, dus altijd een PR.
2. Bewijs in de PR: `jq` schoon op beide JSON-bestanden, en als je `SKILL.md` of `references/`
   raakt, één echte vraag aan een verse sessie met de skill geladen, met het antwoord erbij.
3. Lees je PR-titel en je commit-bericht nog een keer terug met de vraag: kan een buitenstaander
   dit lezen? Zo niet, herschrijf.

## Deze gids actueel houden

Raakt je wijziging de marketplace, de generatie of de manier waarop de skill geladen wordt, werk
dan in dezelfde PR dit bestand bij en zet de regel hieronder op je commitdatum.

Actueel per: 22 september 2026

## Waar de geschiedenis staat

Deze repo is bij de verhuizing naar de organisatie `laposta` op 22 september 2026 opnieuw aangemaakt en had geen open of gesloten pull requests, dus er is geen archiefrepo naast. De commit-historie is compleet.
