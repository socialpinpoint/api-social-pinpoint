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

    curl -u user:password https://demo.ourcommunitymap.com/api/project.json

# API Overview
The API base URL is

    https://<yoursubdomain>.ourcommunitymap.com/api

# Resources
The various resources you can retrieve from our API are all documented below.

* [Projects](#projects)
    * [Comments](#comments)
* [Users](#Users)

## Projects
Engagement activities are organised under projects.

For documentation see [our online documentation](http://wiki.socialpinpoint.com/display/Public/Project+Setup+-+Projects)

`GET /api/projects.json` will return a list of all the projects associated with the site account

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
        "map_type": 3,
        "styles": null,
        "url": "http://demo.lvh.me:3000/api/projects/3.json",
        "project_url": "http://demo.lvh.me:3000/home",
        "project_state": "Active"
      }
    ]

### Comments
Comments are associated with a project and are attached to a geolocated marker

`GET /api/projects/{project_id}/comments.json` will return all comments for the `{project_id}`

An example result contains

    [
      {
        "id": 18,
        "body": "A very cost effective and proven method for effective consultation and collaboration",
        "up_votes": 4,
        "down_votes": 1,
        "response_text": null,
        "marker_id": 18,
        "published_at": "2013-06-09T20:12:22.321+10:00",
        "created_at": "2013-06-09T20:12:22.353+10:00"
      },
      {
        "id": 81,
        "body": "Community Issues are important - have your say!",
        "up_votes": 4,
        "down_votes": 1,
        "response_text": null,
        "marker_id": 81,
        "published_at": "2013-06-26T09:53:51.402+10:00",
        "created_at": "2013-06-26T09:53:51.437+10:00"
      },
      {
        "id": 2176,
        "body": "Great tool!",
        "up_votes": 0,
        "down_votes": 0,
        "response_text": null,
        "marker_id": 2782,
        "published_at": "2014-08-15T11:41:10.502+10:00",
        "created_at": "2014-08-15T11:41:10.586+10:00"
      },
      {
        "id": 129,
        "body": "New Marker Type! Admin users can now add Information messages/ photos onto the project area.",
        "up_votes": 4,
        "down_votes": 2,
        "response_text": null,
        "marker_id": 129,
        "published_at": "2013-07-22T10:39:03.251+10:00",
        "created_at": "2013-07-22T10:39:03.295+10:00"
      }
    ]


## Users
Social Pinpoint does not require public users to create an account to interact with the site. User accounts are only
required for site Administrators so that they can login to the Admin site, have access to system setup, comment
moderation and review and export system data.

For documentation see [our online documentation](http://wiki.socialpinpoint.com/display/Public/Manage+Users)

`GET /api/users.json` will return a list of all the administrator users associated with the site account

An example result contains

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