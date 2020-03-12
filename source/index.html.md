---
title: Smart Reference Data REST API

<!-- language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - ruby
  - python
  - javascript --> 

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  
  - errors
 

search: true
---

# Overivew

The *Smart Reference Data REST API* provides you with a convenient, and simple web services interface for interacting with Smart Reference Data database server. The REST APIs are designed to easily access Smart Reference Data database and perform key tasks, that include, insert, update, and retrieve operation.

The Intergraph Smart® Reference Data REST API Help explains the basics of using the REST APIs to access Smart Reference Data database server.

You will be able to perform insert, update, and retrieve operations on the following business objects:

* Projects
* Disciplines
* Nls
* Attributes
* Tables
* Geometrics
* Table Groups
* Table Details
* Commodity Rules
* Commodity Group
* Commodity Parts
* Commodity Codes
* Idents
* Company Idents
* Schedule Jobs

You will be able to perform retrieve operation on the following business objects:

* Specification Types
* Specification Headers
* Specification Header Details
* Specification Header Geometrics
   * Specification Header Notes
   * Specification Items
   * Specification Item Notes


# Authorization Architecture

A common OAuth allows a third-party client, such as PostMan web API, termed the client in the OAuth 2.0 specification, to operate on behalf of a user, without revealing that user’s credentials, such as user name and password, to the client. The client first sends the user credentials to an authorization server (Intergraph's Cloud9 service), which authenticates the user, obtains the user’s authorization, and issues an access token which the client can use in interacting with a resource server (Smart Reference Data database server)
![OAuth2.0](index.png)


`Authorization: Process Flow`

## Access Privileges

Access privileges allows you to perform read or write operations in Smart Reference Data using REST APIs. You must assign the following privileges for a user to access data in Smart Reference Data:

| Privilege          | Short Desc        | Description                 |
|--------------------|-------------------|-----------------------------|
| API_ATTRIBUTES_R   | View Attributes   | Allows to view attributes   |
| API_ATTRIBUTES_R/W | Create Attributes | Allows to create attributes |
| API_GEOMETRICS_R   | View Geometrics   | Allows to view geometrics   |
| API_GEOMETRICS_R/W | Create Geometrics | Allows to create geometrics |
| API_TABLES_R       | View Tables       | Allows to view tables       |
| API_TABLES_R/W     | Create Tables     | Allows to create tables     |

## Request access token

You must have the following key value pairs in the request Body to access the token:

| Key           | Value                         |
|---------------|-------------------------------|
| grant_type    | password                      |
| username      | user created in SAM           |
| password      | password for SAM user         |
| client_id     | client Id from SAM            |
| client_secret | client secret from SAM        |
| scope         | Smart API Service Id from SAM |

### HTTP Request

> The above command returns JSON structured like this:

```json
	{

  "access_token": "XXXXXXXX…",

  "expires_in": 86400,

  "token_type": "Bearer"

}
```
`POST https://samdev.ingrnet.com/sam/oauth/connect/token`

# API Discoverability

The following section helps you to find the available projects, disciplines, and the National Language Support (NLS) in Smart Reference Data database server.

**Standard URI format**

| Resource                  | Description                                            |
|---------------------------|--------------------------------------------------------|
| in-sprdapisrv.ingrnet.com | API Server where all the RESTFUL services are deployed |
| SRD713                    | Virtual directory on the API Server                    |
| Srd/V2                    | Route prefix                                           |
| client_id                 | client Id from SAM                                     |
| client_secret             | client secret from SAM                                 |
| scope                     | Smart API Service Id from SAM                          |

## Configure Web API

### Application settings

You must set the following configuration in the web.config file to consume from client service:

   * Open the web.config file, search for `Services baseUri`section, and set value for baseUri as:

`baseUri ="https://<ServerName>/<VirtualDirectoryName>"/>`

For example, if your server name is in-sprdapisrv.ingrnet.com, and the virtual directory name is SRD713, the `<baseUri>` must be:

  `<services baseUri=" https://in-sprdapisrv.ingrnet.com/SRD713"/>`

## Nullable Values

* For a nullable column, if no value is passed in the request body, the software replaces the column with the default value (if exists) else it is considered as NULL.

* For a mandatory column if no value is passed in the request body, the software replaces the column with the default value (if exists) else an appropriate message is shown.


