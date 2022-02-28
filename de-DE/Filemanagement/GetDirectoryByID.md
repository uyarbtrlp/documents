# Verzeichnis nach ID abrufen

### Förderung
In diesem Abschnitt wird erläutert, wie Sie **einen bestimmten Index erhalten**, auf den über die Network Model Management-Plattform zugegriffen werden kann.

### Workflow-Beschreibung
Diese Funktion gibt ein bestimmtes Verzeichnis zurück. Dies wird verwendet, um zusätzliche Informationen zu einem bestimmten Ordner im System zu erhalten.


### Bedienungsanleitung
In diesem Abschnitt werden die Schritte erläutert, die zur Verwendung dieser Funktion erforderlich sind.


###### Drei Punkte
> GET /api/file-management/directory-descriptor/{id}

###### Autorität
- Authorization Type: "Bearer Token"
- Token: AccessToken [see here](../IdentityManagement/Authorization.md)

###### Parameter
- ID: UUID

###### Body
Body wird nicht verwendet

###### Return
Diese Funktion gibt ein Objekt wie im folgenden Beispiel beschrieben zurück.
```JSON
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