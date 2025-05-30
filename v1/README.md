# Social Pinpoint Classic API Documentation
This document outlines our JSON REST API that client can use to retrieve information in their projects. This API
requires authentication.

The Social Pinpoint Classic API is REST based and uses [JSON](http://www.json.org/) for serialisation and Basic Authentication
over SSL for authentication and encrypted communication. The access credentials of any admin user in the site account
in question can be used to access the API.

Non admin access is at present not available.

# Authentication Overview
The API is protected by Basic HTTP Authentication over SSL. You will be prompted in your browser when accessing our API
endpoints or you can provide them in your client of choice when connecting to the API.

An example providing basic authentication when using `curl` is shown below.

    curl -u user:password https://demo.mysocialpinpoint.com/api/v1/projects.json

# API Overview
The API base URL is

    https://<yoursubdomain>.mysocialpinpoint.com/api/v1

## Notes about id, url and links
Most resources have some form of linking properties to other resources. We have define these properties as

### id's
A property `id` will be the numeric id of the resource

A property `property_id` will be the numeric id of the associated property called `property`

### URL's
URL properties will be a URL linking to the json api url for that resource

For example, a property in a resource called `property_url` would link to something like `https://<yoursubdomain>.mysocialpinpoint.com/api/v1/someresource/<property_id>.json`

### Links
Link properties are actual URLs that link to non-api urls. For example, the `project.json` resource has a `project_link`

    "project_link": "https://demo.mysocialpinpoint.com/home",

# Paging
Various resources support paging. If the resource does then the paging details are returned in the response headers

    Link: <http://demo.lvh.me:3030/api/v1/comments.json?page=5>; rel="last", <http://demo.lvh.me:3030/api/v1/comments.json?page=2>; rel="next"
    Per-Page: 25
    Total: 209

Default page sizes are '25', but you can change this with URL param ```per_page```

    `GET /api/v1/projects.json?per_page=1000`

# Timestamp Format
Various resources support a timestamp paramter. The format should be in

    timestamp=2016-06-01

or

    timestamp=2016-06-01T00:00:00

# Resources
The various resources you can retrieve from our API are all documented below.

NOTE: These are examples and the data shown may not be internally consistent in each result. Use for reference only

- [Social Pinpoint Classic API Documentation](#social-pinpoint-api-documentation)
- [Authentication Overview](#authentication-overview)
- [API Overview](#api-overview)
  - [Notes about id, url and links](#notes-about-id-url-and-links)
    - [id's](#ids)
    - [URL's](#urls)
    - [Links](#links)
- [Paging](#paging)
- [Timestamp Format](#timestamp-format)
- [Resources](#resources)
  - [Projects](#projects)
    - [Markers](#markers)
    - [Comments](#comments)
    - [Information Markers](#information-markers)
    - [Surveys](#surveys)
    - [Survey Responses](#survey-responses)
    - [Marker Types](#marker-types)
    - [Tags](#tags)
    - [Zones](#zones)
    - [Statistics](#statistics)
  - [Stakeholders](#stakeholders)
  - [Users](#users)

## Projects
_Supports Paging_

Engagement activities are organised under projects.

For documentation see [our online documentation](http://wiki.socialpinpoint.com/display/Public/Project+Setup+-+Projects)

`GET /api/v1/projects.json` will return a list of all the projects associated with the site account

You can also specify a ``timestamp`` parameter and only projects with a ``created_at`` after that time will be returned

An example result

    [
      {
        "id": 3,
        "name": "Social Pinpoint ",
        "slug": "home",
        "created_at": "2013-06-09T20:07:29.280+10:00",
        "start_date": "2015-05-01T00:01:00.000+10:00",
        "end_date": "2015-09-30T23:59:00.000+10:00",
        "time_zone": "Australia/Sydney",
        "url": "https://demo.mysocialpinpoint.com/api/v1/projects/3.json",
        "project_link": "https://demo.mysocialpinpoint.com/home",
        "project_state": "Active",
        "map": {
          "max_bounds_ratio": "0.0",
          "lat": "-32.92852",
          "lng": "151.77396",
          "zoom": 15,
          "min_zoom": 11,
          "max_zoom": 25,
          "styles": "",
          "map_type": "Hybrid"
        }
      }
    ]


### Markers
_Supports Paging_

Markers are added to the map via users and also may contain information specifically added by administrators. The API
call will contain either the associated `comment` or `information_marker`

`GET /api/v1/projects/{project_id}/markers.json` will return all markers for the `{project_id}`

You can also specify a ``timestamp`` parameter and only markers with a ``published_at`` after that time will be returned

An example result

    [
      {
        "id": 1114,
        "lat": "-32.927455",
        "lng": "151.771799",
        "category_id": 55,
        "created_at": "2014-02-10T17:09:33.587+11:00",
        "published_at": "2014-04-02T17:09:00.000+11:00",
        "url": "https://demo.mysocialpinpoint.com/api/v1/projects/3/markers/1114.json",
        "comment": null,
        "info_marker": {
          "id": 375,
          "up_votes": 3,
          "down_votes": 0,
          "body": "<h2>Online Mapping for Community Engagement</h2><p><a href=\"http://www.socialpinpoint.com\">www.socialpinpoint.com</a></p>",
          "summary": "Social Pinpoint ",
          "marker_id": 1114,
          "published_at": "2014-04-02T17:09:00.000+11:00",
          "created_at": "2014-02-10T17:09:33.591+11:00",
          "photos": [
            {
              "url": "https://demo.mysocialpinpoint.com/uploads/photo/image/5/459/limited_size_SocialPinpoint_Landscape_Icon.jpg"
            }
          ]
        }
      },
      {
        "id": 775,
        "lat": "-32.927231",
        "lng": "151.772601",
        "category_id": 9,
        "created_at": "2013-10-24T14:54:05.696+11:00",
        "published_at": "2013-10-24T14:54:05.680+11:00",
        "url": "https://demo.mysocialpinpoint.com/api/v1/projects/3/markers/775.json",
        "comment": {
          "id": 485,
          "body": "This is my comment",
          "body_extra": "",
          "up_votes": 0,
          "down_votes": 0,
          "review_notes": "",
          "response_text": null,
          "ip_address": null,
          "stakeholder": {
                "id": 1245,
                "first_name": "",
                "last_name": null,
                "address": null,
                "suburb": null,
                "postcode": null,
                "state": null,
                "country": null,
                "email": "user@here.blah",
                "phone": null,
                "created_at": "2013-06-09T20:12:22.321+10:00"
              },
          "reviewed": false,
          "moderated": false,
          "marker_id": 775,
          "published_at": "2013-10-24T14:54:05.690+11:00",
          "created_at": "2013-10-24T14:54:05.741+11:00",
          "areas": "Planning Proposal Notification, NewcastleCBD, CBD"
        },
        "info_marker": null
      }
    ]

### Comments
_Supports Paging_

Comments are associated with a project and are attached to a georeferenced marker and stakeholder

`GET /api/v1/projects/{project_id}/comments.json` will return all comments for the `{project_id}`

You can also specify a ``timestamp`` parameter and only comments with a ``created_at`` after that time will be returned

You will notice there is a ``marker_url`` and ``parent_url`` attribute in comments

Comments can comment on other comments. Hence ``marker_url`` refers to the link back to the parent marker that the comment was made on.
``parent_url`` refers to the link of the parent of this comment. It could be a marker or a nother comment

Comments also contain a field called 'full_response' which aggregates body, body_extra and survey response text

An example result

    [
      {
          "id": 12162,
          "body": "This is a sample comment about why I love this area!",
          "body_extra": "",
          "up_votes": 1,
          "down_votes": 1,
          "review_notes": "",
          "response_text": "",
          "ip_address": "120.146.151.160",
          "reviewed": true,
          "moderated": false,
          "marker_id": 13562,
          "published_at": "2016-03-15T13:14:09.926+11:00",
          "created_at": "2016-03-15T13:14:10.001+11:00",
          "stakeholder": {
              "id": 1030,
              "first_name": "",
              "last_name": "",
              "address": "",
              "suburb": "",
              "postcode": "",
              "state": null,
              "country": null,
              "email": "charles@socialpinpoint.com",
              "phone": "",
              "created_at": "2013-06-26T09:39:41.882+10:00"
          },
          "photos": [
              {
                  "url": "https://s3-us-west-2.amazonaws.com/staging-myspp/uploads/photo/image/5/1292/limited_size_swing.jpg"
              }
          ],
          "areas": "Industrial, Area of Influence, Study Area",
          "url": "https://demo.staging-myspp.com/api/v1/projects/166/comments/12162.json",
          "parent_url": "https://demo.staging-myspp.com/api/v1/projects/166/markers/13562.json",
          "marker_url": "https://demo.staging-myspp.com/api/v1/projects/166/markers/13562.json",
          "marker_link": "https://demo.staging-myspp.com/land-use/map#/marker/13562",
          "marker_view_link": "https://demo.staging-myspp.com/markers/view/13562",
          "review_url": "https://demo.staging-myspp.com/admin/comments/12162/edit",
          "marker": {
              "id": 13562,
              "lat": "-33.764878",
              "lng": "151.260409",
              "category_id": 703,
              "created_at": "2016-03-15T13:14:09.960+11:00",
              "published_at": "2016-03-15T13:14:09.924+11:00"
          },
          "stakeholder_url": "https://demo.staging-myspp.com/api/v1/stakeholders/1030.json",
          "full_response": "This is a sample comment about why I love this area!\n\n\n"
      },
      ...
    ]

### Information Markers
Social Pinpoint Classic allows you to configure Admin (or Information) Markers that can only be selected/ dragged onto the map by Administrators when logged into the system and are useful for displaying information related to areas on the map.

For documentation see [our online documentation](http://wiki.socialpinpoint.com/x/KwAc)

`GET /api/v1/projects/{project_id}/info_markers.json` will return all markers for the `{project_id}`

An example result

    [
      {
        "id": 261,
        "up_votes": 3,
        "down_votes": 1,
        "body": "<p><strong>Proposed Tree Plantation Site</strong></p>\n\n<p>Improving the streetscape by planting trees? Why not inform the community about the project and allow stakeholders to have their say. </p>\n\n<p>Provide species information; <a href=\"https://demo.mysocialpinpoint.com/home\">links to more infomation</a> - inform and engage!</p>\n",
        "summary": "Proposed Tree Plantation Site",
        "marker_id": 736,
        "published_at": "2013-10-10T14:25:05.895+11:00",
        "created_at": "2013-10-10T14:25:05.907+11:00",
        "photos": [
          {
            "url": "https://demo.mysocialpinpoint.com/uploads/photo/image/5/333/limited_size_TullichSt_Services.png"
          }
        ],
        "url": "https://demo.mysocialpinpoint.com/api/v1/projects/3/info_markers/261.json",
        "marker_url": "https://demo.mysocialpinpoint.com/api/v1/projects/3/markers/736.json",
        "marker_link": "https://demo.mysocialpinpoint.com/home#marker/736",
        "marker": {
          "id": 736,
          "lat": "-32.928468",
          "lng": "151.776026",
          "category_id": 55,
          "created_at": "2013-10-10T14:25:05.903+11:00",
          "published_at": "2013-10-10T14:25:05.893+11:00"
        }
      },
      {
        "id": 536,
        "up_votes": 0,
        "down_votes": 0,
        "body": "",
        "summary": "First release of Geo-Survey functionality!",
        "marker_id": 2712,
        "published_at": "2014-08-14T15:02:00.000+10:00",
        "created_at": "2014-08-14T11:41:54.438+10:00",
        "survey": {
          "id": 10,
          "name": "Infrastructure",
          "questions": [
            {
              "id": 28,
              "name": "How important is it that you live close to the following? Please rank these items where 1= Most important and 5 = least important ",
              "required": false,
              "body": "How important is it that you live close to the following? Please rank these items where 1= Most important and 5 = least important ",
              "options": "Shops\r\nSchools\r\nHealth services\r\nRestaurants and cafes\r\nParks",
              "question_type": "Rank"
            },
            {
              "id": 29,
              "name": "Relationship to study area (select all that apply)",
              "required": false,
              "body": "Relationship to study area (select all that apply)",
              "options": "I live here\r\nI work here\r\nFrequent Visitor\r\nOther",
              "question_type": "Checkbox"
            }
          ]
        },
        "url": "https://demo.mysocialpinpoint.com/api/v1/projects/3/info_markers/536.json",
        "marker_url": "https://demo.mysocialpinpoint.com/api/v1/projects/3/markers/2712.json",
        "marker_link": "https://demo.mysocialpinpoint.com/home#marker/2712",
        "marker": {
          "id": 2712,
          "lat": "-32.928319",
          "lng": "151.769707",
          "category_id": 212,
          "created_at": "2014-08-14T11:41:54.351+10:00",
          "published_at": "2014-08-14T15:02:00.000+10:00"
        }
      }
    ]

### Surveys
Surveys allow structured feedback and can be attached to information markers or zones (polygons)

`GET /api/v1/projects/{project_id}/surveys.json' will return all configured surveys for the `{project_id}`

An example result

    [
      {
        "id": 251,
        "name": "Project Survey",
        "submit_url": "",
        "thank_you_message": "",
        "mail_body": "<p>Thanks for submitting a survey response</p>",
        "mail_subject": "Thanks for your response",
        "single_submit": false,
        "questions": [
            {
                "id": 841,
                "name": "Question 1",
                "required": false,
                "body": "How great is Social Pinpoint?",
                "options": "Awesome!\r\nSuper duper!\r\nI love it!",
                "inline": false,
                "sort_order": 1,
                "question_type": "Checkbox",
                "type_specific_data: {}
            },
            {
                "id": 893,
                "name": "Question 2",
                "required": false,
                "body": "This is a sample survey. Did you find this information useful?",
                "options": "",
                "inline": false,
                "sort_order": null,
                "question_type": "Text Area",
                "type_specific_data: {}
            }
        ],
        "survey_submit_action": "Submit then Close"
      }
    ]


### Survey Responses
_Supports Paging_

`GET /api/v1/projects/{project_id}/survey_responses.json` will return all configured surveys for the `{project_id}`

Survey Responses also contain a field called 'full_response' which aggregates survey response text

An example result

    [
      {
        "id": 5,
        "name": "Infrastructure",
        "stakeholder_url": "http://demo.lvh.me:3030/api/v1/stakeholders/834.json",
        "stakeholder": {
              "id": 834,
              "first_name": "",
              "last_name": "",
              "address": "",
              "suburb": "",
              "postcode": "",
              "state": null,
              "country": null,
              "email": "a@a.com",
              "phone": "",
              "created_at": "2014-06-03T13:34:46.481+10:00"
            },
        "survey_id": 1,
        "updated_at": "2014-08-26T16:45:40.806+10:00",
        "marker_id": 2712,
        "zone_id": null,
        "review_url": "http://demo.lvh.me:3030/admin/survey_responses/5/edit",
        "full_response": "Survey Response to: 'SampleSurvey-planningdemo'\n  1. Rate these\n  \n     - Affordable Housing\n\n     - Public Transport\n\n     - Jobs\n\n     - Education \n\n     - Environment\n\n  2. Question\n   - Did not answer\n  3. Ideas and Suggestions\n  \n     - \n\n"
        "survey_answers": [
          {
            "question_id":  1,
            "value": "Shops",
            "rank": 1
          },
          {
            "question_id":  1,
            "value": "Schools",
            "rank": 2
          },
          {
            "question_id":  1,
            "value": "Health services",
            "rank": 3
          },
          {
            "question_id":  1,
            "value": "Restaurants and cafes",
            "rank": 4
          },
          {
            "question_id":  1,
            "value": "Parks",
            "rank": 5
          },
          {
            "question_id":  2,
            "value": "I live here",
            "rank": null
          },
          {
            "question_id":  2,
            "value": "Other",
            "rank": null
          }
        ]
      }
    ]

### Marker Types
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
        "url": "https://demo.mysocialpinpoint.com/api/v1/projects/3/categories/9.json"
      },
      {
        "id": 10,
        "name": "Something I don't like",
        "marker_url": "markers/red-conversation-map-icon.png",
        "admin_marker": false,
        "hint_title": "Leave us your comment",
        "instruction": null,
        "url": "https://demo.mysocialpinpoint.com/api/v1/projects/3/categories/10.json"
      }
      ...
    ]

### Tags
Tags allow the moderator/reviewer to categorise comments at a finer level to Marker Types.

for document see [our online documentation](http://wiki.socialpinpoint.com/x/VgAV)

`GET /api/v1/projects/{project_id}/tags.json` will return all tags for the `{project_id}`

An example result

    [
      {
        "id": 79,
        "name": "Footpaths",
        "url": "https://demo.mysocialpinpoint.com/api/v1/projects/3/tags/79.json"
      },
      {
        "id": 80,
        "name": "Industrial",
        "url": "https://demo.mysocialpinpoint.com/api/v1/projects/3/tags/80.json"
      }
      ...
    ]

### Zones

`GET /api/v1/projects/{project_id}/zones.json` will return all tags for the `{project_id}`

An example result

    [
      {
        "id": 4,
        "name": "Growth Strategies",
        "colour": "#000000",
        "line_opacity": "0.4",
        "line_width": 4,
        "fill_colour": "#000000",
        "fill_opacity": "0.05",
        "created_at": "2013-06-09T05:09:54.364-05:00",
        "updated_at": "2017-10-31T16:19:14.061-05:00",
        "area_info": "",
        "viewable_in_legend": false,
        "clickable": false,
        "zindex": 400,
        "discussion": false,
        "allow_voting": false,
        "up_votes": 0,
        "down_votes": 0,
        "legend_stroke_colour": "#000000",
        "legend_fill_colour": "#000000",
        "legend_label": "Growth Strategies",
        "zone_select_action": 1,
        "select_url": null,
        "legend_fill_style": 1,
        "sidebar_tab": null,
        "legend_order": 400,
        "show_labels": false,
        "min_zoom": 11,
        "max_zoom": 15,
        "font_size": 24,
        "line_symbol": 0,
        "line_arrow_position": 0,
        "line_arrow_symbol": 0,
        "line_arrow_scale": 1,
        "line_symbol_scale": 1,
        "point_symbol_scale": 1,
        "label_font_color": "#000000",
        "label_stroke_color": "#ffffff",
        "label_stroke_weight": 4,
        "label_alignment": 2,
        "label_offset": 0,
        "legend_action_trigger": false,
        "points": [],
        "legend_group": null,
        "legend_symbol": null,
        "point_symbol": null,
        "replies": 0,
        "url": "http://demo.dev-myspp.com/api/v1/projects/3/zones/4.json"
      },
      {
        "id": 151,
        "name": "B - Hunter Street",
        "colour": "#d200ff",
        "line_opacity": "1.0",
        "line_width": 5,
        "fill_colour": "#d200ff",
        "fill_opacity": "0.0",
        "created_at": "2014-03-23T15:51:06.981-05:00",
        "updated_at": "2017-10-31T16:18:32.098-05:00",
        "area_info": "",
        "viewable_in_legend": true,
        "clickable": false,
        "zindex": 400,
        "discussion": false,
        "allow_voting": false,
        "up_votes": 0,
        "down_votes": 0,
        "legend_stroke_colour": "#d200ff",
        "legend_fill_colour": "#d200ff",
        "legend_label": "B - Hunter Street",
        "zone_select_action": 1,
        "select_url": "",
        "legend_fill_style": 1,
        "sidebar_tab": null,
        "legend_order": 400,
        "show_labels": false,
        "min_zoom": 11,
        "max_zoom": 15,
        "font_size": 24,
        "line_symbol": 0,
        "line_arrow_position": null,
        "line_arrow_symbol": 1,
        "line_arrow_scale": 1,
        "line_symbol_scale": 1,
        "point_symbol_scale": 1,
        "label_font_color": "#000000",
        "label_stroke_color": "#ffffff",
        "label_stroke_weight": 4,
        "label_alignment": 2,
        "label_offset": 0,
        "legend_action_trigger": false,
        "points": [],
        "legend_group": "Example Light Rail Options",
        "legend_symbol": "spp-icon-straight-line",
        "point_symbol": "",
        "replies": 0,
        "url": "http://demo.dev-myspp.com/api/v1/projects/3/zones/151.json"
      }
    ]

### Statistics
This is still to be implemented. We forsee this reporting various project metrics that are currently visible on the
admin dashboard

## Stakeholders
_Supports Paging_

The Stakeholder resource represents the end user who has left a comment or survey response. It contains information
about that stakeholder and the responses they have contributed to your account

`GET /api/v1/stakeholders.json` will return all stakeholders for your account

An example result

    [
      {
        "id": 10241,
        "first_name": "Colin",
        "last_name": "Goudie",
        "address": "10 Somewhere Street",
        "suburb": "Suburb",
        "postcode": "2222",
        "state": "NSW",
        "country": "Australia",
        "email": "colin@socialpinpoint.com",
        "phone": "xxx xxx xx",
        "created_at": "2016-12-06T14:28:53.416+11:00"
      },
      ...
    ]

## Users
Social Pinpoint Classic does not require public users to create an account to interact with the site. User accounts are only
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
