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
        "max_bounds_ratio": "0.6",
        "region": "AU",
        "additional_confirmation_message": "We'd greatly appreciate a little further information in order to better understand your comment. Feel free to add any additional information in the area below.",
        "lat": "-32.927175",
        "lng": "151.770887",
        "zoom": 16,
        "min_zoom": 10,
        "max_zoom": 25,
        "project_state": 2,
        "map_type": 3,
        "styles": null,
        "url": "http://demo.lvh.me:3000/api/projects/3.json",
        "project_url": "http://demo.lvh.me:3000/home"
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