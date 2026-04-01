# Claude Jimeng Skills

> Claude Code skill for Dreamina (Jimeng) image and video generation via CLI.

---

## What Is This?

A Claude Code skill that enables AI agents to generate images and videos using [Dreamina](https://www.capcut.com/ai-tool/dreamina) (also known as Jimeng / Ji Meng in Chinese) through a local CLI tool called `dreamina`.

## Features

- **Image Generation**: Text-to-image and image-to-image workflows
- **Video Generation**: Text-to-video, image-to-video, multi-frame-to-video, and multimodal-to-video (SeedDance 2.0 family)
- **Account Management**: Login session reuse, credit checking
- **Async Task Management**: Submit, query results, list history
- **Agent-Friendly**: Designed for AI agents to operate autonomously with proper guardrails

## Skill File

The [`SKILL.md`](SKILL.md) file is a Claude Code skill definition that teaches the agent how to properly use the `dreamina` CLI. Drop it into your project or reference it in your Claude Code configuration.

### Key Behaviors the Skill Teaches

1. **Always check help first**: `dreamina -h` and `dreamina <subcommand> -h` before any real command
2. **Credit awareness**: Check `user_credit` before expensive operations
3. **Async workflow**: Submit returns a `submit_id`; use `query_result` for follow-up
4. **Model selection**: Don't hardcode -- always verify model support via subcommand help
5. **Success validation**: Don't trust exit codes alone; check `gen_status` and `fail_reason`
6. **Batch discipline**: Small, reviewable batches for real generation tasks

## Available Commands

| Command | Purpose |
|---------|---------|
| `dreamina user_credit` | Check remaining credits |
| `dreamina query_result --submit_id=<id>` | Query async task result |
| `dreamina list_task` | Review saved task history |
| Image commands | Text-to-image, image-to-image generation |
| Video commands | Text-to-video, image-to-video generation |
| `dreamina image2video` | Single image to video |
| `dreamina multiframe2video` | Multiple images to coherent story video |
| `dreamina multimodal2video` | Flagship mode: images + video + audio references (SeedDance 2.0) |

## Usage

### As a Claude Code Skill

Place `SKILL.md` where Claude Code can find it (project root or skills directory).

### Choosing the Right Command

- **Budget check**: `user_credit`
- **Have a submit_id**: `query_result`
- **Review history**: `list_task`
- **Output is image**: Use image commands
- **Output is video, one reference image**: `image2video`
- **Output is video, multiple images for a story**: `multiframe2video`
- **Output is video, needs all-around references**: `multimodal2video` (SeedDance 2.0)

### Important Notes

- Some generation commands are **asynchronous** -- submit and query are separate steps
- Some models may require a one-time web authorization. If the CLI returns `AigcComplianceConfirmationRequired`, complete the web-side confirmation first
- Different commands support different models, ratios, durations, and resolutions -- always check each subcommand's `-h`
- SeedDance 2.0 family models can be capacity-constrained; don't default to them unless quality is explicitly prioritized over speed

## License

MIT
