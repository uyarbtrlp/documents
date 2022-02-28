# Alle Unterverzeichnisse abrufen

### Förderung
In diesem Abschnitt wird erläutert, wie Sie alle Unterverzeichnisse eines bestimmten übergeordneten Verzeichnisses auflisten, auf die in der Network Model Management-Plattform zugegriffen werden kann.

### Workflow-Beschreibung
Diese Funktion listet alle dubdirectories eines bestimmten Verzeichnisses auf. Dies hilft bei der Navigation durch die Ordnerstruktur des Systems.


### Bedienungsanleitung
In diesem Abschnitt werden die Schritte erläutert, die zur Verwendung dieser Funktion erforderlich sind.


###### Drei Punkte
> GET /api/file-management/directory-descriptor/sub-directories


###### Autorität
- Authorization Type: "Bearer Token"
- Token: AccessToken [see here](../IdentityManagement/Authorization.md)

###### Parameter
- Elternteil: UUID

###### Body
Body wird nicht verwendet

###### Return
Diese Funktion gibt ein Objekt wie im folgenden Beispiel beschrieben zurück.
```JSON
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