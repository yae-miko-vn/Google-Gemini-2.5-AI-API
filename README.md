
# AI Chat Backend

A Flask-based web service that provides an AI chat interface using Google's Gemini API with multi-language support and rate limiting.

## Features

- **Multi-language Support**: Arabic (ar), French (fr), and English (eng)
- **Rate Limiting**: Prevents abuse with IP-based request limiting (20 requests per minute)
- **RESTful API**: Supports both GET and POST requests
- **CORS Enabled**: Can be accessed from different domains
- **Error Handling**: Comprehensive error responses for various scenarios

## API Endpoints

### POST/GET `/ask`

Send a message to the AI and get a response in the specified language.

#### Parameters

- `msg` (required): The message/question to send to the AI
- `lang` (optional): Language code - `ar` (Arabic), `fr` (French), or `eng` (English). Defaults to `eng`.

#### Request Examples

**GET Request:**
```
/ask?msg=Hello, how are you?&lang=eng
```

**POST Request:**
```json
{
  "msg": "What is the weather like today?",
  "lang": "fr"
}
```

#### Response

**Success:**
```json
{
  "answer": "AI response content here..."
}
```

**Error Responses:**
```json
{
  "error": "rate_limited",
  "message": "Too many requests. Try later."
}
```

```json
{
  "error": "missing_msg",
  "message": "Provide msg and lang (ar, fr, eng)"
}
```

```json
{
  "error": "unsupported_lang",
  "message": "Supported: ['ar', 'fr', 'eng']"
}
```

## Installation

1. Clone the repository
2. Install required dependencies:
```bash
pip install flask flask-cors requests
```

3. Run the application:
```bash
python Google_Gemini_2-5-AI-API.py
```

The server will start on `http://0.0.0.0:5000`

## Configuration

- The application uses Google Gemini API with the model `gemini-2.5-flash`
- API key is hardcoded in the application
- Rate limiting: 20 requests per minute per IP address
- Supported languages are defined in the `lo8a` dictionary

## Error Codes

- `400`: Bad Request (missing parameters or unsupported language)
- `429`: Too Many Requests (rate limit exceeded)
- `502`: Bad Gateway (Gemini API error)

## Development

Developed by @yae-miko-vn

**Note**: This code contains a hardcoded API key which is not recommended for production use. Consider using environment variables or secure configuration management for production deployments.
```
