# Epicollect5 API

## Epicollect5 API

Epicollect5 is currently a **read-only** API. Only **GET** requests are exposed to third-party clients/apps.

Adding/editing resources can be done only via the Epicollect5 official applications (Android, iOS, web).

Only secure **HTTPS** requests are allowed.

## Server responses:

* 200 `OK` The request was successful.
* 400 `Bad Request` The request could not be understood or was missing required parameters.
* 404 `Not Found` The resource was not found.
* 500 `Internal Server Error` Something unexpected happened

## Status code responses

When an error occurs, you will receive a status code in the response.

Error objects are returned in the standard [JSON API format](http://jsonapi.org/examples/#error-objects) and consist of:

* code - the EC5 code
* title - a title for the EC5 code (in English)
* source - the source of the response

A full list of the available status codes can be found [here](https://five.epicollect.net/json/ec5-status-codes/en.json).

## Rate limiting

We currently limit access to the API to

* 10 requests per hour per project.
* 30 requests per minute for media files.
* 500 entries per request.
* 10 auth tokens per hour.

{% hint style="warning" %}
Every day, hundreds of developers make requests to the Epicollect5 API. To help manage the sheer volume of these requests, limits are placed on the number of requests that can be made. These limits help us provide a reliable and scalable API that our developer community relies on.
{% endhint %}

## Google Apps Scripts Integration

Google Apps Script is a popular way to sync Epicollect5 data into Google Sheets. However, Google Apps Script rotates through a large pool of shared IP addresses, which means multiple users' scripts share the same IP. This makes it impossible for us to apply per-user limits without affecting other users on the same IP.

As a result, **Google Apps Script integrations are subject to the same 10 requests per hour limit shared across all scripts at any given time.**

To avoid hitting this limit, follow the best practices below.

#### Best practices for automated exports

**✅ Always use a date filter**

The most important optimisation. Instead of fetching your entire dataset on every run, only fetch entries uploaded since your last sync:

```
/api/export/entries/{project-slug}
    ?form_ref={your-form-ref}
    &per_page=500
    &filter_by=uploaded_at
    &filter_from=2026-03-15T00:00:00.000Z
```

In your script, store the timestamp of the last successful sync and use it as `filter_from` on the next run. This way, each run fetches only new entries — typically a handful of rows — rather than your entire dataset.

**✅ Use per\_page=500**

Using smaller page sizes like `per_page=100` means 10× more requests for the same data. Always use `per_page=500` unless you have a specific reason not to.

**✅ Add a delay between requests in your script**

Even a small delay between paginated requests spreads the load and keeps you well within the rate limit. In Google Apps Script:

```javascript
function exportData() {
  const baseUrl = 'https://five.epicollect.net/api/export/entries/your-project';
  const formRef = 'your-form-ref';
  const props = PropertiesService.getScriptProperties();
  
  // 1. Check Hourly Request Budget (Limit: 10 per hour)
  const now = new Date().getTime();
  let usage = JSON.parse(props.getProperty('hourly_usage') || '{"count": 0, "reset": 0}');
  
  // Reset usage if an hour has passed
  if (now > usage.reset) {
    usage = { count: 0, reset: now + (60 * 60 * 1000) };
  }
  
  const lastSync = props.getProperty('last_sync_date') || '2020-01-01T00:00:00Z';
  let page = 1;
  let allData = [];
  
  while (usage.count < 10) { // Strict 10 requests per hour limit
    // 2. Updated per_page to 500
    const url = `${baseUrl}?form_ref=${formRef}&per_page=500&page=${page}` +
                `&filter_by=created_at&filter_from=${lastSync}&sort_order=ASC`;
    
    const response = UrlFetchApp.fetch(url, {
      headers: { 'Authorization': 'Bearer ' + getToken() },
      muteHttpExceptions: true // Allows us to handle 429 errors gracefully
    });

    const code = response.getResponseCode();
    
    if (code === 429) {
      console.warn('Rate limit reached on server. Stopping for now.');
      break; 
    }

    const json = JSON.parse(response.getContentText());
    const entries = json.data.data;
    
    if (!entries || entries.length === 0) break;

    allData = allData.concat(entries);
    
    // Track last successfully fetched timestamp to prevent redundant repeats
    const newestEntryTime = entries[entries.length - 1].created_at;
    props.setProperty('last_sync_date', newestEntryTime);
    
    usage.count++;
    page++;
    
    // Save current usage state
    props.setProperty('hourly_usage', JSON.stringify(usage));

    // Small delay (10 secs) to be polite to the server CPU
    Utilities.sleep(10000); 
  }

  if (usage.count >= 10) {
    console.log('Hourly budget exhausted. Script will resume on next trigger.');
  }

  return allData;
}
```

**❌ Do not fetch your entire dataset on every run**

Fetching all pages of a large project on every script execution is the most common cause of rate limit violations. It is unnecessary in almost all cases and places a significant load on our servers, affecting all Epicollect5 users.

Scripts that repeatedly fetch entire datasets without date filters will receive a `429 Too Many Requests` response. Persistent violations may result in automated API access being suspended for the affected project.

## Authentication

For **PRIVATE** projects, access to data is restricted.

To access the data, you need to create an Epicollect5 Client App and generate an API Token, which can be added to all requests made via the **Authorization** header, like so:

`Authorization: Bearer {api_token}`

This can be done from the Project Details page by the **Creator or Manager** of a Project.
