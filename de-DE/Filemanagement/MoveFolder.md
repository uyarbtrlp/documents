# Verschieben Sie einen vorhandenen Ordner

### Förderung
In diesem Abschnitt wird erläutert, wie Sie **einen vorhandenen Ordner verschieben**, auf den über die Network Model Management-Plattform zugegriffen werden kann.

### Workflow-Beschreibung
Diese Funktion hat einen angegebenen Ordner in einen neuen Ordner verschoben. Es ermöglicht das Erstellen einer verschachtelten Ordnerstruktur.
Diese Funktion gibt die Informationen des verschobenen Ordners zurück.


### Bedienungsanleitung
In diesem Abschnitt werden die Schritte erläutert, die zur Verwendung dieser Funktion erforderlich sind.


###### Drei Punkte
> POST /api/file-management/directory-descriptor/move

###### Autorität
- Authorization Type: "Bearer Token"
- Token: AccessToken [see here](../IdentityManagement/Authorization.md)


###### Parameter
es werden keine Parameter verwendet

###### Body
Sehen Sie sich diesen Beispiel-Anfragetext an.
```JSON
{
    "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "newParentId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}
````

###### Return
Diese Funktion gibt ein Objekt wie im folgenden Beispielobjekt beschrieben zurück.
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