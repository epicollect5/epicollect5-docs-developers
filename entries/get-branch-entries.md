# Get Branch Entries

Get the branch entries for a particular Branch in a Form for a Project, mapped using either your custom mapping or the EC5 AUTO mapping. If the project is private, an `access_token` must be provided (See: API Authentication).

We assume the base domain to be **five.epicollect.net**.

## HTTP REQUEST

`GET /api/export/entries/{project_slug}?{key=value&key=value...}`

## Query Parameters

| Parameter           | Required            | Description                                                                                                                  |
| ------------------- | ------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| project\_slug       | yes, as url segment | The slugified project name.                                                                                                  |
| branch\_ref         | yes                 | The ref of a branch input in a form.                                                                                         |
| branch\_owner\_uuid | no                  | The uuid of the entry which owns the branch entry/entries.                                                                   |
| form\_ref           | no                  | The ref used to identify a form. If this is not supplied, the first form form\_ref will be used by default.                  |
| uuid                | no                  | The unique identifier for a particular branch entry.                                                                         |
| map\_index          | no                  | The index of the particular mapping you want the data to be mapped against. The default mapping is used if none is supplied. |
| per\_page           | no                  | The number of entries to show per page. (max 1000).Default is 50.                                                            |
| page                | no                  | The current page.                                                                                                            |
| format              | no                  | The format of the exported data.                                                                                             |
| headers             | no                  | Whether to include headers or not.                                                                                           |
| sort\_by            | no                  | The column on which to sort.                                                                                                 |
| sort\_order         | no                  | The sort order for the entries: ASC (ascending) or DESC (descending).                                                        |
| filter\_by          | no                  | The column on which to filter.                                                                                               |
| filter\_from        | no                  | The value to filter from.                                                                                                    |
| filter\_to          | no                  | The value to filter to.                                                                                                      |

## Further Descriptions

### `project_slug`

The **project\_slug** is slugified version of the project name. Any spaces in the project name are replaced by a hyphen "-" to make it URL safe. To retrieve it, check the **Developers** section on your project details page. From the same page, you can download the full project definition in JSON format. It is used as a segment in the request URL.

### `branch_ref`

The **branch\_ref** is the reference of the branch input question attached to a form. To retrieve it, check the **Developers** section on your project details page. From the same page you can download the full project definition in JSON format.

Supplying this will return all entries for a particular branch input, regardless of the main entry to which each branch entry is associated.

### `branch_owner_uuid`

The **branch\_owner\_uuid** is a unique identifier for an entry to which a branch entry/entries are associated. For example, if I have a Person form entry "Mr Doe", it may have 0, 1 or more Family Members branch entries associated with it, such as "Mrs Doe", "Miss Doe" etc and each of these branch form entries will be associated back to the main entry via the branch\_owner\_uuid.

Supplying this, along with the **branch\_ref**, will return all entries for a particular branch input for a particular main entry.

To retrieve this, check the `branch`.`data`.`branch_owner_uuid` attribute of a branch entry object.

### `form_ref`

The **form\_ref** is a unique identifier assigned to each form. To retrieve it, check the **Developers** section on your project details page. From the same page you can download the full project definition in JSON format.

### `uuid`

The **uuid** is a unique identifier for a branch entry. To retrieve a uuid, check the `id` or `entry_uuid` attribute of a branch entry object.

### `format`

Accepted values are `csv` or `json`. The default, if none is supplied, is `json`.

### `headers`

Whether to include headers when the format is `csv`. Accepted values are `true` or `false`. The default, if none is supplied, is `true`.

### Sorting

You can currently sort by the columns `created_at` and `uploaded_at` by "ASC" (ascending) or "DESC" (descending) order.

### Filtering

You can currently filter by the columns `created_at` and `uploaded_at`.\
You may choose a DATE value on which to filter: "`filter_from`" (all the entries from a value), "`filter_to`" (all the values to a value) or "`filter_from`" and "`filter_to`" (all the entries between two values).
