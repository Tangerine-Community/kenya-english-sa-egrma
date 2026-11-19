# Kenya Self-Administered EGRA / EGMA (Tangerine content set)

Kenyan adaptation of the Tangerine Self-Administered EGRA/EGMA tools, with item prompts re-recorded in a Kenyan English accent. IDinsight used these instruments to assess early-grade literacy and numeracy in Kenyan schools across baseline, midline and endline rounds (2025–2026).

The content builds on Tangerine's Self-Administered EGRA/EGMA tools. We thank the [Tangerine Community](https://github.com/Tangerine-Community) for making them available. 
> [!NOTE]
> There is an updated version of these forms in Kiswahili, using the built-in radio blocks and tangy prompt inputs.
> - [Mainland](https://github.com/Tangerine-Community/tanzania-mainland-sa-egrma)
> - [Zanzibar](https://github.com/Tangerine-Community/tanzania-zanzibar-sa-egrma)

> [!IMPORTANT]
> These instruments use the **older Tangerine form format with a lot of custom JavaScript** inside each form (section logic, scoring, audio queueing). They are not built with the newer radio blocks used in recent content sets. Expect to read and edit form HTML directly when adapting them.

## What's included

| Form | Notes |
|---|---|
| Letters - Kenyan Version | Baseline letters/reading instrument |
| Letters - Kenyan Version - Midline Version A | Parallel form A |
| Letters - Kenyan Version - Midline Version B | Parallel form B |
| Letters - Kenyan Version - Endline | |
| Numbers - Kenyan Version - Midline Version A | Parallel form A |
| Numbers - Kenyan Version - Midline Version B | Parallel form B (see known issues) |
| Numbers - Kenyan Version - Endline | |

- `client/media/`: the Kenyan-accent audio (`.m4a`) plus the shared Tangerine prompts (`.mp3`). Only files referenced by the forms above are included.
- `client/sounds/`, `client/images/`: shared UI sounds and images from the Tangerine template.
- `client/app-config.defaults.json`: a template config. It has no server URL, group ID or upload token.

## Before you use it

**School lists are placeholders.** The forms ask the enumerator to pick the school, and on endline forms the partner institution first. We replaced our study's school lists with three example schools per list (`EXAMPLE SCHOOL 1–3`, IDs `PC901`, `JF901`, etc.), and the two partner institutions with `Partner A` / `Partner B`. Put in your own sample before fielding:

- `school_select` (midline forms), or `fi`, `school_select_jf` and `school_select_pc` (endline forms): the `<option>` lists
- `var SCHOOL_NAMES = { ... }` in the endline forms' `on-open` logic: the ID → name map that fills `school_name`

**Student identifiers.** The forms collect student first name, last name, grade, gender and a register line number. Review this against your own consent and data-protection requirements and remove fields you don't need.

## Installation

Tested on **Tangerine v3.32.0**.

1. Copy this repository into a folder under your Tangerine install's `content-sets` directory, for example `tangerine/content-sets/kenya-sa-egrma`.
2. Open a shell in the container and create a group from it:
   ```bash
   docker exec -it tangerine bash
   create-group "Kenya SA-EGRMA" kenya-sa-egrma
   ```
3. In the new group's app config, set `serverUrl`, `uploadToken` and anything else specific to your deployment. Compare with `client/app-config.defaults.json`. The defaults turn on kiosk mode and return to the home screen after each form.
4. Build an APK from the group and install it on the tablets.

See the Tangerine docs on [content sets](https://docs.tangerinecentral.org/editor/advanced-form-programming/content-sets/#creating-a-new-content-set) and [app configuration](https://docs.tangerinecentral.org/editor/advanced-form-programming/configuration/#configuration) for details.

## Known issues

- **Numbers - Midline Version B** refers to `Q1.m4a`, `Q2.m4a` and `Q3.m4a`, which are not in `media/`. These were not on our production server either, so those three prompts play no audio. Record them or remove the references before using that form.
- We corrected one broken reference in the Numbers Midline A and Endline forms: `math_6-forty-five.mp3` now points to the existing file `math_6-forty_five.mp3`.

## Contact

IDinsight, [idinsight.org](https://www.idinsight.org)
