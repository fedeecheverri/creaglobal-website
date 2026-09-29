# CREA Global website — brand rules for Claude Code

This repo is the CREA Global website (`/` = current site, `/concept-abra/` = editorial concept). Every change must match the CREA brand system that the Word and PowerPoint templates already follow. When a rule here conflicts with existing code, the rule wins. When a rule conflicts with something the user asks, ask before acting.

## Sources of truth (read before large changes)

All in `~/Library/CloudStorage/OneDrive-Personal/CREA OneDrive/CREA Marca/Manual de Marca CREA/`:

- `CREA_Manual_de_Marca_Concepto1_1.pdf` — brand manual (colors, type, logo, labyrinth, applications).
- `CREA_Arquetipos_Marca.docx` — archetypes, sequence, voice by channel, usage rules.
- `Plantillas/CREA_Plantilla_Propuesta_Comercial.docx` and `Plantillas/CREA_Plantilla_Presentacion_Comercial.pptx` — the web must look and read like these.
- `Logos CREA/` — official logos. Use the PNGs with transparent backgrounds. The `.svg` files in that folder are empty shells; never use them.

Exception to the manual: **"Lo hacemos pasar." is retired** (another company uses it). The manual PDF still shows it; ignore it there.

## Brand logic: two archetypes, fixed order

CREA always communicates **authority first, relationship second**. Never the reverse.

| | Experto integrado (authority) | Socio operativo (relationship) |
|---|---|---|
| Promise | «Hemos estado ahí. Sabemos cómo funciona.» | «El proyecto es nuestro hasta que termina.» |
| On the web | Hero, experience, figures, cities, clients | Method, team, contact, closing |
| Visual voice | onyx, hueso, Poppins, data, austerity | bronce, champagne, Lora, labyrinth, warmth |

Page order must follow that sequence: facts (projects, figures, cities) before promises (method, ownership, contact).

## Design tokens (exact values, no others)

```css
:root {
  /* brand */
  --onyx: #141416;       /* authority: dark sections, text, positive logo */
  --hueso: #F2EEE7;      /* warm base: light sections */
  --bronce: #B98B5E;     /* accent: eyebrows, section numbers, labyrinth, key rules */
  --champagne: #E2C49A;  /* highlight: figures and quotes ON ONYX ONLY */
  --papel: #FFFFFF;      /* only if a white surface is truly needed */
  /* text on hueso */
  --ink: #1A1A1C;        /* titles */
  --body: #3A3733;       /* body copy */
  --ink-2: #55524C;      /* secondary */
  --muted: #6E6A64;      /* captions, footer — lightest allowed for text */
  --rule: #DAD3C7;       /* hairlines */
  /* text on onyx */
  --body-dark: #C9C3B8;
  --muted-dark: #8C877E;
  --rule-dark: #2B2B30;
}
```

