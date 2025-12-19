# FiftyOne Skills

<div align="center">
<p align="center">

<!-- prettier-ignore -->
<img src="https://user-images.githubusercontent.com/25985824/106288517-2422e000-6216-11eb-871d-26ad2e7b1e59.png" height="55px"> &nbsp;
<img src="https://user-images.githubusercontent.com/25985824/106288518-24bb7680-6216-11eb-8f10-60052c519586.png" height="50px">

</p>
</div>

> Control FiftyOne datasets through AI assistants using SKILLS

## Overview

FiftyOne provides a powerful [MCP server](https://github.com/AdonaiVera/fiftyone-mcp-server) that allows AI assistants to interact with your computer vision datasets. Skills extend this functionality by packaging expert workflows that AI assistants can follow autonomously.

With skills, you can teach your AI assistant to find duplicates, evaluate models, and explore datasets using natural language—all powered by FiftyOne's operator framework.

## Installation

As simple as:

```shell
pip install fiftyone
```

Then install the [FiftyOne MCP Server](https://github.com/AdonaiVera/fiftyone-mcp-server):

```shell
git clone https://github.com/AdonaiVera/fiftyone-mcp-server.git
cd fiftyone-mcp-server
poetry install
```

Configure the MCP server in your AI assistant (Claude, ChatGPT, etc.) and install the skills plugin.

## Available Skills

<table>
    <tr>
        <th>Skill</th>
        <th>Description</th>
    </tr>
    <tr>
        <td><b><a href="find-duplicates/skills/fiftyone-find-duplicates/SKILL.md">Find Duplicates</a></b></td>
        <td>Find and remove duplicate or near-duplicate images using brain similarity computation</td>
    </tr>
    <tr>
        <td><b><a href="dataset-inference/skills/fiftyone-dataset-inference/SKILL.md">Dataset Inference</a></b></td>
        <td>Create datasets from local directories, import labels (COCO, YOLO, VOC), and run model inference</td>
    </tr>
</table>

## Quick Start

### Install Claude Code

Download [Claude Code](https://claude.com/product/claude-code) desktop app.

### Register Skills Marketplace

In Claude Code chat:

```
/plugin marketplace add AdonaiVera/fiftyone-skills
```

### Install a Skill

```
/plugin install fiftyone-find-duplicates@fiftyone-skills
```

### Use the Skill

```
Use the FiftyOne find duplicates skill to remove redundant images from my quickstart dataset
```

Claude will automatically:
1. Load the skill instructions
2. Set the dataset context
3. Launch the FiftyOne App
4. Compute similarity embeddings
5. Find and remove duplicates
6. Clean up and report results

## How Skills Work

Skills are workflow packages that orchestrate FiftyOne MCP server tools:

**FiftyOne MCP Server** provides 16 low-level tools:
- Dataset management (list, load, summarize)
- Operator execution (80+ FiftyOne operators)
- Plugin management (install, enable, discover)
- Session control (launch/close App)

**FiftyOne Skills** provide high-level workflows:
- Step-by-step instructions
- Key directives (ALWAYS/NEVER rules)
- Concrete examples
- Troubleshooting guidance

When you mention a skill, your AI assistant loads the `SKILL.md` instructions and uses MCP tools to complete the task autonomously.

## Skill Architecture

Each skill is a single markdown file with YAML frontmatter:

```
find-duplicates/
├── plugin.json
└── skills/
    └── fiftyone-find-duplicates/
        └── SKILL.md          # Complete workflow instructions
```

**SKILL.md structure:**

```markdown
---
name: skill-name
description: When to use this skill
---

# Overview
What this skill does

# Prerequisites
Required setup

# Key Directives
ALWAYS/NEVER rules for AI

# Workflow
Step-by-step instructions

# Examples
Concrete use cases
```

## Integration with FiftyOne

Skills assume the FiftyOne MCP server provides these tools:

**Dataset Tools:**
- `list_datasets`, `load_dataset`, `get_dataset_summary`

**Operator Tools:**
- `set_context`, `list_operators`, `get_operator_schema`, `execute_operator`

**Plugin Tools:**
- `list_plugins`, `download_plugin`, `enable_plugin`

**Session Tools:**
- `launch_app`, `close_app`, `get_session_info`

Skills orchestrate these tools into complete workflows.

## Contributing Your Own Skill

Want to create a custom skill?

1. Copy the `find-duplicates` folder and rename it
2. Update `SKILL.md` frontmatter with name and description
3. Write workflow instructions following FiftyOne patterns
4. Update `.claude-plugin/marketplace.json`
5. Test with your AI assistant

See the [find-duplicates SKILL.md](find-duplicates/skills/fiftyone-find-duplicates/SKILL.md) for a complete example.

## Installation Options

### Claude Code

**Prerequisites:** [Claude Code](https://claude.com/product/claude-code) desktop app

Register marketplace (in Claude Code chat):
```
/plugin marketplace add voxel51/fiftyone-skills
```

Install skill:
```
/plugin install fiftyone-find-duplicates@fiftyone-skills
```

### Codex

Codex identifies skills via `AGENTS.md`. Verify:

```bash
codex --ask-for-approval never "Summarize the current instructions."
```

### Gemini CLI

Install locally:

```bash
gemini extensions install . --consent
```

Or via GitHub:

```bash
gemini extensions install https://github.com/voxel51/fiftyone-skills.git --consent
```

## Resources

- **Website**: https://fiftyone.ai
- **Documentation**: https://docs.voxel51.com
- **FiftyOne MCP Server**: https://github.com/AdonaiVera/fiftyone-mcp-server
- **FiftyOne Plugins**: https://github.com/voxel51/fiftyone-plugins
- **Claude Code Docs**: https://code.claude.com/docs/en/skills
- **Community**: https://discord.gg/fiftyone-community

## License

Apache 2.0 - See [LICENSE](LICENSE) for details

Copyright 2017-2025, Voxel51, Inc.
