# Download Model By Name

### Introduction
This section describes how to **download a created file by name** which is stored in the file management system.

### Workflow Description
This function returns the requested file from the file management system. It uses the model name to bypass all other options to download any files.

### Function Description 
This section describes the necessary steps to use this function.

###### Endpoint
> GET /api/odms/xml/download-model/{name}

###### Authorization
- Authorization Type: "Bearer Token"
- Token: AccessToken [see here](../IdentityManagement/Authorization.md)

###### Parameters
- name: Full name of the model as returned by the creation functions

###### Body
no body required

###### Return
Returns the requested file