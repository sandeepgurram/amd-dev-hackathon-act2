# AMD Developer Hackathon: ACT II Reference

Date captured: 2026-07-06

This document consolidates the official participant guide PDF and the public hackathon page into a single working reference for Track 1 planning and implementation.

## Sources

- Participant Guide PDF: [Participant Guide_ AMD Developer Hackathon (ACT II).pdf](Participant%20Guide_%20AMD%20Developer%20Hackathon%20%28ACT%20II%29.pdf)
- Public hackathon page: [AMD Developer Hackathon: ACT II](https://lablab.ai/ai-hackathons/amd-developer-hackathon-act-ii)

## Public Announcement Notes

- Participant Guide is live.
- The guide points participants to the full PDF for exact I/O formats, environment variables, and scoring details.
- GPU access link: [AMD Developer Cloud notebooks](https://notebooks.amd.com/hackathon)
- Questions are directed to the event Discord channel.

## Launch Email Notes

- Email headline: the hackathon kicks off today.
- Email headline prize pool: `$20,000+`.
- Kick-off stream:
  - `6:00 PM CET` goes live.
  - `7:00 PM CET` Discord Q&A session on the LabLab Discord server.
- The stream covers:
  - challenge overview
  - judging criteria
  - all three tracks
  - available tools and credits
- New AMD AI Developer Program members may claim:
  - `1 Month DeepLearning.AI Pro`
  - `$100 AMD Developer Cloud Credits`
  - `$50 Fireworks AI API Credits`
- Bonus challenge:
  - Best Use of Gemma 4
  - `$6k` prize pool
  - open across all hackathon tracks
- The email also promotes the Natively AI Challenge and Native.builder.

## Hackathon Overview

- Event name: AMD Developer Hackathon: ACT II
- Platform: lablab.ai
- Theme: build AI agents and high-performance AI apps on AMD GPUs in the cloud
- Core stack:
  - AMD Developer Cloud
  - ROCm
  - Fireworks AI API
- Submission format: all submissions must be containerized

## Participation and Access

- To participate, you must sign up with AMD and register for the AMD AI Developer Program.
- The hackathon is online on the lablab.ai platform.
- The public page states:
  - Registration is eligible until 8:00 PM CET on the closing day.
  - Registrations after that are not eligible for the hackathon.
  - Registration before July 2 gets hackathon credits on day one.
  - Late sign-ups still can join, but hackathon credits are allocated from July 7 onward.
- Credit structure is separate:
  - Hackathon credits: all participants receive $50 in Fireworks AI API credits.
  - New AMD AI Developer Program sign-ups may also receive:
    - $100 AMD Developer Cloud credits
    - $50 Fireworks AI API credits
  - The new-member credits are subject to a separate manual approval process.

## Track 1

### Official Track Name

- PDF title: `Track 1: General-Purpose AI Agent`
- Public page title: `Track 1 - Hybrid Token-Efficient Routing Agent`

These appear to describe the same challenge. The working intent is the same:
build a token-efficient AI agent that can route tasks intelligently between local and remote inference.

### What You Are Building

- An AI agent that handles a wide variety of natural-language tasks across multiple capability domains.
- The agent must complete a fixed set of tasks autonomously.
- It should decide in real time whether to:
  - use a local model, or
  - call a remote model via Fireworks AI credits
- The main objective is to choose the cheapest option while staying above the accuracy threshold.

### Evaluation Scope

The participant guide says Track 1 is evaluated across eight categories:

1. Factual knowledge
2. Mathematical reasoning
3. Sentiment classification
4. Text summarisation
5. Named entity recognition
6. Code debugging
7. Logical / deductive reasoning
8. Code generation

### Allowed Models

The announcement lists these Track 1 models:

- `minimax-m3`
- `kimi-k2p7-code`
- `gemma-4-31b-it`
- `gemma-4-26b-a4b-it`
- `gemma-4-31b-it-nvfp4`

### Track 1 Build Guidance

- Build for generality, not for a known benchmark prompt set.
- Do not hardcode answers.
- Use routing intelligence, not raw compute, to minimize token usage.
- Prompt-based and fine-tuned routing approaches are judged the same way.
- Local evaluation is recommended before submitting.
- Local models and local token use count as zero toward the final score.
- The final scoring environment is standardized, so the agent must work within those constraints.

## Track 2

### Video Captioning Agent

- Build an agent that captions video clips in four styles:
  - formal
  - sarcastic
  - humorous-tech
  - humorous-non-tech
- Submit a Docker image.
- Any model or API may be used.
- There are no model restrictions for this track.
- Scoring is based on caption accuracy plus style match.

## Track 3

### Unicorn Track

- This is the open-innovation track.
- There is no fixed task.
- The goal is to build the most innovative, technically impressive project using AMD compute.
- Submission requires:
  - GitHub repository
  - demo video
  - slide deck
- Evaluation uses automated pre-screening plus human judges.

## Track 1 Submission Contract

Your container must:

1. Read tasks from `/input/tasks.json` on startup.
2. Write results to `/output/results.json` before exiting.

### Example Input Shape

```json
[
  {
    "task_id": "t1",
    "prompt": "Summarise the following text in one sentence: ..."
  },
  {
    "task_id": "t2",
    "prompt": "..."
  }
]
```

### Example Output Shape

```json
[
  {
    "task_id": "t1",
    "answer": "..."
  },
  {
    "task_id": "t2",
    "answer": "..."
  }
]
```

### Track 1 Runtime and Environment

- All API calls must go through `FIREWORKS_BASE_URL`.
- Do not use your own Fireworks key; use the provided `FIREWORKS_API_KEY`.
- Do not hardcode model IDs; read them from `ALLOWED_MODELS` at runtime.
- Only models listed in `ALLOWED_MODELS` are permitted.
- Calls to other models invalidate the submission.
- The guide says exact evaluation inputs are intentionally omitted.
- Do not cache answers to specific inputs.
- All inference must go through Fireworks AI via `FIREWORKS_BASE_URL`.

### Track 1 Rules

- Exit code must be `0` on success.
- Maximum runtime: 10 minutes.
- `/output/results.json` must be valid JSON.
- Image compressed size must not exceed 10 GB.
- Submissions are rate-limited to 10 per hour per team.
- The container image must be publicly pullable at submission time.
- The image must include a `linux/amd64` manifest.

## Track 1 Scoring

Track 1 is scored in two phases:

1. Accuracy gate
   - LLM-Judge checks whether each answer matches the expected intent.
   - Submissions below the threshold are excluded from the leaderboard.
2. Token efficiency
   - Among submissions that pass accuracy, ranking is by total tokens recorded by the judging proxy.
   - Fewer tokens is better.

## Cross-Track Rules

These apply to all tracks unless otherwise noted:

- Container must start and be ready within 60 seconds.
- Response time per request must be under 30 seconds.
- All responses must be in English.
- Do not hardcode or cache answers to specific inputs.
- Container images must be publicly pullable at submission time.

## Prizes

### Overall Prize Pool

- Total prize pool: $21,000

### Track 1 Prize Breakdown

- 1st place: $2,500
- 2nd place: $1,500
- 3rd place: $1,000

### Partner Reward

- Google DeepMind Gemma prize pool: $6,000 total
- Track 1 Gemma reward:
  - Best Use of Gemma via Fireworks
  - Prize: $1,000

### Referral Program

- Referral prize pool: $1,000
- Top referrer: $250 cash + $250 Natively credits
- 2nd referrer: $150 cash + $150 Natively credits
- 3rd referrer: $100 cash + $100 Natively credits
- Minimum threshold to qualify: refer at least 100 approved participants

## Useful Planning Notes

- The guide is intentionally designed to prevent hardcoding.
- The hidden evaluation set means you should build a general-purpose router, not a prompt-specific shortcut.
- Because local tokens count as zero, a reasonable strategy is:
  - use a lightweight local decision layer for routing,
  - call Fireworks only when the task needs stronger reasoning,
  - keep remote calls sparse and targeted.
- If you later build an evaluation harness, make sure it mirrors:
  - `/input/tasks.json`
  - `/output/results.json`
  - runtime limit
  - allowed-model constraint
  - standardized environment assumptions

## Open Questions to Verify Before Implementation

- Whether the live evaluation container expects any additional metadata beyond `task_id` and `answer`.
- Whether the submitted image should include a fixed entrypoint, shell wrapper, or both.
- Which specific model IDs are published in `ALLOWED_MODELS` on launch day.
- Whether the event page has any final-day schedule changes after the date captured here.
