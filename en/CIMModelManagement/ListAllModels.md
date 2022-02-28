# List all Models

### Introduction
This section describes how to **list all models** which are stored in the CIM database (PSS®ODMS).

### Workflow Description
This function lists all accessible models in the system. It provides an overview about all exports and imports associated with a specific CIM model. This function is used to get the right UUID to export the necessary files from the system.

### Function Description 
This section describes the necessary steps to use this function.

###### Endpoint
> GET /api/odms/model-management/models

###### Authorization
- Authorization Type: "Bearer Token"
- Token: AccessToken [see here](../IdentityManagement/Authorization.md)

###### Parameters
- Filter: string
- Sorting: string
- SkipCount: integer
- MaxResultCount: integer

###### Body
no Body is used

###### Return
This function will return an object as described by the example object below.
````JSON
{
    "items": [
        {
        "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
        "creationTime": "2021-04-27T07:28:07.795Z",
        "creatorId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
        "lastModificationTime": "2021-04-27T07:28:07.795Z",
        "lastModifierId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
        "schemaName": "string",
        "serverName": "string",
        "exports": [
            {
            "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
            "creationTime": "2021-04-27T07:28:07.795Z",
            "creatorId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
            "lastModificationTime": "2021-04-27T07:28:07.795Z",
            "lastModifierId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
            "fileId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
            "fileName": "string"
            }
        ],
        "imports": [
            {
            "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
            "creationTime": "2021-04-27T07:28:07.795Z",
            "creatorId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
            "lastModificationTime": "2021-04-27T07:28:07.795Z",
            "lastModifierId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
            }
        ]
        }
    ],
    "totalCount": 0
}
````