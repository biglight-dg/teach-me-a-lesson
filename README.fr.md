[English](README.md) | [한국어](README.ko.md) | [Español](README.es.md) | **Français** | [中文](README.zh.md) | [日本語](README.ja.md) | [Tiếng Việt](README.vi.md)

# teach-me-a-lesson — une skill de professeur patient et bienveillant pour les débutants en IA et en programmation

Une [skill Claude](https://docs.claude.com/en/docs/claude-code/skills) qui explique Claude, les outils d'IA et les notions de programmation/informatique **comme le ferait un bon professeur pour des grands débutants et des personnes non techniques**, et qui continue à vous aider pendant que vous travaillez.

Au lieu de simplement donner la réponse, elle se concentre sur ce moment de **« ah, *c'était donc ça* ! »** grâce à une seule bonne analogie.

## Ce qu'elle fait

Elle fonctionne en six modes (déclenchés par une simple demande ou par une commande slash).

| Mode | Commande | Ce qu'elle fait |
|------|----------|-----------------|
| **explain** | `/tl-explain <sujet>` | Explique une notion avec des analogies, des tableaux et des points clés (par défaut) |
| **mistake** | `/tl-mistake` | Diagnostique ce qui a mal tourné et pourquoi — sans culpabiliser — et comment corriger |
| **bad-habit** | `/tl-bad-habit` | Repère les mauvaises habitudes récurrentes et propose de meilleures façons de faire |
| **knowledge** | `/tl-knowledge <sujet>` | Enregistre ce que vous venez d'apprendre dans un fichier de connaissances (note markdown) |
| **token** | `/tl-token` | Observe votre façon de travailler et signale le gaspillage de tokens/contexte, avec des solutions concrètes |
| **config** | `/tl-config` | Règle la langue, le niveau de langue, le ton/persona, le niveau d'émojis et la façon de s'adresser à vous |

Tant que la skill est chargée, elle agit aussi comme une **aide toujours présente** : lorsqu'elle voit des actions risquées (coller des commandes inconnues, exposer des clés d'API, opérations irréversibles), des demandes fondées sur un malentendu ou un chemin inefficace, elle le **signale avec douceur** — sans harceler — et vous laisse décider.

> Remarque : l'aide permanente fonctionne tant que la skill est chargée (dans le contexte de la conversation). Ce n'est pas un hook qui vérifie automatiquement chaque saisie.

### Exemples de déclenchement

- « Explique-moi ce qu'est MCP, très simplement — je suis grand débutant »
- « Je confonds toujours API et SDK. Explique la différence avec une analogie »
- « Les terminaux me font peur — dois-je vraiment en utiliser un ? »
- « Je crois que je viens de pousser mon .env sur GitHub — quel est le problème ? » → mistake
- « Signale-moi mes mauvaises habitudes » → bad-habit
- « J'ai l'impression de brûler des tokens — tu peux jeter un œil ? » → token

## Installation

### 1) Copiez le dossier de la skill

```bash
# macOS / Linux
cp -r teach-me-a-lesson ~/.claude/skills/

# Windows (PowerShell)
Copy-Item -Recurse teach-me-a-lesson $env:USERPROFILE\.claude\skills\
```

### 2) Installez les commandes slash (facultatif, pour utiliser /tl-*)

Copiez les fichiers du dossier `commands/` de la skill dans votre dossier de commandes.

```bash
# macOS / Linux
cp teach-me-a-lesson/commands/tl-*.md ~/.claude/commands/

# Windows (PowerShell)
Copy-Item teach-me-a-lesson\commands\tl-*.md $env:USERPROFILE\.claude\commands\
```

La skill se déclenche aussi automatiquement à partir de phrases simples comme « explique-moi ça simplement ». Les commandes ne sont qu'un moyen pratique d'appeler explicitement un mode précis.

## (Facultatif) Connectez vos propres fichiers de connaissances

Si vous avez des **fichiers de connaissances** (un dossier de notes markdown), la skill les utilise comme source principale. Sinon, elle s'appuie sur les connaissances propres de Claude — elle **fonctionne donc très bien sans aucun fichier de connaissances**.

- Dossier de recherche/sauvegarde par défaut : `./knowledge/` dans votre répertoire de travail, ou `~/.claude/teach-me-a-lesson/knowledge/`
- Si vous avez déjà un dossier de notes, pointez simplement vers celui-ci.
- Pour les règles détaillées et le format d'index facultatif, voir `references/knowledge-files.md`.

> Ce dépôt ne contient **aucun** document de connaissances personnel. Seule la méthodologie d'enseignement (la skill elle-même) est publiée.

## Régler le ton et la langue

Vous pouvez ajuster la **langue, le niveau de langue et le style** du professeur à votre goût. Par exemple, en coréen, elle ajuste non seulement le niveau de politesse (존댓말/반말), mais aussi l'**ambiance** (chaleureuse, sobre, enjouée, formelle).

- `/tl-config` — demande tour à tour : langue → niveau de langue → ton/persona → niveau d'émojis → façon de s'adresser à vous, puis enregistre
- Le langage naturel fonctionne aussi — « tutoie-moi et sois enthousiaste », « explique en anglais », « moins d'émojis »
- Les réglages sont enregistrés dans `~/.claude/teach-me-a-lesson/config.json` (un fichier de ton personnel, donc **non** inclus dans la distribution). Sans réglage, elle fonctionne avec les **valeurs par défaut (professeur chaleureux, coréen poli 해요체)**.
- Quel que soit le ton, la qualité de l'enseignement (analogies, sans culpabiliser, sans surcharger, en citant les sources) reste la même. Voir `references/tone-config.md`.

## Structure

```
teach-me-a-lesson/
├── SKILL.md                      # Déclencheurs + 6 modes + aide permanente + config du ton + flux
├── references/
│   ├── teaching-style.md         # Créer des analogies, bons/mauvais exemples, corrections en douceur
│   ├── knowledge-files.md        # Règles de recherche/sauvegarde des fichiers de connaissances (générique)
│   ├── modes.md                  # Les 6 modes en détail + exemples d'aide permanente
│   └── tone-config.md            # Schéma et personas pour langue/niveau/ton/émojis/adresse
├── commands/                     # Commandes slash /tl-* (à copier dans votre dossier de commandes)
├── evals/
│   └── evals.json
├── README.md                     # Anglais (par défaut)
├── README.{ko,es,fr,zh,ja,vi}.md # Traductions (KO/ES/FR/ZH/JA/VI)
└── LICENSE
```

## Licence

Licence MIT. Utilisez, modifiez et redistribuez librement.
