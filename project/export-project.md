# Get Project

Export the project definition, mapping and stats for a particular Project. If the project is private, an `access_token` must be provided (See: API Authentication).

We assume the base domain to be **five.epicollect.net**.

## HTTP REQUEST

`GET /api/export/project/{project_slug}`

## Query Parameters

| Parameter     | Required            | Description                 |
| ------------- | ------------------- | --------------------------- |
| project\_slug | yes, as url segment | The slugified project name. |

## Further Descriptions

### `project_slug`

The **project\_slug** is slugified version of the project name. Any spaces in the project name are replaced by a hyphen "-" to make it url safe. To retrieve it, check the **Developers** section on your project details page. From the same page you can download the full project definition in JSON format. It is used as a segment in the request url.
