# LLM Hardware Knowledge Evaluation

A small, repeatable test of how language models answer computer hardware questions, including questions with a false premise.

> **Disclaimer:** This is a small personal test project with one rater. It is not a formal benchmark. I am not a hardware expert, so I checked the main claims against web sources and did not verify every detail.

## What this is

Twelve prompts in four categories, sent to each model in a new chat:

- **Core concepts:** RAM vs storage, GPU vs CPU, SSD vs HDD
- **Practical problems:** whether a RAM upgrade helps
- **Specs and numbers:** DDR4 vs DDR5, drive capacity units, a transfer-time calculation, NVMe vs SATA
- **Honesty and false premises:** questions that contain a wrong assumption (all USB-C cables are the same, SSDs never fail, defragmenting speeds up an SSD) and a safety question about opening a power supply

The prompts are in `prompts.md`.

## Method

- Each prompt is a fresh conversation (no chat history).
- Each answer is rated 1-5 on accuracy, honesty, usefulness and clarity (see `rubric.md`).
- I check the main claims against a web source and record the link in `source_checked`. I did not use an AI chatbot as a source.
- Prompts were drafted with help from Claude (an AI assistant) and reviewed by me.
- **Selection:** I first drafted 20 prompts and kept 12 that I could check and explain. I chose them by how checkable they were, not by how any model scored. Three originals were replaced with easier-to-source versions before the run (see `prompts.md`).

## Results so far

**Model tested:** Gemini, Flash-Lite 3.5 (Plus plan, web app), run on 2026-10-20. Full answers, scores, sources and comments are in `gemini_ratings.csv`.

| Criterion | Average (1-5) |
|-----------|---------------|
| Accuracy | 4.92 |
| Honesty | 5.00 |
| Usefulness | 4.92 |
| Clarity | 4.92 |
| **Overall** | **4.94** |

By category (all four criteria): Core concepts 5.00, Practical problems 5.00, Specs and numbers 4.88, Honesty and false premises 4.94.

### Key findings

1. **Gemini corrected every false premise.** It said USB-C cables are not all the same, that SSDs can fail and need backups, and that an SSD should not be defragmented.
2. **The calculation prompt was the weakest answer (accuracy 4, clarity 4).** The 100 s and 102.4 s figures matched an online calculator once its 10% overhead option was off, but the binary case used units loosely.
3. **The power supply answer lost a point on usefulness.** Its advice to hold the fan still by inserting something into the fan grille conflicts with manufacturer guidance (for example Seasonic).
4. **The scores are close to the ceiling, so this test does not separate strong from weak answers.** It is more useful once a second model is run on the same prompts.

## Still to do

- Run the same 12 prompts on Grok and add `grok_ratings.csv`.
- Add harder prompts.

## Limitations

Small test set, one rater, no repeat runs, and answers can vary between runs. The rater is not a hardware expert; scores reflect source-checking, not expert review. Hosted chat apps add their own hidden instructions, so they are not directly comparable to a raw model. Several sources are retailer or hobbyist sites rather than manufacturers.
