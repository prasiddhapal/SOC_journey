# 03 - Email Attachment Analysis

## Objective
Analyze a suspicious email attachment and determine what the attached HTML document does.

## Attachment Analysis
The `.eml` file contained an embedded attachment named:

`ParrotPostACTIONREQUIRED.htm`

The MIME metadata identified it as an HTML attachment.

The investigation noted that attackers can use alternate HTML-related extensions such as `.htm` to bypass simplistic file-type filtering.

## Content Transfer Encoding
The attachment content was Base64 encoded inside the email.

The encoded data was extracted for analysis.

## HTML Analysis
The extracted file contained an HTML page with a script:

```html
<script>
    var b64 = "...";
    document.write(unescape(atob(b64)));
</script>
```

The important indicators were:
- variable containing Base64 data
- `atob()` used to decode Base64
- `unescape()` used on the decoded data
- `document.write()` used to render the resulting content

## Decoding Workflow
1. Extract the HTML attachment.
2. Open the HTML as text.
3. Locate the encoded variable.
4. Copy the Base64 value.
5. Decode it with a suitable Base64 decoder.
6. Inspect the resulting HTML.
7. Continue into the JavaScript and form behavior.

## Result
The decoded content revealed a fake ParrotPost secure webmail login page.

The page was designed to look legitimate and collect an email address and password.

## Key Lesson
An attachment that appears to be a normal HTML document can contain multiple layers of encoding and executable browser-side logic. Inspect the source rather than trusting the rendered page.
