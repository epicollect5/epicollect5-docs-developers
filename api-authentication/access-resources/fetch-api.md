---
description: https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch
---

# Fetch API

Using `fetch()` [JSFiddle](https://jsfiddle.net/mirko77/28qk35mx/4)

```
// Replace parameters with your own credentials
const params = {
  grant_type: 'client_credentials',
  client_id: 4879,
  client_secret: 'XbIHCZHh5WQhJCaLduHSAzzddFFI6PkHA78XUZeE'
};

// Replace with your project slug
const projectSlug = "ec5-api-private";

// Perform Fetch request to get token
fetch('https://five.epicollect.net/api/oauth/token', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/vnd.api+json'
  },
  body: JSON.stringify(params)
})
.then(response => response.json())
.then(data => {
  console.log(JSON.stringify(data));
  // The token is valid for 2 hours, let's get the entries
  _getEntries(data.access_token);
})
.catch(error => {
  console.error(error);
});

// Get the entries, passing token for authorization
function _getEntries(token) {
  fetch(`https://five.epicollect.net/api/export/entries/${projectSlug}`, {
    headers: {
      'Content-Type': 'application/vnd.api+json',
      'Authorization': `Bearer ${token}`
    }
  })
  .then(response => response.json())
  .then(data => {
    console.log(JSON.stringify(data, null, 2));
    document.querySelector('.content').textContent = JSON.stringify(data, null, 2);
  })
  .catch(error => {
    console.error(error);
    document.querySelector('.content').textContent = JSON.stringify(error, null, 2);
  });
}

```
