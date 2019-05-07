# ![LOGO](logo.png) OpenFinTech.io **flow**ground Connector

## Description

A generated **flow**ground connector for the OpenFinTech.io API (version 2017-08-24).

Generated from: https://api.apis.guru/v2/specs/openfintech.io/2017-08-24/swagger.json<br/>
Generated at: 2019-05-07T17:43:26+03:00

## API Description

# Introduction
[OpenFinTech.io](https://openfintech.io) is an open database that comprises of standardized primary data for FinTech industry.<br>
It contains such information as geolocation data (countries, cities, regions), organizations, currencies (national, digital, virtual, crypto), banks, digital exchangers, payment providers (PSP), payment methods, etc.<br>
It is created for communication of cross-integrated micro-services on "one language". This is achieved through standardization of entity identifiers that are used to exchange information among different services.<br>

### UML
UML Domain Model diagram you can find [here](https://api.openfintech.io/public_domain_model.png).<br>

### Persistence
Entities are updated not more than 1 time per day.<br>

### Terms and Conditions
This *OpenFinTech.io* is made available under the [Open Database License](http://opendatacommons.org/licenses/odbl/1.0/).<br>
Any rights in individual contents of the database are licensed under the [Database Contents License](http://opendatacommons.org/licenses/dbcl/1.0/).<br>

### Contacts
For any questions, please email - info@openfintech.io<br>
Or you can contact us at <a href="https://gitter.im/paymaxicom/openfintech.io">Gitter</a><br>

Powered by [Paymaxi](https://www.paymaxi.com)

# Get Started

If you use [POSTMAN](https://www.getpostman.com) or similar program which can operate with swagger`s files - just [download](https://docs.openfintech.io) our spec and [import it](https://www.getpostman.com/docs/importing_swagger). Also you can try live [API demo](https://api.openfintech.io).

## Overview

The OpenFinTech API is organized around [REST](https://en.wikipedia.org/wiki/Representational_state_transfer). Our API has predictable, resource-oriented URLs, and uses HTTP response codes to indicate API errors.<br>
API is based on [JSON API](http://jsonapi.org) standard. JSON is returned by all API responses, including errors, although our API libraries convert responses to appropriate language-specific objects.<br>
JSON API requires use of the JSON API media type (`application/vnd.api+json`) for exchanging data.<br>
### Additional Request Headers
#### ACCEPT HEADER
Your requests should always include the header:
```curl
Accept: application/vnd.api+json
```

## Authentication

To use OpenFinTech API no needed authorization.

## Versioning

When we make changes to the API, we release new, dated versions. The current version is **2017-08-24**. Read our [API upgrades guide]() to see our API changelog and to learn more about backwards compatibility.

## Pagination

OpenFinTech APIs to retrieve lists of banks, currencies and other resources - paginated to **100** items by default. The pagination information will be included in the list API response under the node name `meta` - contains information about listed objects [`total` - contains information about total count of listed objects, `pages` - count of pages], `links` - contain links to navigate between pages [`first` - link to first page, `prev` - link to previous page, `next` - link to next page, `last` - link to last page].<br>
By default first page will be listed. For navigating through pages, use the page parameter (e.g. `page[number]`, `page[size]`).<br>
The `page[size]` parameter can be used to set the number of records that you want to receive in the response.<br>
The `page[number]` parameter can be used to set needed page number.<br>
Example of response:
```json
{
  "meta": {
    "total": 419,
    "pages": 42
  },
  "links": {
    "first": "/v1/{path}?page[number]=1&page[size]=10",
    "prev": "/v1/{path}?page[number]=39&page[size]=10",
    "next": "/v1/{path}?page[number]=41&page[size]=10",
    "last": "/v1/{path}?page[number]=42&page[size]=10"
  }
```

### Sorting

OpenFinTech\`s API supported query parameter to sort result collection [e.g. `?sort=code`]. Information about available parameters may be found in the endpoint description. Positive parameter [e.g. `?sort=code`] points to ascending sorting, negative  [e.g. `?sort=-code`] - to descending sorting. Also, supported multiple sorting parameters [e.g. `?sort=code, -name, id`, etc.]
```curl
https://api.openfintech.io/v1/countries?sort=name,-area
```

### Filtering

Filtering provided by unique query key `filter[*filtering_condition*]`. Information about available parameters may be found in the endpoint description.
```curl
https://api.openfintech.io/v1/countries?filter[region]=europe
```

## Images

OpenFinTech provides two types of images: icons and logos. To get one of those types you should to use next url pattern:
``` curl
https://api.openfintech.io/v1/{path}/{id}/{icon/logo}
```
Also, images can be resized by adding next parameters: `h={height}&w={width}`. For example, you want to get organization icon with width equals to 20 pixels:
``` curl
https://api.openfintech.io/v1/organizations/{id}/icon?w=20&h=20
```
If argument height or width is missing API returns original image with real sizes.

## Errors

API uses conventional HTTP response codes to indicate the success or failure of an API request. In general, codes in the `2xx` range indicate success, codes in the `4xx` range indicate an error that failed given the information provided (e.g., a required parameter was omitted, etc.), and codes in the `5xx` range indicate an error with OpenFinTech's servers (these are rare).

| Code | Description |
|------|-------------|
| 200 - OK	| Everything worked as expected. |
| 400 - Bad Request |	The request was unacceptable, often due to missing a required parameter. |
| 401 - Unauthorized |	No valid API key provided. |
| 402 - Request Failed	| The parameters were valid but the request failed. |
| 404 - Not Found |	The requested resource doesn't exist. |
| 409 - Conflict	| The request conflicts with another request (perhaps due to using the same idempotent key). |
| 429 - Too Many Requests |	Too many requests hit the API too quickly. We recommend an exponential backoff of your requests. |
| 500, 502, 503, 504 - Server Errors |	Something went wrong on OpenFinTech's end. (These are rare.) |


## Authorization

This API does not require authorization.

## Actions

### List of banks

> Returns list of banks. Each object contains general information about bank such as name and status, also information about bank details and related link to main organization.

*Tags:* `Banks`

#### Input Parameters
* `page[number]` - _optional_ - Current page number.
* `page[size]` - _optional_ - Page size.<br>*Default value: 100*

* `filter[sort_code]` - _optional_ - Filtering by banks code.
* `filter[code]` - _optional_ - Filtering by code.
* `filter[status]` - _optional_ - Filtration by status.
* `sort` - _optional_ - Sort params:<br>

| ASC | DESC |
|-----|------|
| name | -name |
| code | -code |
| status | -status |
| sort_code | -sort_code |


### Bank by ID

> Returns bank with specific ID.

*Tags:* `Banks`

#### Input Parameters
* `id` - _required_ - Unique ID.

### List of countries

> Returns all available countries.

*Tags:* `Countries`

#### Input Parameters
* `page[number]` - _optional_ - Current page number.
* `page[size]` - _optional_ - Page size.<br>*Default value: 100*

* `filter[region]` - _optional_ - Filtration by region.
* `filter[sub_region]` - _optional_ - Filtration by sub region.
* `sort` - _optional_ - Sort params:<br>

| ASC | DESC |
|-----|------|
| name | -name |
| area | -area |
| population | -population |
| region | -region |
| sub_region | -sub_region |


### Country by ID

> Returns country with specific ID.

*Tags:* `Countries`

#### Input Parameters
* `id` - _required_ - Unique ID.

### List of currencies

> Returns all available currencies.

*Tags:* `Currencies`

#### Input Parameters
* `page[number]` - _optional_ - Current page number.
* `page[size]` - _optional_ - Page size.<br>*Default value: 100*

* `filter[search]` - _optional_ - Full text search with name, code, type, code_iso_alpha3, code_jsons_alpha, code_estandards_alpha, category.
* `filter[code_iso_alpha3]` - _optional_ - Filtering by ISO code.
* `filter[code_iso_numeric3]` - _optional_ - Filtering by ISO number.
* `filter[code_estandards_alpha]` - _optional_ - Filtering by estandards code.
* `filter[currency_type]` - _optional_ - Filtration by currency type.
* `filter[category]` - _optional_ - Filtration by category.
* `sort` - _optional_ - Sort params:<br>

| ASC | DESC |
|-----|------|
| name | -name |
| type | -type |
| category | -category |
| code | -code |
| code_iso_alpha3 | -code_iso_alpha3 |
| code_iso_numeric3 | -code_iso_numeric3 |
| code_estandards_alpha | -code_estandards_alpha |


### Currency by ID

> Returns currency with specific ID.

*Tags:* `Currencies`

#### Input Parameters
* `id` - _required_ - Unique ID.

### List of deposit methods

> Returns list of deposit methods. Each object contains information about deposit method such as name and category, also related link to deposit method issuer (which processing it).

*Tags:* `Deposit methods`

#### Input Parameters
* `page[number]` - _optional_ - Current page number.
* `page[size]` - _optional_ - Page size.<br>*Default value: 100*

* `filter[search]` - _optional_ - Full text search with id, name, code, category.
* `filter[name]` - _optional_ - Filtering by name.
* `filter[code]` - _optional_ - Filtering by code.
* `filter[processor_name]` - _optional_ - Filtering by processor_name.
* `filter[category]` - _optional_ - Filtering by category.
* `sort` - _optional_ - Sort params:<br>

| ASC | DESC |
|-----|------|
| name | -name |
| code | -code |
| processor_name | -processor_name |
| category | -category |


### Deposit method by ID

> Returns deposit method with specific ID.

*Tags:* `Deposit methods`

#### Input Parameters
* `id` - _required_ - Unique ID.

### List of exchangers

> Returns list of exchange markets. Each object contains general information about exchanger such as name and status, also information about rates export and related link to main organization.<br><br/>
> Rates export standards is represented by:<br/>
> * [estandards](http://estandards.info)<br/>
> * [jsons](http://jsons.info)<br/>
> * ratex - our internal standard

*Tags:* `Exchangers`

#### Input Parameters
* `page[number]` - _optional_ - Current page number.
* `page[size]` - _optional_ - Page size.<br>*Default value: 100*

* `filter[name]` - _optional_ - Filtering by name.
* `filter[status]` - _optional_ - Filtration by status.
* `sort` - _optional_ - Sort params:<br>

| ASC | DESC |
|-----|------|
| name | -name |
| status | -status |
| wmid | -wmid |
| rate_type | -rate_type |
| rates_export_standard | <nobr>-rates_export_standard</nobr> |


### Exchanger by ID

> Returns exchanger with specific ID.

*Tags:* `Exchangers`

#### Input Parameters
* `id` - _required_ - Unique ID.

### List of merchant industries

> Returns all available merchant fields of activity.

*Tags:* `Merchant industries`

#### Input Parameters
* `page[number]` - _optional_ - Current page number.
* `page[size]` - _optional_ - Page size.<br>*Default value: 100*

* `filter[name]` - _optional_ - Filtering by name.

### Merchant industry by ID

> Returns merchant industry with specific ID.

*Tags:* `Merchant industries`

#### Input Parameters
* `id` - _required_ - Unique ID.

### List of organizations

> This endpoint retrievs the list of organizations present in the system. The data displays general, public information, without reference to the type of activity (for example - name, address, contacts, etc.).

*Tags:* `Organizations`

#### Input Parameters
* `page[number]` - _optional_ - Current page number.
* `page[size]` - _optional_ - Page size.<br>*Default value: 100*

* `filter[search]` - _optional_ - Full text search with id, name, code.
* `filter[name]` - _optional_ - Filtering by name.
* `filter[code]` - _optional_ - Filtering by code.
* `filter[status]` - _optional_ - Filtration by status.
* `filter[industries]` - _optional_ - Filtering by industries.
* `sort` - _optional_ - Sort params:<br>

| ASC | DESC |
|-----|------|
| name | -name |
| code | -code |
| status | -status |
| description | -description |


### Organization by ID

> Returns organization with specific ID.

*Tags:* `Organizations`

#### Input Parameters
* `id` - _required_ - Unique ID.

### List of payment methods

> Returns list of payment methods. Each object contains information about payment method such as name and category, also related link to payment method issuer (which processing it).

*Tags:* `Payment methods`

#### Input Parameters
* `page[number]` - _optional_ - Current page number.
* `page[size]` - _optional_ - Page size.<br>*Default value: 100*

* `filter[search]` - _optional_ - Full text search with id, name, code, category.
* `filter[name]` - _optional_ - Filtering by name.
* `filter[code]` - _optional_ - Filtering by code.
* `filter[processor_name]` - _optional_ - Filtering by processor_name.
* `filter[category]` - _optional_ - Filtering by category.
* `sort` - _optional_ - Sort params:<br>

| ASC | DESC |
|-----|------|
| name | -name |
| code | -code |
| processor_name | -processor_name |
| category | -category |


### Payment method by ID

> Returns payment method with specific ID.

*Tags:* `Payment methods`

#### Input Parameters
* `id` - _required_ - Unique ID.

### List of payment providers

> A payment service provider (PSP) offers shops online services for accepting electronic payments by a variety of payment methods.<br> Endpoint returns list of PSPs. Each object contains: name, type, supported features and sales channels, also related link to available payment methods and main organization.

*Tags:* `Payment providers`

#### Input Parameters
* `page[number]` - _optional_ - Current page number.
* `page[size]` - _optional_ - Page size.<br>*Default value: 100*

* `filter[search]` - _optional_ - Full text search with id, code, name.
* `filter[name]` - _optional_ - Filtering by name.
* `filter[code]` - _optional_ - Filtering by code.
* `filter[types]` - _optional_ - Filtering by types.
* `filter[sales_channels]` - _optional_ - Filtering by sales channels.
* `filter[features]` - _optional_ - Filtering by features.
* `sort` - _optional_ - Sort params:<br>

| ASC | DESC |
|-----|------|
| name | -name |
| code | -code |


### Payment provider by ID

> Returns payment provider with specific ID.

*Tags:* `Payment providers`

#### Input Parameters
* `id` - _required_ - Unique ID.

## License

**flow**ground :- Telekom iPaaS / openfintech-io-connector<br/>
Copyright © 2019, [Deutsche Telekom AG](https://www.telekom.de)<br/>
contact: flowground@telekom.de

All files of this connector are licensed under the Apache 2.0 License. For details
see the file LICENSE on the toplevel directory.
