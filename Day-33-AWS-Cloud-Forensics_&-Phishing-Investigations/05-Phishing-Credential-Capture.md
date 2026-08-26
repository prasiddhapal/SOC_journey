# 05 - Phishing Credential Capture

## Fake Login Page
The decoded webpage presented:

`ParrotPost Secure Webmail Login`

The email field was pre-populated, increasing the appearance of legitimacy.

## Credential Capture
The JavaScript listened for the login form submission and prevented the normal form submission.

It retrieved:

```javascript
document.getElementById("email").value
document.getElementById("password").value
```

It then created an HTTP request.

The credentials were URL-encoded with:

```javascript
encodeURIComponent()
```

## Network Request
Firefox Developer Tools -> Network showed the request to:

```text
evilparrot.thm:8080
```

with the endpoint:

```text
/cred-capture.php
```

The credentials were included as GET query parameters.

## Response
After submitting fake credentials, the server returned a successful response.

The response disclosed the credential log location:

```text
http://evilparrot.thm:8080/creds.txt
```

It also provided the lab flag:

```text
THM{c4p7ur3d_y0ur_cr3d5}
```

## Credential Log
The log contained captured email/password pairs.

The relevant entry was for:

```text
chris.smith@zebramail.com
```

The observed password was:

```text
FlyLike!A-Bird
```

## Important Evidence
The browser Network panel was more useful than the visible error message on the page. The page displayed an error to the user, while the background request still transmitted the credentials.

## Key Lesson
A visible application error does not prove that a network request failed. Always inspect browser network activity when analyzing suspicious client-side credential capture.
