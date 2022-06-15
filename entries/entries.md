# Get Entries

Get the entries for a particular Form for a Project, mapped using either your custom mapping or the EC5 AUTO mapping. If the project is private, an `access_token` must be provided (See: API Authentication).

We assume the base domain to be **five.epicollect.net**.

## HTTP REQUEST

`GET /api/export/entries/{project_slug}?{key=value&key=value...}`

## Query Parameters

| Parameter         | Required            | Description                                                                                                                          |
| ----------------- | ------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| project\_slug     | yes, as url segment | The slugified project name.                                                                                                          |
| form\_ref         | no                  | The ref used to identify a form. If this is not supplied, the first form form\_ref will be used by default.                          |
| uuid              | no                  | The unique identifier for a particular entry.                                                                                        |
| parent\_form\_ref | no                  | The form ref of a child form's parent.                                                                                               |
| parent\_uuid      | no                  | The uuid of a child entry's parent.                                                                                                  |
| map\_index        | no                  | The integer index of the particular mapping you want the data to be mapped against. The default mapping is used if none is supplied. |
| per\_page         | no                  | The number of entries to show per page. (integer, max 1000). Default is 50.                                                          |
| page              | no                  | The current page. (integer)                                                                                                          |
| sort\_by          | no                  | The column on which to sort.                                                                                                         |
| sort\_order       | no                  | The sort order for the entries: ASC (ascending) or DESC (descending).                                                                |
| filter\_by        | no                  | The column on which to filter.                                                                                                       |
| filter\_from      | no                  | The value to filter from.                                                                                                            |
| filter\_to        | no                  | The value to filter to.                                                                                                              |
| format            | no                  | Get the data in csv format                                                                                                           |
| headers           | no                  | Whether you need the csv headers.                                                                                                    |
| title             | no                  | A title to filter on ([**What is a title?**](https://docs.epicollect.net/formbuilder/title))                                         |

## Further Descriptions

### `project_slug`

The **project\_slug** is slugified version of the project name. Any spaces in the project name are replaced by a hyphen "-" to make it url safe. To retrieve it, check the **Developers** section on your project details page. From the same page you can download the full project definition in JSON format. It is used as a segment in the request url.

### `form_ref`

The **form\_ref** is a unique identifier assigned to each form. To retrieve it, check the **Developers** section on your project details page. From the same page you can download the full project definition in JSON format.

### `uuid`

The **uuid** is a unique identifier for an entry. To retrieve a uuid, check the `id` or `entry_uuid` attribute of an entry object.

### `parent_form_ref`

The **parent\_form\_ref** is the form ref of a parent form to which a child form is related. To retrieve it, check the **Developers** section on your project details page. From the same page you can download the full project definition in JSON format.

### `parent_uuid`

The **parent\_uuid** is a unique identifier for an entry to which a child or children entries are related. For example, if I have a University form entry "Imperial College", it may have 0, 1 or more Department form entries related to it, such as "DIDE", "Biology" etc and each of these child form entries will be related back to the parent entry via the **parent\_uuid**.

To retrieve this, check the `parent`.`data`.`parent_uuid` attribute of an entry object.

### `format`

Accepted values are `csv` or `json`. The default, if none is supplied, is `json`.

### `headers`

Whether to include headers when the format is `csv`. Accepted values are `true` or `false`. The default, if none is supplied, is `true`.

### Sorting

You can currently sort by the columns `created_at` and `uploaded_at` by "ASC" (ascending) or "DESC" (descending) order.

### Filtering

You can currently filter by the columns `created_at` and `uploaded_at`.\
You may choose a DATE value (in ISO 8601 format, like _2022-01-26T00:00:00.000_) on which to filter: "`filter_from`" (all the entries from a value), "`filter_to`" (all the values to a value) or "`filter_from`" and "`filter_to`" (all the entries between two values).

### Title

You can filter entries by their titles passing a search string.
