# How Websites Work

## Website Basics

A website is made up of two main components:

### Front End (Client-Side)

The part of a website that users interact with directly through their browser.

Examples:

* Text
* Images
* Buttons
* Forms
* Animations

### Back End (Server-Side)

The server responsible for:

* Processing requests
* Managing databases
* Handling authentication
* Returning responses to users

### How It Works

```text
Browser → Request → Web Server
Browser ← Response ← Web Server
```

---

# Core Web Technologies

Modern websites are primarily built using:

| Technology | Purpose                       |
| ---------- | ----------------------------- |
| HTML       | Structure                     |
| CSS        | Styling                       |
| JavaScript | Functionality & Interactivity |

---

# HTML (HyperText Markup Language)

HTML provides the structure and content of a webpage.

### Basic Structure

```html
<!DOCTYPE html>
<html>
<head>
    <title>Page Title</title>
</head>
<body>
    <h1>Heading</h1>
    <p>Paragraph</p>
</body>
</html>
```

---

## Common HTML Elements

| Tag        | Purpose              |
| ---------- | -------------------- |
| `<html>`   | Root element         |
| `<head>`   | Page metadata        |
| `<title>`  | Browser tab title    |
| `<body>`   | Visible page content |
| `<h1>`     | Main heading         |
| `<p>`      | Paragraph            |
| `<img>`    | Image                |
| `<button>` | Button               |

---

## HTML Attributes

Attributes provide additional information about an element.

### Example

```html
<img src="cat.jpg">
```

### Common Attributes

| Attribute | Purpose                    |
| --------- | -------------------------- |
| src       | Resource location          |
| class     | Group elements for styling |
| id        | Unique identifier          |
| href      | Link destination           |

---

## Class vs ID

### Class

```html
<p class="important">
```

* Can be used by multiple elements.
* Mainly used for styling.

### ID

```html
<p id="header">
```

* Must be unique on a page.
* Often used by JavaScript and CSS.

---

# JavaScript (JS)

JavaScript adds functionality and interactivity to websites.

Without JavaScript, websites would mostly be static.

### Common Uses

* Button actions
* Form validation
* Animations
* Dynamic content updates
* Real-time updates

---

## JavaScript Example

```javascript
document.getElementById("demo").innerHTML = "Hack the Planet";
```

This changes the content of an HTML element.

---

## Events

JavaScript can execute when specific actions occur.

### Example

```html
<button onclick="alert('Clicked!')">
    Click Me
</button>
```

### Common Events

| Event       | Trigger         |
| ----------- | --------------- |
| onclick     | Mouse click     |
| onmouseover | Mouse hover     |
| onsubmit    | Form submission |
| onload      | Page load       |

---

# Sensitive Data Exposure

Sensitive Data Exposure occurs when confidential information is unintentionally accessible to users.

### Examples

* Hardcoded usernames/passwords
* API keys
* Hidden links
* Internal comments
* Configuration data

### Common Places to Check

* Page source code
* HTML comments
* JavaScript files
* Hidden form fields

### Security Tip

> Always inspect page source when performing web application assessments.

---

# HTML Injection

HTML Injection occurs when a website displays unsanitized user input.

### Vulnerable Example

User Input:

```html
<h1>Hacked</h1>
```

Output:

```html
<h1>Hacked</h1>
```

The browser renders the injected HTML instead of displaying it as plain text.

---

## Why It Happens

The application trusts user input without validation or filtering.

### Unsafe Flow

```text
User Input
      ↓
Application
      ↓
Displayed Without Filtering
      ↓
HTML Injection
```

---

## Prevention

### Input Sanitization

Remove or escape dangerous characters before displaying user input.

### Best Practice

> Never trust user input.

Always validate and sanitize data before processing or displaying it.

---

# Quick Revision

* Front End = What users see and interact with
* Back End = Processes requests and returns responses
* HTML = Website structure
* CSS = Website styling
* JavaScript = Website functionality
* `<body>` contains visible content
* `class` can be reused
* `id` must be unique
* JavaScript adds interactivity
* Sensitive Data Exposure = Leaked confidential information
* Check page source for exposed data
* HTML Injection = Unsanitized user input rendered as HTML
* Input Sanitization helps prevent injection attacks
