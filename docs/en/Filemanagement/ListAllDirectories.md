# List all Directories

### Introduction
This section describes how to **list all directories** which are accessible on the Network Model Management platform.

### Workflow Description
This function lists all accessible directories in the system. It helps to navigate through the system. Other functions might be used to navigate to subdirectories.


### Function Description 
This section describes the necessary steps to use this function.

###### Endpoint
> GET /api/file-management/directory-descriptor

###### Authorization
- Authorization Type: "Bearer Token"
- Token: AccessToken [see here](../IdentityManagement/Authorization.md)

###### Parameters
- Filter: string
- Sorting: string
- Id: UUID

###### Body
no Body is used

###### Return
This function will return an object as described by the example object below.
````JSON
{
    "items": [
        {
        "name": "string",
        "isDirectory": true,
        "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
        "size": 0,
        "iconInfo": {
            "icon": "string",
            "type": 0
        }
        }
    ],
    "totalCount": 0
}
````