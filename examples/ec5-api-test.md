# Getting Entries

We set up a project called [EC5 API Test](https://five.epicollect.net/project/ec5-api-test). The project is **public** so anyone can perform a GET request to fetch its entries.

Here is the response of the following GET endpoint: ([Open in browser](https://five.epicollect.net/api/export/entries/ec5-api-test))

```
https://five.epicollect.net/api/export/entries/ec5-api-test
```

```
{
  "links": {
    "self": "https://five.epicollect.net/api/export/entries/ec5-api-test?form_ref=d500a44b973e4de4a80fda57ca3dfe4d_5901f6bb53273&parent_form_ref=&branch=&branch_ref=&branch_owner_uuid=&parent_uuid=&uuid=&input_ref=&per_page=50&sort_order=DESC&entry_col=created_at&map_index=&page=1",
    "first": "https://five.epicollect.net/api/export/entries/ec5-api-test?form_ref=d500a44b973e4de4a80fda57ca3dfe4d_5901f6bb53273&parent_form_ref=&branch=&branch_ref=&branch_owner_uuid=&parent_uuid=&uuid=&input_ref=&per_page=50&sort_order=DESC&entry_col=created_at&map_index=&page=1",
    "prev": null,
    "next": null,
    "last": "https://five.epicollect.net/api/export/entries/ec5-api-test?form_ref=d500a44b973e4de4a80fda57ca3dfe4d_5901f6bb53273&parent_form_ref=&branch=&branch_ref=&branch_owner_uuid=&parent_uuid=&uuid=&input_ref=&per_page=50&sort_order=DESC&entry_col=created_at&map_index=&page=1"
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
        "ec5_uuid": "39f51e6d-6438-76ba-e63c-82b6b387c041",
        "created_at": "2017-04-27T14:42:04.080Z",
        "1_Name": "Megan Fox",
        "2_Age": 30,
        "3_Date_of_birth": "16/05/1986",
        "4_Sex": "Female",
        "5_Photo": "https://five.epicollect.net/api/media/ec5-api-test?type=photo&format=entry_original&name=39f51e6d-6438-76ba-e63c-82b6b387c041_1493304122.jpg"
      },
      {
        "ec5_uuid": "768bb179-fd2c-87b1-ec20-86a9acfdc87a",
        "created_at": "2017-04-27T14:38:17.564Z",
        "1_Name": "Jim Carrey",
        "2_Age": 55,
        "3_Date_of_birth": "17/01/1962",
        "4_Sex": "Male",
        "5_Photo": "https://five.epicollect.net/api/media/ec5-api-test?type=photo&format=entry_original&name=768bb179-fd2c-87b1-ec20-86a9acfdc87a_1493303895.jpg"
      },
      {
        "ec5_uuid": "e83d3770-2b55-11e7-a60a-656c7ec627a0",
        "created_at": "2017-04-27T14:29:22.663Z",
        "1_Name": "Nicholas Cage",
        "2_Age": 53,
        "3_Date_of_birth": "07/01/2017",
        "4_Sex": "Male",
        "5_Photo": "https://five.epicollect.net/api/media/ec5-api-test?type=photo&format=entry_original&name=e83d3770-2b55-11e7-a60a-656c7ec627a0_1493303578.jpg"
      }
    ],
    "mapping": {
      "map_name": "EC5_AUTO",
      "map_index": 0
    }
  }
}
```

Since we did not pass any map parameter, by default the entries are mapped against the default EC5\_AUTO mapping.

The `links` and `meta` properties contains info about how many entries there are in total and the endpoints to get the next set. By default the **entries are paginated by 50 at a time,** so you will have to write a loop to get all of them by using the `links.next` enpoint until is `null`. In the above example it is `null` already as we only have a few entries.
