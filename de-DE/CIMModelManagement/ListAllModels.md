# Alle Modelle auflisten

### Förderung
In diesem Abschnitt wird erläutert, wie Sie **alle Modelle** auflisten, die in der CIM-Datenbank (PSS®ODMS) gespeichert sind.

### Workflow-Beschreibung
Diese Funktion listet alle zugänglichen Modelle im System auf. Es bietet einen Überblick über alle Export- und Importvorgänge, die mit einem bestimmten CIM-Modell verbunden sind. Diese Funktion wird verwendet, um die richtige UUID zu erhalten, um die erforderlichen Dateien aus dem System zu exportieren.

### Bedienungsanleitung
In diesem Abschnitt werden die Schritte erläutert, die zur Verwendung dieser Funktion erforderlich sind.

###### Drei Punkte
> GET /api/odms/model-management/models

###### Autorität
- Authorization Type: "Bearer Token"
- Token: AccessToken [see here](../IdentityManagement/Authorization.md)

###### Parameter
- Filter: Zeichenfolge
- Sortierung: Zeichenfolge
- SkipCount: Ganzzahl
- MaxResultCount: Ganzzahl

###### Body
Body wird nicht verwendet

###### Zurückkehren
Diese Funktion gibt ein Objekt wie im folgenden Beispielobjekt beschrieben zurück.
````JSON
{
     "items": [
        {
        "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
        "creationTime": "2021-04-27T07:28:07.795Z",
        "creatorId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
        "lastModificationTime": "2021-04-27T07:28:07.795Z",
        "lastModifierId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
        "schemaName": "string",
        "serverName": "string",
        "exports": [
            {
            "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
            "creationTime": "2021-04-27T07:28:07.795Z",
            "creatorId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
            "lastModificationTime": "2021-04-27T07:28:07.795Z",
            "lastModifierId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
            "fileId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
            "fileName": "string"
            }
        ],
        "imports": [
            {
            "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
            "creationTime": "2021-04-27T07:28:07.795Z",
            "creatorId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
            "lastModificationTime": "2021-04-27T07:28:07.795Z",
            "lastModifierId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
            }
        ]
        }
    ],
    "totalCount": 0
}
````