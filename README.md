# Epicollect5 API

## Epicollect5 API

Epicollect5 is currently a **read-only** API. Only **GET** requests are exposed to third party clients/apps.

Adding/editing resources can be done only via Epicollect5 official applications (Android, iOS, web).

Only secure **https** requests are allowed.

## Server responses:

* 200 `OK` the request was successful.
* 400 `Bad Request` the request could not be understood or was missing required parameters.
* 404 `Not Found` the resource was not found.
* 500 `Internal Server Error` something unexpected happened

## Status code responses

When an error occurs, you will receive a status code in the response.

Error objects are returned in the standard [JSON API format](http://jsonapi.org/examples/#error-objects) and consist of:

* code - the EC5 code
* title - a title for the EC5 code (in English)
* source - the source of the response

A full list of the available status codes can be found [here](https://five.epicollect.net/json/ec5-status-codes/en.json).

## Rate limiting

We currently limit accessing the API to&#x20;

* 60 requests per minute for entries.
* 30 requests per minute for media files.
* 1000 entries per request.

{% hint style="warning" %}
Every day hundreds of developers make requests to the Epicollect5 API. To help manage the sheer volume of these requests, limits are placed on the number of requests that can be made. These limits help us provide the reliable and scalable API that our developer community relies on.
{% endhint %}

## Authentication

For **PRIVATE** projects, access to data is restricted.

In order to access the data, you need to create an Epicollect5 Client App and generate an API Token, which can be added to all requests made via the Authorization header, like so:

`Authorization: Bearer {api_token}`

This can be done from the Project Details page by the **Creator or Manager** of a Project.
