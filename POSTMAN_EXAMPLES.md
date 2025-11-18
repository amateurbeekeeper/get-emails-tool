# Postman Test Examples

## Get Emails from HTML Endpoint

### Request Details

**Method:** `POST`  
**URL:** `http://localhost:3000/api/get-emails-from-html`

### Headers

```
Content-Type: application/json
```

### Request Body (JSON)

```json
{
  "url": "https://example.com"
}
```

### Example Requests

#### Test 1: Basic URL
```json
{
  "url": "https://example.com"
}
```

#### Test 2: Company Website
```json
{
  "url": "https://stripe.com"
}
```

#### Test 3: News Website
```json
{
  "url": "https://techcrunch.com"
}
```

#### Test 4: Contact Page
```json
{
  "url": "https://example.com/contact"
}
```

### Expected Response (Success)

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

### Expected Response (Error - Invalid URL)

```json
{
  "error": "Invalid request: url field is required"
}
```

### Expected Response (Error - Timeout)

```json
{
  "error": "Request timeout: The URL took too long to respond",
  "url": "https://example.com"
}
```

---

## Quick Postman Setup

### For HTML Email Extractor

1. **Create a new request**
   - Method: `POST`
   - URL: `http://localhost:3000/api/get-emails-from-html`

2. **Set Headers**
   - Key: `Content-Type`
   - Value: `application/json`

3. **Set Body**
   - Select: `raw`
   - Format: `JSON`
   - Paste the JSON body from above

4. **Send Request**

**Note:** This endpoint requires no API keys or authentication. It works out of the box!

---

## Environment Variables (Optional)

Create a Postman environment with:

- `base_url`: `http://localhost:3000`

Then use: `{{base_url}}/api/get-emails-from-html`
