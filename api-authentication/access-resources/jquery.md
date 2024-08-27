# JQuery

For example, using **jQuery** [**(JSFiddle)**](https://jsfiddle.net/yvbf4cw1/)

```
//Example of getting entries using jQuery

//Replace parameters with your own
var params = {
  grant_type: 'client_credentials',
  client_id: 2,
  client_secret: 'QowjYIFrWbzLEwttXzuTnb20OPbRWwlPlaNLQ6VW'
}

//perform Ajax request to get token
$.ajax({
  url: 'https://five.epicollect.net/api/oauth/token',
  type: 'POST',
  contentType: 'application/vnd.api+json',
  data: JSON.stringify(params),
  success: function(response) {
    console.log(JSON.stringify(response));
    //the token is valid for 2 hours, let's get the entries
    _getEntries(response.access_token);
  },
  error: function(xhr, status, error) {
    console.log(xhr.responseText);
  }
});

//get the entries, passing token for authorisation
//ec5-api-test is the project slug
function _getEntries(token) {
  $.ajax({
    url: 'https://five.epicollect.net/api/export/entries/ec5-api-test',
    type: 'GET',
    contentType: 'application/vnd.api+json',
    headers: {
      Authorization: 'Bearer ' + token
    },
    success: function(response) {
      //Here are the entries, just log them for now ;)
      console.log(JSON.stringify(response));

      //do what you want with the response (entries)
      // ...
    },
    error: function(xhr, status, error) {
      console.log(xhr.responseText);
    }
  });
}
```
