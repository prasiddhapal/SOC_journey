# 04 - Obfuscation Analysis

## Base64
The HTML attachment stored its webpage content in a Base64-encoded variable.

The browser-side decoding function was:

```javascript
atob(b64)
```

`atob()` converts a Base64-encoded string into its decoded representation.

The surrounding code then used:

```javascript
unescape(...)
```

and:

```javascript
document.write(...)
```

to render the result.

## JavaScript Obfuscation
The decoded webpage contained JavaScript that had been minified/obfuscated.

Beautifying the JavaScript made the logic readable.

Important behavior included:
- reading the email input
- reading the password input
- URL-encoding both values
- creating an `XMLHttpRequest`
- sending a GET request
- adding the credentials as query parameters

## Credential-Capture Logic
The important structure was:

```javascript
const email = document.getElementById("email").value;
const password = document.getElementById("password").value;
```

The values were then encoded with:

```javascript
encodeURIComponent()
```

and included in a URL pointing to the attacker-controlled service.

## CSS Obfuscation
The stylesheet was heavily minified/obfuscated.

The lab explained that CSS obfuscation can make copied phishing pages harder to analyze and can be used alongside other layers of obfuscation.

The useful approach was simply to focus on the closing `</style>` tag and format the CSS for readability.

## Practical Workflow
When facing an obfuscated web attachment:

1. Identify the encoding.
2. Decode one layer.
3. Beautify/minify the result for readability.
4. Search for form fields and event handlers.
5. Follow data flow from user input to network requests.
6. Inspect the request and response in browser Developer Tools.

## Key Lesson
Obfuscation does not necessarily make a malicious page sophisticated. It often only adds layers that must be peeled away systematically.
