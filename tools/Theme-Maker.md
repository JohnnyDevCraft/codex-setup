# Theme Maker

## Name

Theme Maker

## Category

Manual Tool

## URL

[themes.xelseor.com](https://themes.xelseor.com)

Related theme source:

- `theme-unifiedflow`

## Tool Description

Theme Maker is a theme-system workbench used to create, manage, refine, and export visual themes for apps and websites in a structured way.

It organizes work into projects, where each project can contain one or more themes. A theme stores semantic colors, typography choices, and theme images such as logos, icons, and backgrounds. The goal is for a theme to serve as a reusable source of truth for application styling, exportable assets, and human-readable documentation.

The current implementation is centered on the Laravel application `theme-mkr-web`, which supports:

- User accounts and authentication
- Project and theme management
- Theme color and font management
- Theme image management
- AI assistant chat
- Voice recording and transcription into chat
- Queue-based AI image generation
- Theme export packaging

The assistant is a major part of the product. Users can chat with AI in scoped contexts so the assistant understands the project or theme it is working on. The system stores chat sessions and messages, and uses the user’s own OpenAI API key for chat, transcription, and image generation workflows.

An important implemented feature is the Image Assistant on the image detail page. It lets a user discuss a specific image with AI, send voice instructions, and request revised image variants based on the current image plus surrounding project and theme context. The original image is not overwritten by default. Instead, a proposed revision is created, shown side by side with the current image, and must be explicitly accepted before becoming the active image.

Theme Maker also supports export. Current exports package the theme’s Tailwind-oriented input CSS, a README, and image assets. The broader goal is for a saved theme to become portable and understandable outside the app for both developers and non-developers.

The active visual direction is based on the `theme-unifiedflow` theme source, using Montserrat for headings and Lato for body text. The product should feel like a design-system workbench rather than a generic CRUD application.

Architecturally, the Laravel app acts as the orchestration layer, the relational database stores canonical state, and long-running image work is handled asynchronously through queues. The repository is documentation-driven, with root documents covering the product, architecture, model, theme direction, and discovery decisions as source-of-truth context.

In one sentence: Theme Maker is a system for building structured, AI-assisted, exportable visual themes, with the current product focused on managing design tokens and images through a Laravel web application.

## Primary Use Cases

- Define and refine visual themes for applications or websites
- Manage semantic colors, fonts, logos, icons, and backgrounds
- Use AI chat to discuss and evolve theme decisions
- Generate or revise theme images with AI assistance
- Export a theme as portable assets and documentation

## Tool Commands

None for shared-agent use at this time.

This tool is currently documented as a `Manual Tool`, which means AI may prepare content for the user but does not directly operate Theme Maker through MCP or shell commands based on this catalog entry.

## MCP JSON

Not applicable.

## Tool Inputs

The following are inputs AI may be asked to prepare for a human to use in Theme Maker or for related project setup work.

### Project Name

- Purpose: Name of the project that we are going to design themes for
- Audience: Internal users of Theme Maker
- Format: Plain text
- Limit: 150 characters maximum
- Guidance: Should be a concise, recognizable product or project name

### Project Description

- Purpose: Short description of the project and what it does
- Audience: Internal users of Theme Maker
- Format: Plain text
- Limit: 400 characters maximum
- Guidance: Should briefly explain what the project is, what it does, and the type of experience the theme will support

### Theme Description

- Purpose: A user-friendly explanation of the theme’s intent and personality
- Audience: Designers, developers, and stakeholders
- Format: Plain text or markdown depending on destination
- Guidance: Should describe mood, brand qualities, intended usage, and any design principles

### Color System Guidance

- Purpose: Explain the semantic role of colors in the theme
- Format: Structured text
- Guidance: Should distinguish meaning such as primary, secondary, accent, success, warning, danger, surface, border, and text roles

### Typography Guidance

- Purpose: Describe heading, body, and supporting type choices
- Format: Structured text
- Guidance: Should explain font pairing, use cases, hierarchy, and tone

### Image Prompt

- Purpose: Prompt text for AI-driven image generation or revision workflows
- Format: Plain text prompt
- Guidance: Should reference project context, theme context, image purpose, stylistic direction, and constraints

### Export README Content

- Purpose: Human-readable documentation packaged with a theme export
- Format: Markdown
- Guidance: Should explain theme purpose, included assets, color roles, typography, and implementation notes

### Tailwind Input CSS Guidance

- Purpose: Source styling direction for exported Tailwind-oriented theme assets
- Format: CSS or structured implementation notes
- Guidance: Should align semantic tokens, fonts, and theme assets to the intended exported system

## Outputs

### Zip File Export

- Format: Zip file
- Purpose: Export package containing the theme elements needed to build and design applications

### Color Outputs

- Three normal theme colors
- Each normal theme color includes `100` through `900` shades in `100` increments
- The `500` shade is the main color
- The surrounding shades provide lighter and darker variants
- Muted versions of each of the three colors are also included
- Each muted color also includes `100` through `900` shades in `100` increments

### Text Color Outputs

- One light text color
- One dark text color

### Font Outputs

- One heading font
- One body font
- Both fonts are always Google Fonts

### Image Outputs

- Logos
- Icons
- UI Icons
- Backgrounds
- General Images
- Textures

### Output Usage

- These exported theme elements are intended to be used to build and design applications
- The output package should act as a reusable source of truth for downstream implementation and design work

## AI Usage Notes

- AI can help prepare project names, project descriptions, theme descriptions, color rationales, typography rationales, export README content, and image prompts.
- AI should respect the character limits of tool inputs when generating content for this tool.
- AI should use project context, theme context, and existing documentation when generating content for this tool.
- AI should keep generated content aligned with the target brand and visual direction, not generic design language.
- AI should distinguish between content intended for end users, internal designers, and developers.

## Constraints and Limits

- `Project Name` is limited to 150 characters.
- `Project Description` is limited to 400 characters.
- Theme Maker is currently treated as a manual tool in this shared catalog.
- AI should not assume direct access to the running application unless a future tool definition adds MCP or local console workflows.
- Image-related requests should preserve the distinction between the current image and a proposed revision workflow.
- Export content should be understandable by both developers and non-developers where appropriate.

## Authentication or Access Requirements

- User accounts and authentication exist in the product.
- The system uses the user’s own OpenAI API key for chat, transcription, and image generation flows.
- Additional deployment or local setup details are not yet documented in this shared tool file.

## Output or Deliverables

- Project names
- Project descriptions
- Theme descriptions
- Theme documentation
- Image prompts
- Export README text
- Structured notes for color, typography, and asset decisions

## Architecture and Product Notes

- Primary implementation: Laravel application `theme-mkr-web`
- Theme source inspiration: `theme-unifiedflow`
- Heading font direction: Montserrat
- Body font direction: Lato
- Long-running image work is asynchronous through queues
- Repository workflow is documentation-driven

## Example Requests

- “Write a theme description for a calm, premium fintech dashboard theme.”
- “Generate export README content for this theme based on the chosen colors and fonts.”
- “Draft an image prompt for a hero background that matches the current theme.”
- “Summarize this project so I can create the theme record in Theme Maker.”
