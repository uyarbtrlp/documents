# Move an existing Folder

### Introduction
This section describes how to **Move an existing folder** which is accessible on the Network Model Management platform.

### Workflow Description
This function moved a specified folder to a new folder. It will allow to create a nested folder structure.
This function returns the information of the moved folder.


### Function Description 
This section describes the necessary steps to use this function.


###### Endpoint
> POST /api/file-management/directory-descriptor/move

###### Authorization
- Authorization Type: "Bearer Token"
- Token: AccessToken [see here](../IdentityManagement/Authorization.md)

###### Parameters
no parameters are used

###### Body
See this exmaple request body.
````JSON
{
    "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "newParentId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
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