# Delete Directory by ID

### Introduction
This section describes how to **delete a specific directory** which is accessible on the Network Model Management platform.

### Workflow Description
This deletes a specific directory. This is used to remove a folder from the file management strucutre


### Function Description 
This section describes the necessary steps to use this function.


###### Endpoint
> DELETE /api/file-management/directory-descriptor/{id}

###### Authorization
- Authorization Type: "Bearer Token"
- Token: AccessToken [see here](../IdentityManagement/Authorization.md)

###### Parameters
- id: UUID

###### Body
no Body is used

###### Return
This function will a HTTP status code on success

    HTTP 200