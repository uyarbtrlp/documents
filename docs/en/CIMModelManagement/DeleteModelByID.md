# Delete Model by ID

### Introduction
This section describes how to **delete a specific model** from the CIM database.

### Workflow Description
This deletes a specific model. This will remove the model from the CIM database as well as all the exports and imports associated with that model.

### Function Description 
This section describes the necessary steps to use this function.

###### Endpoint
> DELETE /api/odms/model-management/model/{id}

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