# Export an Incremental Model

### Introduction
This section describes how to **export an incremental model** which is stored in the CIM database (PSS®ODMS).

### Workflow Description
This function exports an incremental model as CIM/XML incremental from a model history and stores the result in the filemanagement system. This function will return information about the file, which is created in the file management.
Following information is required in the request body:
- dbType: Enumeration of database type (1=Oracle, 2=MSSQL)
- serverName: Servername or Address
- schemaName: Schemaname of the ODMS instance on the server
- operationId: this ID will be used internally to track the operation, it will also end up in the naming of the created file.
- password: only if in use, default empty string
- fromRevision: Revision ID for the original model
- toRevision: Revision ID of the changed model

Following information is optional in the request body:
- modelAuthoritySet: Option to filter the model content by a single modeling authority set

### Function Description 
This section describes the necessary steps to use this function.

###### Endpoint
> POST /api/odms/model-management/export/incremental-xml

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
  "fromRevision": 0,
  "toRevision": 0,
  "modelAuthoritySet": "string"
}
````

###### Return
This function will return an object as described by the example object below.
````JSON
{
  "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "creationTime": "2021-04-27T07:51:54.126Z",
  "creatorId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "lastModificationTime": "2021-04-27T07:51:54.126Z",
  "lastModifierId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "fileId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "fileName": "string"
}
````