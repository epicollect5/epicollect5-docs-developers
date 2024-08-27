# PHP

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
