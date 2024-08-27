# Getting Media

### Public project

We set up a project called [EC5 API Test](https://five.epicollect.net/project/ec5-api-test). The project is **public** so anyone can perform a GET request to fetch its entries. However, the same approach can be used for private projects by providing a valid \``Authorization: Bearer {value}`\`  in the request, as explained in the [API authentication section](../api-authentication/access-resources/)**.**

Here is the response of the following GET endpoint, to retrieve a project logo image: ([Open in browser](https://five.epicollect.net/api/export/media/ec5-api-test?type=photo\&format=project\_thumb\&name=logo.jpg))

```
https://five.epicollect.net/api/export/media/ec5-api-test?type=photo&format=project_thumb&name=logo.jpg
```

Here is the response of the following GET endpoint, to retrieve an answer original image: ([Open in browser](https://five.epicollect.net/api/export/media/ec5-api-test?type=photo\&format=entry\_original\&name=768bb179-fd2c-87b1-ec20-86a9acfdc87a\_1493303895.jpg))

```
https://five.epicollect.net/api/export/media/ec5-api-test?type=photo&format=entry_original&name=768bb179-fd2c-87b1-ec20-86a9acfdc87a_1493303895.jpg
```

You can also get the image as a blob, useful when the project is private: ([jsFiddle](https://jsfiddle.net/mirko77/y45brprq/))



### Javascript

```
var mediaEndpoint = 'https://five.epicollect.net/api/export/media/ec5-api-test?';

 function _getEntries() {
   window.setTimeout(function() {
     $.ajax({
       url: 'https://five.epicollect.net/api/export/entries/ec5-api-test',
       type: 'GET',
       contentType: 'application/vnd.api+json',
       success: function(response) {
         var entries = response.data.entries;
         var images = [];
         var filename;

         $(response.data.entries).each(function(index, entry) {
           filename = entry.photo;

           _getMedia(mediaEndpoint + 'type=photo&format=entry_original&name=' + entry.photo)
         });
       },
       error: function(xhr, status, error) {
         console.log(xhr.responseText);
       }
     });
   }, 1000);
 }

 function _getMedia(fileUrl) {

   var myImage = document.querySelector('img');

   //uncomment and add the token to the headers if the project is private
   //var myHeaders = new Headers();
   //myHeaders.append("Authorization", 'Bearer ' + token);
   var myInit = {
     method: 'GET',
    // headers: myHeaders, //uncomment when project is private
     mode: 'cors',
     cache: 'default'
   };

   fetch(fileUrl, myInit).then(function(response) {
     return response.blob();
   }).then(function(myBlob) {
     var objectURL = URL.createObjectURL(myBlob);
     myImage.src = objectURL;
   });
 }

 _getEntries();
```

You can get the media files and download them to your server.

### PHP

Here is an example using PHP and [Guzzle](http://docs.guzzlephp.org/en/stable/index.html) (add your project credentials accordingly):

```
use GuzzleHttp\Exception\RequestException;
use GuzzleHttp\Client;

$tokenClient = new Client();
$tokenURL = $this->serverURL.'/api/oauth/token';

 //get token first
 try {
     $tokenResponse = $tokenClient->request('POST', $tokenURL, [
         'headers' => [
         'Content-Type' => 'application/vnd.api+json'
         ],
         'body' => json_encode([
             'grant_type' => 'client_credentials',
             'client_id' => $this->clientId,
             'client_secret' => $this->clientSecret
         ])
     ]);

     $body = $tokenResponse->getBody();
     $obj = json_decode($body);
     $token = $obj->access_token;
 } catch (RequestException $e) {
     //handle errors
     echo $e->getMessage();
     exit();
 }

 //get media files now
 $mediaURL = $this->serverURL.'/api/export/entries/'.$this->projectSlug;

 $mediaClient = new Client([
     'headers' => [
         'Authorization' => 'Bearer '.$token //this will last for 2 hours!
     ]
 ]);

 try {
     //Get all entries for main form
     $response = $mediaClient-> request('GET', $mediaURL);
     $entries = json_decode($response->getBody())->data-> entries;

     //loop all entries to find the file names
     foreach($entries as $entry) {

        //get the media file (need to look at the project structure)
         $filename = $entry->photo;

         //build the full resolution image url
         $params='?type=photo&format=entry_original&name=';
         $photoURL = $this->serverURL.$this->mediaEndpoint.$this->projectSlug.$params.$filename;

         //get media file and save to proper location
         //IMPORTANT: you server needs to have write access to the folder you are saving the files to
         $mediaClient->request('GET', $photoURL, ['sink' => {your_server_storage_path}.'/'.$filename]);

     }
 } catch (RequestException $e) {
     //handle errors
     echo $e-> getMessage();
     exit();
 }
```



### Private project

We set up a private project for testing called [EC5 Media API Demo](https://five.epicollect.net/project/ec5-media-api-demo).

The project has a single entry with a photo.\
\
The credentials to access this project entry are as follows:

<table><thead><tr><th></th><th width="478"></th><th></th></tr></thead><tbody><tr><td>client ID</td><td>4945</td><td></td></tr><tr><td>client Secret</td><td>djCKm1JGxDJ2zwjr10I4WNkpl7QpvsAbGwimMnXr</td><td></td></tr><tr><td></td><td></td><td></td></tr></tbody></table>

Using a GET request with a proper authorization header and a valid token as explained in t[he authentication section](broken-reference) the photo will be retrieved correctly.\
\
`https://five.epicollect.net/api/export/media/ec5-media-api-demo?type=photo&name=e791b360-cf21-11ee-8f4e-0d257c6d0c4d_1708345534.jpg&format=entry_original`\


Using [Insomnia ](https://insomnia.rest/)client:

<figure><img src="../.gitbook/assets/Screenshot 2024-02-19 at 15.33.37.png" alt=""><figcaption></figcaption></figure>

### JQuery&#x20;

See the fiddle at [https://jsfiddle.net/mirko77/6ugLe5da/](https://jsfiddle.net/mirko77/6ugLe5da/)
