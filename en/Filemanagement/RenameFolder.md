# Rename an existing Folder

### Introduction
This section describes how to **rename an existing folder** which is accessible on the Network Model Management platform.

### Workflow Description
This function returns the information of the renamed folder.


### Function Description 
This section describes the necessary steps to use this function.


###### Endpoint
> POST /api/file-management/directory-descriptor/{id}

###### Authorization
- Authorization Type: "Bearer Token"
- Token: AccessToken [see here](../IdentityManagement/Authorization.md)

###### Parameters
- id: UUID

###### Body
See this exmaple request body.
````JSON
{
    "name": "string"
}
````

###### Return
This function will return an object as described below by the example object.
````JSON
{
    "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "creationTime": "2021-04-23T11:56:33.125Z",
    "creatorId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "lastModificationTime": "2021-04-23T11:56:33.125Z",
    "lastModifierId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "name": "string",
    "parentId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}
````