# Get Model by ID

### Introduction
This section describes how to **get one models** with a specific ID from the CIM database (PSS®ODMS).

### Workflow Description
This function returns a single model from the system. It provides an overview about all exports and imports associated with this specific CIM model. This function is used to get the right UUID to export the necessary files from the system.

### Function Description 
This section describes the necessary steps to use this function.

###### Endpoint
> GET /api/odms/model-management/model/{id}

###### Authorization
- Authorization Type: "Bearer Token"
- Token: AccessToken [see here](../IdentityManagement/Authorization.md)

###### Parameters
- ID: UUID


###### Body
no Body is used

###### Return
This function will return an object as described by the example object below.
````JSON
{
  "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "creationTime": "2021-04-27T07:34:50.858Z",
  "creatorId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "lastModificationTime": "2021-04-27T07:34:50.858Z",
  "lastModifierId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "schemaName": "string",
  "serverName": "string",
  "exports": [
    {
      "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "creationTime": "2021-04-27T07:34:50.858Z",
      "creatorId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "lastModificationTime": "2021-04-27T07:34:50.858Z",
      "lastModifierId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "fileId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "fileName": "string"
    }
  ],
  "imports": [
    {
      "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "creationTime": "2021-04-27T07:34:50.858Z",
      "creatorId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "lastModificationTime": "2021-04-27T07:34:50.858Z",
      "lastModifierId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
    }
  ]
}
````