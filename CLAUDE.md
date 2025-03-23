# Blogme - Development Guide

## Commands

- `npm run dev` - Start development server
- `npm run build` - Build production site
- `npm run preview` - Preview built site locally
- `npm run astro -- --help` - Get Astro CLI help

## Code Style Guidelines

- **TypeScript**: Follow strict mode with strictNullChecks enabled
- **Imports**: Group by external/internal, alphabetical order
- **Formatting**: Use tabs for indentation, single quotes for strings
- **Components**: Separate Astro frontmatter (---)
- **Naming**:
  - Components: PascalCase (e.g., HeaderLink.astro)
  - Files: kebab-case for content (e.g., markdown-style-guide.md)
  - Variables: camelCase, constants in UPPER_SNAKE_CASE
- **Content Structure**: Use frontmatter with title, slug, description, pubDate, heroImage

## Project Structure

Astro blog with MDX support, sitemap generation, and RSS feed.
