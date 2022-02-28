# Alle Verzeichnisse auflisten

### Förderung
In diesem Abschnitt wird erläutert, wie Sie **alle Verzeichnisse** auflisten, auf die in der Network Model Management-Plattform zugegriffen werden kann.

### Workflow-Beschreibung
Diese Funktion listet alle erreichbaren Verzeichnisse im System auf. Es hilft, das System zu navigieren. Andere Funktionen können verwendet werden, um zu Unterverzeichnissen zu navigieren.


### Bedienungsanleitung
In diesem Abschnitt werden die Schritte erläutert, die zur Verwendung dieser Funktion erforderlich sind.

###### Drei Punkte
> GET /api/file-management/directory-descriptor

###### Autorität
- Authorization Type: "Bearer Token"
- Token: AccessToken [see here](../IdentityManagement/Authorization.md)

###### Parameter
- Filter: string
- Sorting: string
- Id: UUID

###### Body
Body wird nicht verwendet

###### Return
Diese Funktion gibt ein Objekt wie im folgenden Beispielobjekt beschrieben zurück.
```JSON
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