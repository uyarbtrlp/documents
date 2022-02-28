# Export a Full Model

### Introduction
This section describes how to **export a full model** which is stored in the CIM database (PSS®ODMS).

### Workflow Description
This function exports a full model as CIM/XML from the CIM database and stores the result in the filemanagement system. This function will return information about the file, which is created in the file management.
Following information is required in the request body:
- dbType: Enumeration of database type (1=Oracle, 2=MSSQL)
- serverName: Servername or Address
- schemaName: Schemaname of the ODMS instance on the server
- password: only if in use, default empty string
- operationId: this ID will be used internally to track the operation, it will also end up in the naming of the created file.

Following information is optional in the request body:
- profileType: Combination of profile IDs to filter by profiles
- modelAuthoritySet: Option to filter the model content by a single modeling authority set

### Function Description 
This section describes the necessary steps to use this function.

###### Endpoint
> POST /api/odms/model-management/export/full-xml

###### Authorization
- Authorization Type: "Bearer Token"
- Token: AccessToken [see here](../IdentityManagement/Authorization.md)

###### Parameters
no Parameters are used

###### Body
````JSON
{
  "dbType": 0,
  "serverName": "string",
  "schemaName": "string",
  "password": "string",
  "operationId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "profileType": 0,
  "modelAuthoritySet": "string"
}
````

###### Return
This function will return an object as described by the example object below.
````JSON
{
  "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "creationTime": "2021-04-27T07:45:02.543Z",
  "creatorId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "lastModificationTime": "2021-04-27T07:45:02.543Z",
  "lastModifierId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "fileId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "fileName": "string"
}
````