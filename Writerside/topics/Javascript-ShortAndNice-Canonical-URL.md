# Canonical URL

## Get the value of canonical URL

To get the value of the canonical URL from the `<link>` tag in the HTML head, you can use the following JavaScript code:
```javascript
const canonicalURLValue = document.querySelector("link[rel='canonical']").href;
```

But if you want to handle the case where the canonical URL is not present, you can use the following code:
```javascript
const canonicalURL = document.querySelector("link[rel='canonical']");
const canonicalURLValue = canonicalURL ? canonicalURL.href : null;
```

You can also use optional chaining to simplify the code:
```javascript
const canonicalURLValue = document.querySelector("link[rel='canonical']")?.href;
```

But if you need to support older browsers that do not have optional chaining, you can use a more traditional approach:
```javascript
const canonicalURLValue = (document.querySelector("link[rel='canonical']") || {}).href || "";
```