- **Delete `--orange` (#F28C38)** and every use of it (CTAs, buttons, header). It is from the old identity.
- Color proportion is roughly onyx 60 · hueso 28 · bronce 9 · champagne 3. Bronce and champagne never dominate a section.
- `champagne` never on hueso or white (1.4:1, invisible).
- `bronce` on hueso is only 2.6:1: use it only for short UPPERCASE labels with wide tracking, never for reading text or buttons with light text. White on bronce (3.0:1) also fails.
- Text contrast minimum 4.5:1 (3:1 at 24px+). Semi-transparent hueso text on onyx (`rgba(242,238,231,.45)` etc.) must be replaced by `--body-dark` or `--muted-dark`.
- No gradients, no drop shadows, no textures, no colored top/left border accents on cards. **Exception**: an onyx-based overlay/gradient scrim over a photo, whose only purpose is text legibility, is allowed. Decorative gradients (ambient glows, colored backgrounds) stay banned.

## Typography

Load from Google Fonts: **Poppins 300, 400, 500** and **Lora 400, 400 italic**. Nothing else.

- **Remove Bebas Neue entirely.** Headlines go in Poppins Light 300, sentence case, never all caps, never bold.
- Poppins = titles, labels, navigation, buttons, figures. Lora = paragraphs, descriptions, quotes.
- No weight above 500 anywhere.

| Style | Spec (desktop) |
|---|---|
| Display / H1 | Poppins 300, 56–72px, line-height 1.05, letter-spacing −0.01em |
| H2 | Poppins 300, 36–40px, line-height 1.1 |
| Eyebrow | Poppins 500, 11–12px, UPPERCASE, letter-spacing 0.32em, `--bronce` |
| Section number | Poppins 300, 17px, letter-spacing 0.2em, `--bronce` (e.g. `01`) |
| Descriptor | Poppins 400, 13px, UPPERCASE, letter-spacing 0.28em |
| Body | Lora 400, 17–18px, line-height 1.55, `--body` |
| Quote | Lora 400, 22–26px, line-height 1.5, «comillas latinas» |
| Caption / footer | Poppins 400, 11px, UPPERCASE, letter-spacing 0.16em, `--muted` |
| Large figures (stats, hero numbers) | Poppins 300, large, `--champagne` on onyx / `--ink` on hueso |
| Inline data in text | Poppins 500, tracking 0.05em (manual p.9) |

Any UPPERCASE text needs wide tracking (0.16–0.32em). Left-align body text; no justified text.

## Logo

- Horizontal lockup (isotipo + CREA + GLOBAL) is the main mark. Positive (onyx) on light backgrounds, negative (hueso) on dark. No other colors.
- Use transparent PNGs. **Fix `concept-abra`: the logo disappears on scroll.** `logo-white-new.jpg` is hidden via `content: none` in `.navbar.scrolled .logo img` (concept-abra/style.css) once the header goes light, leaving no logo at all. Swap to the correct positive/negative PNG depending on header state instead of hiding it.
- Minimum width 150px; below that use the isotipo alone. Clear space = height of the "C" of the wordmark.
- Isotipo: favicon, avatar, and watermark at 5% opacity (bottom-right). The labyrinth is never a watermark.
- Never stretch, rotate, recolor, add effects, or separate "GLOBAL" from the name.

## Shape and layout

- Square corners everywhere (`border-radius: 0`) on cards, buttons, images, inputs. The only rounded shape allowed is the pill tag for archetype labels.
- Team photos: square black-and-white crops, not circles.
- Structure sections as in the templates: section number → eyebrow → H2 → content, separated by `--rule` hairlines, generous whitespace.
- Primary button: `--onyx` background + `--hueso` text on light sections; `--hueso` background + `--onyx` text on dark sections. Secondary: 1px border, no fill.
- The WhatsApp button keeps its function but follows the brand buttons (no WhatsApp green block).
- Labyrinth (bronce on onyx) only in relationship contexts: contact section or closing band. There is no standalone file yet; ask the user before recreating it.
- Footer: `CREA GLOBAL` left, `DE LA IDEA AL RESULTADO` right, as in the slides.

## Phrases

| Status | Phrase | Rule |
|---|---|---|
| Official | **DE LA IDEA AL RESULTADO** | Descriptor. Poppins 400, UPPERCASE, tracking 0.28em. Use in hero, `<title>` and footer. Never on the same line as another slogan. |
| Official | «Hemos estado ahí. Sabemos cómo funciona.» | Hero headline. |
| Official | «El proyecto es nuestro hasta que termina.» | Method / relationship section. |
| **Retired** | Lo hacemos pasar. | Do not use anywhere. |
| **Retired (same claim)** | Hacemos que las cosas pasen. | Too close to the retired phrase. Remove from hero H1, footer and meta. |
| **Replaced** | Estrategia. Ejecución. Resultados. | Replace with the descriptor, including `<title>`. |

Do not invent a new slogan. If the hero needs a headline, use a fact-based line approved by the user; propose options, do not ship one.

**There is currently no emotional closer phrase.** With "Lo hacemos pasar." retired and "Hacemos que las cosas pasen." too close to it, the site has no Lora-italic closing line right now. Do not reuse either retired phrase and do not invent a replacement — leave the closer slot as a TODO for the user, or use only the official descriptor/promise phrases above.

## Voice

- Formal "usted", Spanish (Colombia). No exclamation marks, no emojis, no filler adjectives.
- Verbs that execute: **coordinar, ejecutar, entregar, responder, garantizar.**
- Banned provider verbs: **acompañar, apoyar, facilitar, potenciar.** Current offenders: "CREA acompañó a los representantes de Juan Valdez", "Le acompañamos en la identificación de mercados". Also avoid "asesoramos": it contradicts «No asesoramos sobre lo que otros hacen — nosotros lo hemos hecho.»
- Every capability claim carries a concrete fact (project, city, figure, entity).
- Credential line format: `SHANGHÁI · MILÁN · DUBÁI · OSAKA · COP16`.

## Facts: keep consistent with the templates

- Currency: `US$` (e.g. `+US$100M`), `COP$`. Thousands with a point (15.000), decimals with a comma (1,6 millones).
- Accents: Shanghái, Dubái, Milán.
- Figures in use: +US$100M structured and managed · 4 Expos BIE (Shanghái, Milán, Dubái, Osaka) · +US$15M in fund-raising · +250 entities · COP16: 15.000+ delegates from 170 countries, 1.001.607 Zona Verde visitors · Dubái: 1,6M+ visitors, 72 partners, 450+ business meetings.
- **Resolved**: use **ICARRD+20** sitewide (the templates' "CIRADR+20" is not used on the web).
- Never invent or round up figures, clients, dates, or quotes. If a figure is missing, leave a visible TODO and tell the user.
- **Confirmed facts** (approved by the user; not in the proposal template, but do not flag again): COP16 lema "Paz con la Naturaleza"; Día Mundial de las Ciudades 2025 (ONU-Hábitat, Bogotá); Misión Comercial — Cámara de Comercio de Cali, Japón 2025; Misión Comercial y Académica — Politécnico Grancolombiano, Japón 2025; Misión Comercial y Diplomática — Alcaldía de Cali, World Cities Summit Singapur 2026; Juan Valdez/Procafecol commercial presence at Expo Osaka 2025, including Typica and "más de 40 países".

## Checks before finishing any change

1. `grep -rniE "F28C38|--orange|Bebas|Lo hacemos pasar|Hacemos que las cosas pasen|Estrategia\. Ejecuci" .` returns nothing outside this file.
2. `grep -rniE "acompa[ñn]|apoyamos|facilit|potenci|asesoramos" .` → rewrite any hit in site copy (ask if unsure).
3. No hex colors outside `:root`.
4. Contrast checked for every text/background pair you touched (4.5:1).
5. Check at 375px and 1440px widths; no horizontal scroll.
6. Both `/` and `/concept-abra/` stay working unless the user says to drop one.
7. Summarize to the user what changed, and list any copy you propose but did not ship.
