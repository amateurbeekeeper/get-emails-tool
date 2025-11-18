# Environment Variables Setup

## Quick Setup

1. Create a `.env.local` file in the root directory:

```bash
touch .env.local
```

2. Add your environment variables (all optional):

```bash
# Optional: API Base URL (for Swagger documentation)
NEXT_PUBLIC_API_URL=http://localhost:3000
```

## Environment Variables

### Optional

- **NEXT_PUBLIC_API_URL** - Base URL for your API
  - Used in Swagger documentation
  - Defaults to `http://localhost:3000` if not set

## File Location

- `.env.local` - Your local environment variables (not committed to git)
- `.env.example` - Template file (can be committed to git)

## Security Note

The `.env.local` file is already in `.gitignore` and will NOT be committed to version control.

## No API Keys Required

This application does not require any API keys or external service credentials. It works out of the box by directly parsing HTML content from URLs.
