---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - ruby

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - operators

search: true
---

# Introduction

Welcome to the DHIS2 API! You can use our API to access all data in DHIS2 and actually execute any action possible through the UX.

The examples are using DHIS2 demo version at https://play.dhis2.org/demo/ - just replace the URL with your own.

We have language bindings in Shell and Ruby. You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

This example API documentation page was created with [Slate](https://github.com/tripit/slate).

# Authentication

> To authorize, use this code:

```ruby
require 'dhis2'

client = Dhis2::Client.new(url: "https://play.dhis2.org/demo", user: "admin", password: "district")
```

```shell
# With shell, you can just pass the user and password with each request
curl -u "admin:district" https://play.dhis2.org/demo/api/resources

```

> Make sure to replace `admin:district` with your owner user and password accordingly.

<aside class="notice">
You must replace <code>admin:district</code> with your personal user and password.
</aside>

# Meta data

Most meta data are accessible through the same methods and parameters. Meta includes:

- Organisation Units, Groups and Group Sets
- Data Elements and Groups
- Data Sets
- Indicators and Groups
- ...

Initial examples here use Organisation Units.

## Pagination

All the following commands return paginated results, starting with an header. Page size can be sent as parameters, and it's possible to disable paging altogether.

```shell
{
  "pager": {
    "page":1,
    "pageCount":36,
    "total":1797,
    "pageSize":50,
    "nextPage":"https://play.dhis2.org/demo/api/organisationUnits?page=2"
  }
}
```

```ruby
  org_units = Dhis2.client.organisation_units.list
  org_units.pager.page       # current page
  org_units.pager.page_count # number of pages
  org_units.pager.total      # number of records
```

## Get All Organisation Units

```ruby
require 'dhis2'

client = Dhis2::Client.new(url: "https://play.dhis2.org/demo", user: "admin", password: "district")
all = client.organisation_units.list

=> [#<Dhis2::Api::OrganisationUnit id="fp53yNbjYaN", display_name="1", children_ids=[]>,
 #<Dhis2::Api::OrganisationUnit id="GhRejc2KYSl", display_name="2", children_ids=[]>, ...]
```

```shell
curl -u "admin:district" https://play.dhis2.org/demo/api/organisationUnits

> The above command returns JSON structured like this:

{
  "pager": {
    "page":1,
    "pageCount":36,
    "total":1797,
    "pageSize":50,
    "nextPage":"https://play.dhis2.org/demo/api/organisationUnits?page=2"
  },
  "organisationUnits":[
    {
      "id":"htiTioI7WGO",
      "displayName":"ABBA_CS_RS2"
    },
    {
      "id":"A17jXi1Y3W6",
      "displayName":"ADECOM_RS7"
    }, 
    ... 
  ]
}
```

This endpoint retrieves all organisation units. Note that results are paginated by default (default page size: 50)

### HTTP Request

`GET https://play.dhis2.org/demo/api/organisationUnits`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
fields | [id,displayName] | Fields to retreive for each organisation unit.
filter | none | Restriction on the set returned.

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint retrieves a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete

