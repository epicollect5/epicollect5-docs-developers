# Retrieve Token

Once you have set up a project App, you can then request an access token using your **Client ID** and **Client Secret**.

{% hint style="warning" %}
Access tokens are valid for **2 hours** from the time they are issued.

To help prevent abuse and ensure fair use for all users, we currently enforce a **rate limit of 10 tokens per hour per IP address**.\
This restriction helps protect the system from automated misuse and excessive traffic from a single source.
{% endhint %}

## HTTP REQUEST

We assume the base domain is **five.epicollect.net**

`POST /api/oauth/token`

therefore `https://five.epicollect.net/api/oauth/token`

## POST Parameters

| Parameter      | Required | Description                            |
| -------------- | -------- | -------------------------------------- |
| grant\_type    | yes      | Must have value 'client\_credentials'. |
| client\_id     | yes      | The Client ID of your project App.     |
| client\_secret | yes      | The Client Secret of your project App. |

Here is an example based on our **EC5 API Private** project, using jQuery ([more on jQuery Ajax requests](http://api.jquery.com/jquery.ajax/)):

[(jsFiddle here](https://jsfiddle.net/mirko77/yy3d62n6/))

```
 var params = {
   grant_type: 'client_credentials',
   client_id: 153,
   client_secret: 'J7SZDPssR885Fo0xczGKqkJfa5XyMK8wxbrOYjio'
 }

  $.ajax({
   url: 'https://five.epicollect.net/api/oauth/token',
   type: 'POST',
   contentType: 'application/vnd.api+json',
   data: JSON.stringify(params),
   success: function(response) {
     console.log(JSON.stringify(response));
   },
   error: function(xhr, status, error) {
     console.log(xhr.responseText);
   }
 });
```

**Please note you cannot access the data using a browser!**

## HTTP Response

If you run the code above, this is the response you get:

```
{
  "token_type": "Bearer",
  "expires_in": 7200,
  "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImp0aSI6Ijk5OTE4YWZmMDczYjY2MjJlNWQyODVjMzJjZTM0Y2M1MTA1MDQxY2ZjOTc2MDY5ZDE4NWU5ZDQ3ZDI0MTJkYzQ4NWM0NTI2NmQyNDdhNTYzIn0.eyJhdWQiOiIyIiwianRpIjoiOTk5MThhZmYwNzNiNjYyMmU1ZDI4NWMzMmNlMzRjYzUxMDUwNDFjZmM5NzYwNjlkMTg1ZTlkNDdkMjQxMmRjNDg1YzQ1MjY2ZDI0N2E1NjMiLCJpYXQiOjE0OTQ0MjU3MzMsIm5iZiI6MTQ5NDQyNTczMywiZXhwIjoxNDk0NDMyOTMzLCJzdWIiOiIiLCJzY29wZXMiOltdfQ.S-Lsn8uP_GlUyz5fa-QUICpkyXUvFf4L4StUYYGoJCIPdqMtS7OZqbg1oJgNvCtBnqVO4LTvl7GT6-86QEIlR3d9IpHjykFYxlfOQYIlvrgx4aFwzLk5Q1cpcMFqanM-gNBhTIcq8wOSf0_2fwwKNr991hOtwFilQs4V_KwJBcQ8tpPFR0zXEnWHhmohSna9z-BCab70CTfki6UAxcT-cYG1OPrLDwodWpvRZF2UAtEn7WIRoSICnJfbtt5G21Gvn_UzwS_FxelG-on-q_l-OkgR2GiaOUuge2Ye1hDoFfBVagQhTWcQrAZOUXt9XxsBSL_YAT9uVFYJSs-x6L4kHssYtF9aR-DS8CgI6Zr9RWJMNX53r-2WAV4Idh0qXU4vdSjYFdzOa5XTsBRHHHgrU99S4LLmDySLIJDWciJ-x1owe2pTpDk_AKUA1BgtbliDPY5qGSDBQUXoA4pX-Jh9LlQVnrchTIIDmeUCKUe7ellOfE8DmvG3YcKfjB6oFIZYmdpxM6ikfBRPYTdFMzSGtsM5YHjWaL-1CGbxcJ8Y0eaXZo1DOmlcc0SX0t66pXfyQmcchMvx_O3rze7s1kxczo2BdIOp9zd8Xf3FQT3InTGSrwE5GA3XzX04hzTMGtISvL3ZALX6g5Gl0JJ9JYCgYljPzgnrzpyAaeArShU84_I"
}
```
