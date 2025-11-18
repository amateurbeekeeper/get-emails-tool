# Email Discovery API

A Next.js API for extracting email addresses from web pages. Fetches HTML content and extracts all email addresses found using regex pattern matching.

![Email Finder](1763497969575.jpeg)

## Getting Started

### Installation

Install the dependencies:

```bash
npm install
# or
yarn install
# or
pnpm install
```

### Environment Variables

Create a `.env.local` file in the root directory (copy from `.env.example`):

```bash
cp .env.example .env.local
```

Then edit `.env.local` and add any optional configuration:

```bash
# Optional: API Base URL (for Swagger documentation)
# NEXT_PUBLIC_API_URL=http://localhost:3000
```

**Optional Environment Variables:**
- `NEXT_PUBLIC_API_URL` - Base URL for API (used in Swagger docs, defaults to `http://localhost:3000`)

**Note:** The `.env.local` file is already in `.gitignore` and will not be committed to version control. **No API keys are required** - this tool works out of the box!

### Development

Run the development server:

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser to see the application.

## API Documentation

### Interactive Documentation

- **Swagger UI** (`/api-docs`): Interactive web interface to test API endpoints directly from your browser
  - Visit: [http://localhost:3000/api-docs](http://localhost:3000/api-docs)
  - Try endpoints, see request/response examples, and test with real data

- **OpenAPI Specification** (`/api/swagger`): Machine-readable OpenAPI 3.0 JSON specification
  - Visit: [http://localhost:3000/api/swagger](http://localhost:3000/api/swagger)
  - Use for API client generation, documentation tools, or integration with other services

**Note:** Both are useful - Swagger UI for interactive testing and exploration, OpenAPI spec for programmatic access and tooling.

## API Endpoints

### 📄 POST /api/get-emails-from-html

**Extract email addresses directly from HTML content**

Fetches HTML from a URL and extracts all email addresses found in the page content using regex pattern matching. No external services or API keys required.

**✅ No API keys required** - Works out of the box

**Request Body:**
```json
{
  "url": "https://example.com"
}
```

**Response:**
```json
{
  "url": "https://example.com",
  "emails": [
    "contact@example.com",
    "info@example.com"
  ],
  "count": 2
}
```

**GET /api/get-emails-from-html** - Get API information about this endpoint

---

## Example Usage

```bash
curl -X POST http://localhost:3000/api/get-emails-from-html \
  -H "Content-Type: application/json" \
  -d '{
    "url": "https://example.com"
  }'
```

```typescript
const response = await fetch('http://localhost:3000/api/get-emails-from-html', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    url: 'https://example.com',
  }),
});

const result = await response.json();
console.log(result);
```

## Bulk Processing

For bulk processing of domains from a CSV file, download the repository and use the local script:

```bash
# Install dependencies first
npm install

# Run the script
node scripts/extract-emails-from-csv.js domains.csv

# Or use the npm script
npm run extract-emails domains.csv
```

**Options:**
- `--format csv` or `--format json` - Output format (default: json)
- `--output results.json` - Output file path
- `--concurrent 10` - Number of concurrent requests (default: 5)
- `--timeout 15000` - Timeout per request in ms (default: 10000)

**Example:**
```bash
node scripts/extract-emails-from-csv.js domains.csv --format csv --concurrent 10
```

The script processes domains concurrently, saves results incrementally, and provides progress updates. See `scripts/README.md` for detailed documentation.

## Build

Build the application for production:

```bash
npm run build
# or
yarn build
# or
pnpm build
```

## Start Production Server

Start the production server:

```bash
npm start
# or
yarn start
# or
pnpm start
```

## Project Structure

```
.
├── app/
│   ├── api/
│   │   ├── get-emails-from-html/
│   │   │   └── route.ts      # HTML email extractor API route
│   │   └── swagger/
│   │       └── route.ts      # OpenAPI/Swagger spec endpoint
│   ├── api-docs/
│   │   └── page.tsx          # Swagger UI interactive documentation
│   ├── layout.tsx            # Root layout
│   ├── page.tsx              # Home page
│   └── globals.css           # Global styles
├── next.config.js            # Next.js configuration
├── package.json              # Dependencies
├── tsconfig.json             # TypeScript configuration
└── README.md                 # This file
```

## Technologies

- [Next.js 14](https://nextjs.org/) - React framework
- [TypeScript](https://www.typescriptlang.org/) - Type safety
- [React](https://react.dev/) - UI library
