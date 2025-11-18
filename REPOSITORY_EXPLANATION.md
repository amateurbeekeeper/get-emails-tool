# Detailed Repository Explanation

## Overview

This is an **Email Discovery API** built with Next.js 14 that extracts email addresses from web pages. It's designed to be a comprehensive solution for email discovery with both API endpoints and local bulk processing capabilities.

---

## 🎯 Purpose

The repository solves the problem of discovering email addresses from web pages. It offers:

1. **API Endpoints** - RESTful API for programmatic access
2. **Local Scripts** - Command-line tools for bulk processing
3. **Interactive Documentation** - Swagger UI for testing and exploration
4. **Web Interface** - User-friendly frontend for extracting emails

---

## 🏗️ Architecture

### Technology Stack

- **Framework**: Next.js 14 (App Router)
- **Language**: TypeScript
- **UI**: React 18
- **API Documentation**: Swagger UI + OpenAPI 3.0
- **CSV Processing**: csv-parse, csv-stringify

### Project Structure

```
get-emails-from-html/
├── app/                          # Next.js App Router directory
│   ├── api/                      # API routes
│   │   ├── get-emails-from-html/
│   │   │   └── route.ts         # HTML parsing endpoint
│   │   └── swagger/
│   │       └── route.ts         # OpenAPI spec generator
│   ├── api-docs/
│   │   └── page.tsx             # Swagger UI interface
│   ├── layout.tsx               # Root layout component
│   ├── page.tsx                 # Home page with web interface
│   └── globals.css              # Global styles
├── scripts/                      # Local processing scripts
│   ├── extract-emails-from-csv.js  # Bulk email extraction
│   ├── README.md                # Script documentation
│   └── sample-domains.csv       # Example domain list
├── package.json                 # Dependencies and scripts
├── tsconfig.json                # TypeScript configuration
├── next.config.js               # Next.js configuration
├── README.md                    # Main documentation
├── POSTMAN_EXAMPLES.md          # Postman testing guide
└── ENV_SETUP.md                 # Environment setup guide
```

---

## 🔌 API Endpoints

### `/api/get-emails-from-html` (POST)

**Purpose**: Extract email addresses directly from HTML content of any web page.

**How it works**:
- Accepts a URL
- Fetches the HTML content from that URL
- Uses regex pattern matching to find all email addresses
- Filters out false positives (example.com, image files, etc.)
- Returns unique, sorted email addresses

**Key Features**:
- ✅ No API keys required
- ✅ Free to use
- ✅ Works with any publicly accessible URL
- ✅ Fast processing
- ❌ No verification (may include invalid emails)
- ❌ No additional contact details

**Use Case**: Quick extraction of emails from specific web pages, contact pages, or any publicly accessible website.

**Example Request**:
```json
{
  "url": "https://example.com/contact"
}
```

**Example Response**:
```json
{
  "url": "https://example.com/contact",
  "emails": [
    "contact@example.com",
    "info@example.com",
    "support@example.com"
  ],
  "count": 3
}
```

---

## 📊 Documentation

### Interactive Documentation

1. **Swagger UI** (`/api-docs`)
   - Visual, interactive interface
   - Test endpoints directly in browser
   - See request/response schemas
   - Try different parameters

2. **OpenAPI Spec** (`/api/swagger`)
   - Machine-readable JSON specification
   - Can be imported into Postman, Insomnia, etc.
   - Used for API client generation
   - Integration with documentation tools

### Static Documentation

- **README.md**: Comprehensive guide with examples
- **POSTMAN_EXAMPLES.md**: Step-by-step Postman setup
- **ENV_SETUP.md**: Environment variable configuration
- **scripts/README.md**: Local script documentation

---

## 🛠️ Local Scripts

### Bulk Email Extraction Script

**File**: `scripts/extract-emails-from-csv.js`

**Purpose**: Process thousands of domains from a CSV file and extract emails from each.

**Features**:
- **Concurrent Processing**: Processes multiple domains simultaneously (default: 10)
- **Progress Tracking**: Real-time progress bar with statistics
- **Incremental Saving**: Saves results every 10 domains (configurable)
- **Multiple Output Formats**: JSON or CSV
- **Error Handling**: Continues processing even if some domains fail
- **Timeout Protection**: 10-second timeout per domain
- **Statistics**: Shows success rate, email counts, processing speed

**Usage**:
```bash
node scripts/extract-emails-from-csv.js domains.csv
```

**Options**:
- `--concurrent 20`: Process 20 domains at once
- `--format csv`: Output as CSV instead of JSON
- `--output results.csv`: Custom output file
- `--timeout 15000`: 15 second timeout per request
- `--save-interval 50`: Save every 50 domains

**Progress Display**:
```
[████████████░░░░░░░░░░░░░░░░░░░░░░░░░░] 25.3% | 
Processed: 4350/17251 | 
✓ 4200 | ✗ 150 | 
📧 12500 emails | 
⏱ 120s | 
⚡ 36.2/s | 
⏳ ~356s left
```

**Output**: JSON or CSV file with all results, including:
- URL/domain processed
- Success/failure status
- Emails found
- Error messages (if any)

---

## 🔧 Configuration

### Environment Variables

**Optional**:
- `NEXT_PUBLIC_API_URL`: Base URL for Swagger docs (defaults to localhost:3000)

### Configuration Files

- **next.config.js**: Next.js settings (React strict mode enabled)
- **tsconfig.json**: TypeScript compiler options
- **.eslintrc.json**: ESLint rules (Next.js defaults)

