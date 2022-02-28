# Get Directory by ID

### Introduction
This section describes how to **get a specific directory** which is accessible on the Network Model Management platform.

### Workflow Description
This function returns a specific directory. This is used to get additional information about a specific folder in the system.


### Function Description 
This section describes the necessary steps to use this function.


###### Endpoint
> GET /api/file-management/directory-descriptor/{id}

###### Authorization
- Authorization Type: "Bearer Token"
- Token: AccessToken [see here](../IdentityManagement/Authorization.md)

###### Parameters
- id: UUID

###### Body
no Body is used

###### Return
This function will return an object as described by the example below.
````JSON
{
    "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "creationTime": "2021-04-23T11:53:59.012Z",
    "creatorId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "lastModificationTime": "2021-04-23T11:53:59.012Z",
    "lastModifierId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "name": "string",
    "parentId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}
````