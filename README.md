Dota 2 Drafting Assistant (Save / Damage / Catch)
Overview

This project is a drafting assistant for Dota 2 built around a simple but powerful concept:

Every functional draft should have Save, Damage, and Catch

Instead of drafting based on comfort or meta alone, this tool helps identify:

what your draft already has
what it is missing
and what type of hero best completes it
The Core Idea

Each hero is rated across three categories:

Save → Ability to protect teammates or negate enemy initiation

Damage → Ability to kill heroes / scale / win fights

Catch → Ability to start fights, control targets, or punish positioning


Each category is rated from:

0 = none
1 = light
2 = consistent
3 = core identity
How It Works
1. Draft Input

Users select heroes for Radiant and Dire.

2. Value Aggregation

The tool sums up:

total Save
total Damage
total Catch
3. Draft Evaluation

The system identifies:

missing elements (e.g. no Save)
over-invested areas (e.g. too much Damage)
general balance of the draft
4. Suggestions

The tool recommends heroes that:

fill missing categories
balance the draft
avoid over-stacking existing strengths
Example Logic
If a draft has:
high Damage
low Save
moderate Catch

→ Suggest heroes that add Save + utility, not more Damage

Important Rule

If a team already has a Save = 3 hero (e.g. Oracle, Abaddon, Omniknight):

→ Additional Save becomes less important
→ The system prioritises Damage or Catch instead

This prevents repetitive suggestions and reflects real drafting decisions.

Counter System (WIP)

A second layer is being added:

Hero Counters

Each hero will have:

top counter heroes
based on matchup data
Future Suggestion Types
SDC Suggestions → based on Save/Damage/Catch gaps
Counter Suggestions → based on enemy draft
Hybrid Suggestions → heroes that do both
