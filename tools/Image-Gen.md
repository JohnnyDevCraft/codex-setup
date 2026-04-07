# Image Gen

## Name

Image Gen

## Category

Local Console

## URL

- OpenAI Images API: [platform.openai.com/docs/guides/images](https://platform.openai.com/docs/guides/images)
- Local skill reference: `/Users/john/.codex/skills/imagegen/SKILL.md`

## Tool Description

Image Gen is the shared local-console image generation setup used across projects to create and edit images through the OpenAI Images API.

It is intended to give agents and users a repeatable workflow for generating project assets such as concept art, mockups, logos, hero images, illustrations, UI imagery, textures, and edited image variants without rebuilding the environment from scratch for each project.

The current local setup uses:

- Homebrew-managed Python
- Conda for environment management
- A dedicated `codex-imagegen` environment
- The OpenAI Python SDK for API access
- Pillow for image handling

This tool is the standard path when a project needs AI-generated bitmap assets.

## Primary Use Cases

- Generate new project images from prompts
- Edit existing images using the OpenAI image workflow
- Produce batches of related image concepts
- Create website, app, game, or product visuals for active projects
- Support design exploration before implementation

## Dependencies

- Homebrew
- Python installed through Homebrew
- Conda installed and available in the shell
- A dedicated Conda environment named `codex-imagegen`
- `OPENAI_API_KEY` configured in the local shell environment
- Python packages currently installed in the active setup:
  - `openai`
  - `pillow`
  - `httpx`
  - `pydantic`
  - `tqdm`
- Current verified local environment details:
  - Homebrew Python path: `/opt/homebrew/bin/python3`
  - Conda environment: `codex-imagegen`
  - Python version in that environment: `3.12.12`

## Install Instructions

These instructions document the local setup pattern currently used on this machine.

### 1. Install Homebrew

If Homebrew is not already installed:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

### 2. Install Python with Homebrew

```bash
brew install python
```

Verify:

```bash
which python3
python3 --version
```

Expected current pattern:

- `python3` resolves to `/opt/homebrew/bin/python3`

### 3. Install Conda

Use Miniforge or another Conda distribution and ensure `conda` is available in the shell.

If using Homebrew-based setup for Miniforge:

```bash
brew install --cask miniforge
```

Then initialize Conda for the shell if needed:

```bash
conda init zsh
```

Reload the shell:

```bash
source ~/.zshrc
```

Verify:

```bash
command -v conda
conda env list
```

### 4. Create the Image Gen Environment

```bash
conda create -n codex-imagegen python=3.12 -y
```

Activate it:

```bash
source ~/.zshrc
conda activate codex-imagegen
```

### 5. Install the Current Package Set

Install the packages that match the current working environment:

```bash
python -m pip install --upgrade pip setuptools wheel
python -m pip install openai pillow httpx pydantic tqdm
```

### 6. Configure the OpenAI API Key

Set the key locally in the shell environment:

```bash
export OPENAI_API_KEY="your_api_key_here"
```

Persist it in shell config if desired:

```bash
echo 'export OPENAI_API_KEY="your_api_key_here"' >> ~/.zshrc
source ~/.zshrc
```

Do not paste the real API key into chat or commit it into a repository.

### 7. Validate the Environment

```bash
source ~/.zshrc
conda activate codex-imagegen
python -V
python -m pip list
```

Current verified environment:

- Python `3.12.12`
- Installed packages include `openai 2.20.0` and `pillow 12.1.1`

## Tool Commands

### Activate the Environment

```bash
source ~/.zshrc
conda activate codex-imagegen
```

### Verify Python

```bash
python -V
```

### List Installed Packages

```bash
python -m pip list
```

### Check the API Key Is Available

```bash
echo $OPENAI_API_KEY
```

### Recommended Operating Pattern

Before using image generation in a project:

```bash
source ~/.zshrc
conda activate codex-imagegen
```

Then run the project’s image generation workflow or the shared image generation script if available.

From your existing shared guidance, the standard prep commands are:

```bash
source ~/.zshrc
conda activate codex-imagegen
```

Batching rule from the shared workflow:

- Run up to 5 image jobs in parallel
- Wait 30 seconds after the batch completes before starting the next batch
- This exists because of the current 5 images per minute API limit assumption in the shared process
- This is the shared operating rule for Codex-managed project work using Image Gen

## MCP JSON

Not applicable.

## Tool Inputs

The following are the typical inputs AI may need to prepare for Image Gen requests.

### Image Prompt

- Purpose: Main instruction for the image to generate
- Format: Plain text prompt
- Guidance: Should describe subject, style, composition, mood, constraints, and intended use

### Edit Prompt

- Purpose: Instruction for how an existing image should be changed
- Format: Plain text prompt
- Guidance: Should clearly state what must change and what must remain unchanged

### Use Case

- Purpose: Clarifies the kind of asset being produced
- Format: Plain text
- Guidance: Examples include hero image, icon concept, product mockup, background texture, marketing image, or concept art

### Constraints

- Purpose: Define required limits for the generation
- Format: Plain text or bullet list
- Guidance: May include banned elements, text rules, style restrictions, branding restrictions, or output intent

### Source Image

- Purpose: Existing image to edit or use as a reference
- Format: File path or image input depending on workflow
- Guidance: Needed for edit, revision, and image-preserving tasks

### Mask Image

- Purpose: Defines editable regions for targeted image edits
- Format: File path or image input depending on workflow
- Guidance: Only needed when doing masked edits

### Output Filename or Output Directory

- Purpose: Controls where generated files are written
- Format: Filesystem path
- Guidance: Should use stable, descriptive names

## Outputs

### Generated Image Files

- Format: Raster image files
- Purpose: New generated visual assets for the project

### Edited Image Files

- Format: Raster image files
- Purpose: Revised versions of existing images

### Batch Image Sets

- Format: Multiple raster image outputs grouped by prompt or run
- Purpose: Compare concepts or variations for design selection

### Output Usage

- Outputs can be used in websites, apps, games, prototypes, pitch decks, product concepts, and design workflows
- Outputs should usually be reviewed before being treated as final production assets
- Generated assets may need follow-up processing, resizing, or curation depending on the project

## AI Usage Notes

- AI can prepare prompts, edit instructions, use-case framing, and output naming guidance for this tool.
- AI can also operate this tool directly when local console access is available and the environment is configured.
- Prefer the shared environment activation workflow before attempting image generation commands.
- When generating images for active projects, prompts should use project context instead of generic creative direction.
- When editing an image, prompts should explicitly state what must remain unchanged.

## Constraints and Limits

- This tool depends on a locally configured shell environment and is not portable until the environment is installed correctly.
- Live usage requires a valid `OPENAI_API_KEY`.
- Rate-limit handling should follow the current shared process:
  - Up to 5 image jobs in parallel
  - Wait 30 seconds after a batch before starting the next one
- Agents should treat that batching rule as the default workflow unless the shared tool definition is updated
- Generated assets should be reviewed for quality, correctness, and project fit before use
- Package versions may drift over time, so this file should be updated when the environment changes

## Authentication or Access Requirements

- Requires an OpenAI API key available as `OPENAI_API_KEY`
- Requires local shell access with Conda available
- Requires permission to make live API calls from the machine

## Output or Deliverables

- Image prompts
- Edit prompts
- Generated image assets
- Edited image assets
- Batch output sets for review

## Purpose and Usage Notes

- Use this tool whenever a project needs bitmap image generation or AI-assisted image editing
- Use Theme Maker or other project systems to manage accepted visual assets after generation when applicable
- Keep outputs organized by project so image assets remain traceable

## Example Requests

- “Generate three hero image concepts for this landing page.”
- “Create a background texture that matches this product’s visual theme.”
- “Edit this image to remove the background and keep the subject unchanged.”
- “Generate five icon concepts, then wait before starting the next batch.”
