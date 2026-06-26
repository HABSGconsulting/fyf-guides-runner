# fyf-guides-runner

Public CI/CD runner for the [FYF Guides Engine](https://github.com/HABSGconsulting/fyf-guides-engine) (private).

This repo contains **only workflow files**. No content, no registry, no API keys.
All output (manifests, content, maps) is committed directly into the private engine repo.

## Workflows

| Workflow | Trigger | What it does |
|---|---|---|
| `architect.yml` | Manual | Generates one series manifest + map |
| `architect-batch.yml` | Manual | Generates all approved series manifests in one run |
| `generate.yml` | Manual / Scheduled | Generates content sections via Worker |

## Required Secrets

Set these in this repo's Settings → Secrets and variables → Actions:

| Secret | Purpose |
|---|---|
| `GEMINI_API_KEY` | Google AI Studio API key for Gemini calls |
| `GH_PAT` | GitHub PAT with `repo` scope — used to checkout + push to private engine repo |

## How It Works

Each workflow checks out `HABSGconsulting/fyf-guides-engine` (private) using `GH_PAT`,
runs the relevant script inside it, and commits output back to the private repo.
This runner repo stays permanently empty of content.