---

## 📦 Dependencies

### Production Dependencies

- **next**: Next.js framework
- **react/react-dom**: UI library
- **swagger-ui-react**: Interactive API documentation
- **csv-parse**: Parse CSV files
- **csv-stringify**: Generate CSV output

### Development Dependencies

- **typescript**: Type safety
- **@types/node, @types/react**: TypeScript definitions
- **eslint**: Code linting
- **eslint-config-next**: Next.js ESLint rules

---

## 🚀 Usage Scenarios

### Scenario 1: Extract from Contact Page

**Use Case**: Get all emails from a company's contact page

```bash
curl -X POST http://localhost:3000/api/get-emails-from-html \
  -H "Content-Type: application/json" \
  -d '{"url": "https://company.com/contact"}'
```

**Result**: List of all email addresses found on the page

---

### Scenario 2: Bulk Processing

**Use Case**: Process 17,000 domains from a CSV file

```bash
node scripts/extract-emails-from-csv.js domains.csv --concurrent 20
```

**Result**: JSON/CSV file with emails from all successfully processed domains

---

### Scenario 3: Web Interface

**Use Case**: Quick email extraction using the web interface

1. Visit `http://localhost:3000`
2. Enter a URL
3. Click "Extract Emails"
4. View results instantly

---

## 🔒 Security & Best Practices

### Security Features

- ✅ Environment variables for configuration
- ✅ `.env.local` in `.gitignore` (keys not committed)
- ✅ URL validation (only HTTP/HTTPS allowed)
- ✅ Request timeouts (prevents hanging requests)
- ✅ Error handling (graceful failures)

### Best Practices

- TypeScript for type safety
- ESLint for code quality
- Comprehensive error messages
- Input validation
- Rate limiting ready (can be added)

---

## 📈 Performance

### API Endpoints

- **HTML extractor**: Varies by page size (typically 1-5 seconds)

### Bulk Script

- **Processing rate**: ~2-3 domains/second (with 10 concurrent)
- **Memory efficient**: Processes in batches
- **Resumable**: Saves incrementally, can resume if interrupted

---

## 🎨 User Interface

### Home Page (`/`)

- Interactive form to enter URLs
- Real-time email extraction
- Beautiful results display
- Links to documentation

### Swagger UI (`/api-docs`)

- Interactive API testing
- Request/response examples
- Schema documentation
- Try-it-out functionality

---

## 🔄 Workflow Examples

### Workflow 1: API Integration

1. Start server: `npm run dev`
2. Use endpoints in your application
3. Test with Swagger UI

### Workflow 2: Bulk Processing

1. Prepare CSV file with domains
2. Run script: `npm run extract-emails domains.csv`
3. Monitor progress in terminal
4. Review results in output file

### Workflow 3: Development

1. Clone repository
2. Install dependencies: `npm install`
3. Run dev server: `npm run dev`
4. Test endpoints
5. Build for production: `npm run build`

---

## 🎯 Key Features

### Why This Approach?

1. **No External Dependencies**: Works without API keys or paid services
2. **Free**: No cost per request
3. **Fast**: Direct HTML parsing
4. **Simple**: Easy to use and understand
5. **Flexible**: Works with any publicly accessible URL

---

## 📝 Code Quality

- **TypeScript**: Full type safety
- **Error Handling**: Comprehensive try-catch blocks
- **Validation**: Input validation on all endpoints
- **Documentation**: Inline comments and JSDoc
- **Consistent Style**: ESLint enforced

---

## 🚢 Deployment

### Production Build

```bash
npm run build
npm start
```

### Environment Setup

1. Set `NEXT_PUBLIC_API_URL` to production URL (optional)
2. Deploy to Vercel, AWS, or any Node.js host

### Recommended Platforms

- **Vercel**: Optimized for Next.js (recommended)
- **AWS Lambda**: Serverless deployment
- **Docker**: Containerized deployment
- **Traditional hosting**: Any Node.js server

---

## 🔮 Future Enhancements (Potential)

- Rate limiting middleware
- Caching layer (Redis)
- Database storage for results
- Webhook support
- Batch API endpoints
- Email validation
- Additional email finder services
- Authentication/API keys for public use

---

## 📚 Additional Resources

- **Next.js Docs**: https://nextjs.org/docs
- **OpenAPI Spec**: https://swagger.io/specification/
- **Postman**: https://www.postman.com/

---

## 🤝 Contributing

This is a public repository designed for:
- Learning Next.js API routes
- Email discovery use cases
- API documentation examples
- Bulk processing patterns

---

## 📄 License

Check repository for license information.

---

## 🎓 Learning Points

This repository demonstrates:
- Next.js App Router API routes
- TypeScript in API development
- Swagger/OpenAPI documentation
- Concurrent processing patterns
- Progress tracking and reporting
- Error handling best practices
- Environment variable management
- CSV processing
- RESTful API design
- React client components
- Modern UI/UX design

---

## 💡 Tips for Users

1. **Start with the web interface** - No setup required, test immediately
2. **Bulk script for scale** - Process thousands efficiently
3. **Swagger for testing** - Interactive testing is faster
4. **Monitor progress** - Watch the progress bar for bulk jobs
5. **Save incrementally** - Results saved automatically, safe to interrupt
6. **Try contact pages** - Contact pages often have the most emails

---

This repository provides a complete solution for email discovery with both API and CLI tools, comprehensive documentation, and production-ready code.
