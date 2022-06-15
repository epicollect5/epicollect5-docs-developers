# Access Resources

In order to access a private project's resources over the API, you **must include a valid access token** in the `Authorization` header with each request:

`Authorization: Bearer {access_token}`

For example, using **jQuery**: ([Open in browser](https://jsfiddle.net/mirko77/yy3d62n6/))

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

Using **PHP**, with [Guzzle](http://docs.guzzlephp.org/en/stable/): (Add your project credentials accordingly)

```
use GuzzleHttp\Exception\RequestException;
use GuzzleHttp\Client;

 $tokenClient = new Client(); //GuzzleHttp\Client
 $tokenURL = 'https://five.epicollect.net/api/oauth/token';

 //get token first
 try {
     $tokenResponse = $tokenClient->request('POST', $tokenURL, [
         'headers' => ['Content-Type' => 'application/vnd.api+json'],
         'body' => json_encode([
             'grant_type' => 'client_credentials',
             'client_id' => {your_client_id},
             'client_secret' => '{your_client_secret}'
         ])
     ]);

     $body = $tokenResponse->getBody();
     $obj = json_decode($body);
     $token = $obj->access_token;
 } catch (RequestException $e) {
     //handle errors
     //...
 }

 //get entries now
 $entriesURL = 'https://five.epicollect.net/api/export/entries/{project_slug}';
 $entriesClient = new Client([
     'headers' => [
         'Authorization' => 'Bearer '.$token //this will last for 2 hours!
     ]
 ]);

 try {
     $response = $entriesClient-> request('GET', $entriesURL);

     $body = $response->getBody();
     $obj = json_decode($body);

     //do something with the entries
     echo '<pre>';
     print_r($obj);
     echo '</pre>';

 } catch (RequestException $e) {
     //handle errors
     //...
 }
```

Please note the entries are paginated by 50 at a time.
