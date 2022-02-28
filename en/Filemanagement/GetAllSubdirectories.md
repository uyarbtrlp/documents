# Get all Subdirectories

### Introduction
This section describes how to **list all subdirectories** of a given parent directory which are accessible on the Network Model Management platform.

### Workflow Description
This function lists all dubdirectories of a given directory. This helps to navigat through the folder structure of the system.


### Function Description 
This section describes the necessary steps to use this function.


###### Endpoint
> GET /api/file-management/directory-descriptor/sub-directories

###### Authorization
- Authorization Type: "Bearer Token"
- Token: AccessToken [see here](../IdentityManagement/Authorization.md)

###### Parameters
- parentd: UUID

###### Body
no Body is used

###### Return
This function will return an object as described by the exmaple below.
````JSON
{
    "items": [
        {
        "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
        "name": "string",
        "parentId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
        "hasChildren": true
        }
    ]
}
````