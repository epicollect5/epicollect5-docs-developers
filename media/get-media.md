# Get Media

Get the Project logo image or the media for a particular Entry Answer in a Project. If the project is private, an `access_token` must be provided (See: API Authentication).

We assume the base domain to be **five.epicollect.net**.

## HTTP REQUEST

`GET /api/export/media/{project_slug}?{key=value&key=value...}`

## Query Parameters

| Parameter     | Required            | Description                 |
| ------------- | ------------------- | --------------------------- |
| project\_slug | yes, as url segment | The slugified project name. |
| type          | yes                 | The type of media.          |
| format        | yes                 | The format of the media.    |
| name          | yes                 | The name of the media.      |

## Further Descriptions

### `project_slug`

The **project\_slug** is slugified version of the project name. Any spaces in the project name are replaced by a hyphen "-" to make it url safe. To retrieve it, check the **Developers** section on your project details page. From the same page you can download the full project definition in JSON format. It is used as a segment in the request url.

### `type`

The **type** must be one of the following: `photo`, `audio` or `video`.

### `format`

The **format** must be one of following, depending on the **type**:

| Format                | Type  | Description                       | Resolution |
| --------------------- | ----- | --------------------------------- | ---------- |
| project\_thumb        | photo | The Project logo thumbnail image. | 512x512px  |
| project\_mobile\_logo | photo | The Project logo mobile image.    | 128x128px  |
| entry\_original       | photo | The entry original photo image.   | 1024x768px |
| entry\_thumb          | photo | The entry photo thumbnail image.  | 100x100px  |
| entry\_sidebar        | photo | The entry photo sidebar image.    | 400x300px  |
| audio                 | audio | The entry original audio.         | n/a        |
| video                 | video | The entry original video.         | n/a        |

### `name`

The **name** is the name of the media file.\
For the project logo, this will be `logo.jpg`.\
For entry media, this will be the entry answer.
