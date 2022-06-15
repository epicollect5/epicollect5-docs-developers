# Getting Branch Entries

We set up a project called [EC5 API Test](https://five.epicollect.net/project/ec5-api-test). The project is **public** so anyone can perform a GET request to fetch its entries.

Here is the response of the following GET endpoint, to retrieve all branch entries for a particular branch input: ([Open in browser](https://five.epicollect.net/api/export/entries/ec5-api-test?branch\_ref=d500a44b973e4de4a80fda57ca3dfe4d\_5901f6bb53273\_591ee7dc8400f))

```
https://five.epicollect.net/api/export/entries/ec5-api-test?branch_ref=d500a44b973e4de4a80fda57ca3dfe4d_5901f6bb53273_591ee7dc8400f
```

```
{
  "links": {
    "self": "https://five.epicollect.net/api/export/entries/ec5-api-test?form_ref=d500a44b973e4de4a80fda57ca3dfe4d_5901f6bb53273&parent_form_ref=&branch=&branch_ref=d500a44b973e4de4a80fda57ca3dfe4d_5901f6bb53273_591ee7dc8400f&branch_owner_uuid=&parent_uuid=&uuid=&input_ref=&per_page=50&sort_order=DESC&entry_col=created_at&map_index=&page=1",
    "first": "https://five.epicollect.net/api/export/entries/ec5-api-test?form_ref=d500a44b973e4de4a80fda57ca3dfe4d_5901f6bb53273&parent_form_ref=&branch=&branch_ref=d500a44b973e4de4a80fda57ca3dfe4d_5901f6bb53273_591ee7dc8400f&branch_owner_uuid=&parent_uuid=&uuid=&input_ref=&per_page=50&sort_order=DESC&entry_col=created_at&map_index=&page=1",
    "prev": null,
    "next": null,
    "last": "https://five.epicollect.net/api/export/entries/ec5-api-test?form_ref=d500a44b973e4de4a80fda57ca3dfe4d_5901f6bb53273&parent_form_ref=&branch=&branch_ref=d500a44b973e4de4a80fda57ca3dfe4d_5901f6bb53273_591ee7dc8400f&branch_owner_uuid=&parent_uuid=&uuid=&input_ref=&per_page=50&sort_order=DESC&entry_col=created_at&map_index=&page=1"
  },
  "meta": {
    "total": 4,
    "per_page": 50,
    "current_page": 1,
    "last_page": 1,
    "from": 1,
    "to": 1
  },
  "data": {
    "id": "ec5-api-test",
    "type": "entries",
    "entries": [
      {
        "ec5_branch_owner_uuid": "768bb179-fd2c-87b1-ec20-86a9acfdc87a",
        "ec5_branch_ref": "6_Family_Members",
        "created_at": "2017-05-19T12:51:41.674Z",
        "7_Name": "Andrew Carrey",
        "8_Age": 46
      },
      {
        "ec5_branch_owner_uuid": "39f51e6d-6438-76ba-e63c-82b6b387c041",
        "ec5_branch_ref": "6_Family_Members",
        "created_at": "2017-05-19T12:49:04.825Z",
        "7_Name": "Sally Fox",
        "8_Age": 28
      },
      {
        "ec5_branch_owner_uuid": "39f51e6d-6438-76ba-e63c-82b6b387c041",
        "ec5_branch_ref": "6_Family_Members",
        "created_at": "2017-05-19T12:48:57.512Z",
        "7_Name": "Bob Fox",
        "8_Age": 35
      },
      {
        "ec5_branch_owner_uuid": "39f51e6d-6438-76ba-e63c-82b6b387c041",
        "ec5_branch_ref": "6_Family_Members",
        "created_at": "2017-05-19T12:48:49.713Z",
        "7_Name": "Joe Fox",
        "8_Age": 40
      }
    ],
    "mapping": {
      "map_name": "custom",
      "map_index": 1
    }
  }
}
```

Here is the response of the following GET endpoint, to retrieve all branch entries for a particular branch input for a particular main entry: ([Open in browser](https://five.epicollect.net/api/export/entries/ec5-api-test?branch\_ref=d500a44b973e4de4a80fda57ca3dfe4d\_5901f6bb53273\_591ee7dc8400f\&branch\_owner\_uuid=39f51e6d-6438-76ba-e63c-82b6b387c041))

```
https://five.epicollect.net/api/export/entries/ec5-api-test?branch_ref=d500a44b973e4de4a80fda57ca3dfe4d_5901f6bb53273_591ee7dc8400f&branch_owner_uuid=39f51e6d-6438-76ba-e63c-82b6b387c041
```

```
{
  "links": {
    "self": "https://five.epicollect.net/api/export/entries/ec5-api-test?form_ref=d500a44b973e4de4a80fda57ca3dfe4d_5901f6bb53273&parent_form_ref=&branch=&branch_ref=d500a44b973e4de4a80fda57ca3dfe4d_5901f6bb53273_591ee7dc8400f&branch_owner_uuid=39f51e6d-6438-76ba-e63c-82b6b387c041&parent_uuid=&uuid=&input_ref=&per_page=50&sort_order=DESC&entry_col=created_at&map_index=&page=1",
    "first": "https://five.epicollect.net/api/export/entries/ec5-api-test?form_ref=d500a44b973e4de4a80fda57ca3dfe4d_5901f6bb53273&parent_form_ref=&branch=&branch_ref=d500a44b973e4de4a80fda57ca3dfe4d_5901f6bb53273_591ee7dc8400f&branch_owner_uuid=39f51e6d-6438-76ba-e63c-82b6b387c041&parent_uuid=&uuid=&input_ref=&per_page=50&sort_order=DESC&entry_col=created_at&map_index=&page=1",
    "prev": null,
    "next": null,
    "last": "https://five.epicollect.net/api/export/entries/ec5-api-test?form_ref=d500a44b973e4de4a80fda57ca3dfe4d_5901f6bb53273&parent_form_ref=&branch=&branch_ref=d500a44b973e4de4a80fda57ca3dfe4d_5901f6bb53273_591ee7dc8400f&branch_owner_uuid=39f51e6d-6438-76ba-e63c-82b6b387c041&parent_uuid=&uuid=&input_ref=&per_page=50&sort_order=DESC&entry_col=created_at&map_index=&page=1"
  },
  "meta": {
    "total": 3,
    "per_page": 50,
    "current_page": 1,
    "last_page": 1,
    "from": 1,
    "to": 1
  },
  "data": {
    "id": "ec5-api-test",
    "type": "entries",
    "entries": [
      {
        "ec5_branch_owner_uuid": "39f51e6d-6438-76ba-e63c-82b6b387c041",
        "ec5_branch_ref": "6_Family_Members",
        "created_at": "2017-05-19T12:49:04.825Z",
        "7_Name": "Sally Fox",
        "8_Age": 28
      },
      {
        "ec5_branch_owner_uuid": "39f51e6d-6438-76ba-e63c-82b6b387c041",
        "ec5_branch_ref": "6_Family_Members",
        "created_at": "2017-05-19T12:48:57.512Z",
        "7_Name": "Bob Fox",
        "8_Age": 35
      },
      {
        "ec5_branch_owner_uuid": "39f51e6d-6438-76ba-e63c-82b6b387c041",
        "ec5_branch_ref": "6_Family_Members",
        "created_at": "2017-05-19T12:48:49.713Z",
        "7_Name": "Joe Fox",
        "8_Age": 40
      }
    ],
    "mapping": {
      "map_name": "custom",
      "map_index": 1
    }
  }
}
```

As we did not pass any map parameter, by default the entries are mapped against the default EC5\_AUTO mapping.
