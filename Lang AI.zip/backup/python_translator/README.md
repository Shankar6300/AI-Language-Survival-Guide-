# Python Translation Server

This is a simple Flask-based server that provides API endpoints for language detection and translation services.

## Setup

1. Make sure you have Python 3.6+ installed on your system
2. Install the required dependencies:

```bash
pip install -r requirements.txt
```

## Running the Server

```bash
python translate_server.py
```

The server will start on http://localhost:5000 by default.

## API Endpoints

### Language Detection

**Endpoint:** `/api/detect`  
**Method:** POST  
**Parameters:**
- `q`: The text to detect the language of

**Example Request:**
```json
{
  "q": "Hello, how are you?"
}
```

**Example Response:**
```json
{
  "language": "en"
}
```

### Translation

**Endpoint:** `/api/translate`  
**Method:** POST  
**Parameters:**
- `q`: The text to translate
- `source`: The source language code (e.g., 'en', 'es', 'fr')
- `target`: The target language code

**Example Request:**
```json
{
  "q": "Hello, how are you?",
  "source": "en",
  "target": "es"
}
```

**Example Response:**
```json
{
  "translatedText": "Hola, ¿cómo estás?",
  "source": "en",
  "target": "es"
}
```

### Get Supported Languages

**Endpoint:** `/api/languages`  
**Method:** GET

**Example Response:**
```json
{
  "languages": {
    "auto": "Auto Detect",
    "en": "English",
    "es": "Spanish",
    "fr": "French",
    "de": "German",
    "it": "Italian",
    "ja": "Japanese",
    "zh": "Chinese",
    "ru": "Russian",
    "pt": "Portuguese",
    "ar": "Arabic",
    "hi": "Hindi",
    "ko": "Korean",
    "nl": "Dutch",
    "sv": "Swedish",
    "tr": "Turkish",
    "te": "Telugu"
  }
}
```

## Integration with JavaScript Frontend

Update your JavaScript code to use this API instead of directly calling the translation services:

```javascript
// Example of language detection
function detectLanguageAPI(text) {
    return fetch('http://localhost:5000/api/detect', {
        method: 'POST',
        body: JSON.stringify({ q: text }),
        headers: {
            'Content-Type': 'application/json'
        }
    })
    .then(response => response.json())
    .then(data => data.language);
}

// Example of translation
function translateWithAPI(text, fromLang, toLang) {
    return fetch('http://localhost:5000/api/translate', {
        method: 'POST',
        body: JSON.stringify({
            q: text,
            source: fromLang,
            target: toLang
        }),
        headers: {
            'Content-Type': 'application/json'
        }
    })
    .then(response => response.json())
    .then(data => data.translatedText);
}
``` 