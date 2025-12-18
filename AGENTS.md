# FiftyOne Skills - Agent Instructions

This repository contains skills for computer vision workflows using FiftyOne and the FiftyOne MCP Server.

## Available Skills

### FiftyOne Find Duplicates (`find-duplicates/`)

**When to use:** User wants to find duplicate images, remove redundant samples, find similar images, or deduplicate a dataset.

**Instructions:** Load the skill file at `find-duplicates/skills/fiftyone-find-duplicates/SKILL.md`

**Key requirements:**
- FiftyOne MCP server must be running
- `@voxel51/brain` plugin must be installed
- FiftyOne App must be launched before using brain operators

**Workflow summary:**
1. Set context with dataset name
2. Launch FiftyOne App
3. Compute similarity embeddings
4. Find duplicates with threshold
5. Review and delete duplicates
6. Close app

## Prerequisites

All skills require:

1. **FiftyOne MCP Server** installed and configured
   - Repository: https://github.com/AdonaiVera/fiftyone-mcp-server
   - Must be running and accessible

2. **FiftyOne** installed
   - Install: `pip install fiftyone`

3. **Required plugins** installed via FiftyOne
   - `@voxel51/brain` - For similarity and duplicates
   - `@voxel51/utils` - For dataset operations

## Integration

Skills work alongside the FiftyOne MCP Server:

- **MCP Server provides tools** - Low-level operations (list_datasets, execute_operator, etc.)
- **Skills provide workflows** - High-level guidance on how to use the tools

When a skill is active, use the FiftyOne MCP server tools to complete the workflow as described in the skill's SKILL.md file.

## General Workflow Pattern

Most FiftyOne skills follow this pattern:

1. Set context with `set_context` tool
2. Launch app with `launch_app` (for delegated operators)
3. Execute operators with `execute_operator`
4. Review results with `get_dataset_summary`
5. Close app with `close_app`

## Important Notes

- Delegated operators (brain, evaluation) require FiftyOne App to be running
- Always call `launch_app()` before using brain operators
- Wait 5-10 seconds after launching app before executing operators
- Close app with `close_app()` when workflow is complete

## Troubleshooting

**"No executor available" error:**
- Solution: Call `launch_app()` and wait for initialization

**"Operator not found" error:**
- Solution: Install and enable the required plugin

**"Context not set" error:**
- Solution: Call `set_context(dataset_name="...")` first

## Resources

- [FiftyOne Documentation](https://docs.voxel51.com)
- [FiftyOne MCP Server](https://github.com/AdonaiVera/fiftyone-mcp-server)
- [FiftyOne Plugins](https://github.com/voxel51/fiftyone-plugins)
