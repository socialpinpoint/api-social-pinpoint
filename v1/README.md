# **Warning: Under Development**

# Social Pinpoint API Documentation
This document outlines our JSON REST API that client can use to retrieve information in their projects. This API
requires authentication.

The Social Pinpoint API is REST based and uses [JSON](http://www.json.org/) for serialisation and Basic Authentication
over SSL for authentication and encrypted communication. The access credentials of any admin user in the site account
in question can be used to access the API.

Non admin access is at present not available.


# Authentication Overview
The API is protected by Basic HTTP Authentication over SSL. You will be prompted in your browser when accessing our API
endpoints or you can provide them in your client of choice when connecting to the API.

An example providing basic authentication when using `curl` is shown below.

    curl -u user:password https://demo.ourcommunitymap.com/api/v1/projects.json

# API Overview
The API base URL is

    https://<yoursubdomain>.ourcommunitymap.com/api/v1

# Notes about id, url and links
Most resources have some form of linking properties to other resources. We have define these properties as

## id's
A property `id` will be the numeric id of the resource

A property `property_id` will be the numeric id of the associated property called `property`

## URL's
URL properties will be a URL linking to the json api url for that resource

For example, a property in a resource called `property_url` would link to something like `https://<yoursubdomain>.ourcommunitymap.com/api/v1/someresource/<property_id>.json`

## Links
Link properties are actual URLs that link to non-api urls. For example, the `project.json` resource has a `project_link`

    "project_link": "https://demo.ourcommunitymap.com/home",

# Resources
The various resources you can retrieve from our API are all documented below.

* [Projects](#projects)
    * [Comments](#comments)
* [Users](#Users)

## Projects
Engagement activities are organised under projects.

For documentation see [our online documentation](http://wiki.socialpinpoint.com/display/Public/Project+Setup+-+Projects)

`GET /api/v1/projects.json` will return a list of all the projects associated with the site account

An example result contains

    [
      {
        "id": 3,
        "name": "Social Pinpoint ",
        "slug": "home",
        "additional_confirmation_message": "We'd greatly appreciate a little further information in order to better understand your comment. Feel free to add any additional information in the area below.",
        "created_at": "2013-06-09T20:07:29.280+10:00",
        "start_date": "2014-07-01T00:00:00.000+10:00",
        "end_date": "2014-09-30T23:59:59.000+10:00",
        "time_zone": "Australia/Sydney",
        "max_bounds_ratio": "0.6",
        "region": "AU",
        "lat": "-32.927175",
        "lng": "151.770887",
        "zoom": 16,
        "min_zoom": 10,
        "max_zoom": 25,
        "styles": null,
        "url": "https://demo.ourcommunitymap.com/api/v1/projects/3.json",
        "project_link": "https://demo.ourcommunitymap.com/home",
        "project_state": "Active",
        "map_type": "Hybrid"
      }
    ]

### Comments
Comments are associated with a project and are attached to a geolocated marker

`GET /api/v1/projects/{project_id}/comments.json` will return all comments for the `{project_id}`

An example result contains

    {
        "id": 18,
        "body": "A very cost effective and proven method for effective consultation and collaboration",
        "body_extra": null,
        "up_votes": 4,
        "down_votes": 1,
        "review_notes": null,
        "response_text": null,
        "ip_address": null,
        "email": "user@here.blah",
        "firstname": "",
        "lastname": null,
        "phone": null,
        "postcode": null,
        "address": null,
        "suburb": null,
        "reviewed": true,
        "moderated": false,
        "marker_id": 18,
        "published_at": "2013-06-09T20:12:22.321+10:00",
        "created_at": "2013-06-09T20:12:22.353+10:00",
        "url": "https://demo.ourcommunitymap.com/api/v1/projects/3/comments/18.json",
        "marker_url": "https://demo.ourcommunitymap.com/api/v1/projects/3/markers/18.json",
        "marker_link": "https://demo.ourcommunitymap.com/home#marker/18"
      },
      {
        "id": 81,
        "body": "Community Issues are important - have your say!",
        "body_extra": "",
        "up_votes": 4,
        "down_votes": 1,
        "review_notes": "",
        "response_text": null,
        "ip_address": null,
        "email": "info@socialpinpoint.com",
        "firstname": "Fred",
        "lastname": "Smith",
        "phone": "",
        "postcode": "2302",
        "address": null,
        "suburb": null,
        "reviewed": true,
        "moderated": false,
        "marker_id": 81,
        "published_at": "2013-06-26T09:53:51.402+10:00",
        "created_at": "2013-06-26T09:53:51.437+10:00",
        "url": "https://demo.ourcommunitymap.com/api/v1/projects/3/comments/81.json",
        "marker_url": "https://demo.ourcommunitymap.com/api/v1/projects/3/markers/81.json",
        "marker_link": "https://demo.ourcommunitymap.com/home#marker/81"
      },
      ...
    ]


## Marker Types / Categories
Marker Types (or categories) define the type of comments that users can leave on a map and are associated directly with
a project.

For documentation see [our online documentation](http://wiki.socialpinpoint.com/x/UgAV)

`GET /api/v1/projects/{project_id}/categories.json` will return all marker types for the `{project_id}`

An example result

    [
      {
        "id": 9,
        "name": "Something I like",
        "marker_url": "markers/green-conversation-map-icon.png",
        "admin_marker": false,
        "hint_title": "Leave us your comment",
        "instruction": null,
        "url": "https://demo.ourcommunitymap.com/api/v1/projects/3/categories/9.json"
      },
      {
        "id": 10,
        "name": "Something I don't like",
        "marker_url": "markers/red-conversation-map-icon.png",
        "admin_marker": false,
        "hint_title": "Leave us your comment",
        "instruction": null,
        "url": "https://demo.ourcommunitymap.com/api/v1/projects/3/categories/10.json"
      }
      ...
    ]

## Users
Social Pinpoint does not require public users to create an account to interact with the site. User accounts are only
required for site Administrators so that they can login to the Admin site, have access to system setup, comment
moderation and review and export system data.

For documentation see [our online documentation](http://wiki.socialpinpoint.com/display/Public/Manage+Users)

`GET /api/v1/users.json` will return a list of all the administrator users associated with the site account

An example result

    [
      {
        "id": 9,
        "name": "Account Admin",
        "email": "demo@socialpinpoint.com",
        "roles": [
          {
            "name": "admin"
          },
          {
            "name": "super_admin"
          }
        ]
      }
    ]