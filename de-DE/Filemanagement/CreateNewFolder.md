# Einen neuen Ordner erstellen

### Förderung
In diesem Abschnitt wird beschrieben, **wie Sie einen neuen Ordner erstellen**, auf den über die Network Model Management-Plattform zugegriffen werden kann.

### Workflow-Beschreibung
Diese Funktion gibt die Informationen des neu erstellten Ordners zurück.


### Bedienungsanleitung
In diesem Abschnitt werden die Schritte erläutert, die zur Verwendung dieser Funktion erforderlich sind.


###### Drei Punkte
> POST /api/file-management/directory-descriptor

###### Autorität
- Authorization Type: "Bearer Token"
- Token: AccessToken [see here](../IdentityManagement/Authorization.md)

###### Parameter
es werden keine Parameter verwendet

###### Body
Sehen Sie sich diesen Beispiel-Anfragetext an.
```JSON
{
    "parentId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "name": "string"
}
````

###### Return
Diese Funktion gibt ein Objekt wie im folgenden Beispielobjekt beschrieben zurück.
```JSON
{
    "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "creationTime": "2021-04-23T11:51:17.879Z",
    "creatorId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "lastModificationTime": "2021-04-23T11:51:17.879Z",
    "lastModifierId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "name": "string",
    "parentId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}
````