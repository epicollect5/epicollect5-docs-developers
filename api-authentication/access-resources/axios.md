# Axios

Using the Axios library ([JSFiddle](https://jsfiddle.net/mirko77/4eymak75/1/))

```

// Example of getting entries using Axios

// Replace parameters with your own credentials
const params = {
  grant_type: 'client_credentials',
  client_id: 4879,
  client_secret: 'XbIHCZHh5WQhJCaLduHSAzzddFFI6PkHA78XUZeE'
};

// Replace with your project slug
const projectSlug = "ec5-api-private";

// Perform Axios request to get token
axios.post('https://five.epicollect.net/api/oauth/token', params, {
  headers: {
    'Content-Type': 'application/vnd.api+json'
  }
})
.then(response => {
  console.log(JSON.stringify(response.data));
  // The token is valid for 2 hours, let's get the entries
  _getEntries(response.data.access_token);
})
.catch(error => {
  console.error(error.response.data);
});

// Get the entries, passing token for authorization
function _getEntries(token) {
  axios.get(`https://five.epicollect.net/api/export/entries/${projectSlug}`, {
    headers: {
      'Content-Type': 'application/vnd.api+json',
      'Authorization': `Bearer ${token}`
    }
  })
  .then(response => {
    console.log(JSON.stringify(response.data, null, 2));
    document.querySelector('.content').textContent = JSON.stringify(response.data, null, 2);
  })
  .catch(error => {
    console.error(error.response.data);
    document.querySelector('.content').textContent = JSON.stringify(error.response.data, null, 2);
  });
}

```
