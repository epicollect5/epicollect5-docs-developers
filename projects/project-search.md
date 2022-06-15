# Project Search

Search for a Project. The response given is an array objects, each of which represents a project whose name **contains** the `project_name` string. Each object includes the project `name`, `slug`, `access` and `ref`.

We assume the base domain to be **five.epicollect.net**.

## HTTP REQUEST

`GET /api/projects/{project_name}`

## Query Parameters

| Parameter     | Required            | Description                     |
| ------------- | ------------------- | ------------------------------- |
| project\_name | yes, as url segment | A full or partial project name. |

## Further Descriptions

### `project_name`

The **project\_name** parameter can be the full or partial name of a project you wish to search for. This must be **at least 3 characters long**.
