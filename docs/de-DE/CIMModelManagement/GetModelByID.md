# Modell nach ID abrufen

### Förderung
In diesem Abschnitt wird erläutert, wie Sie **ein Modell** mit einer bestimmten ID aus der CIM-Datenbank (PSS®ODMS) abrufen.

### Workflow-Beschreibung
Diese Funktion gibt ein einzelnes Modell vom System zurück. Es bietet einen Überblick über alle Exporte und Importe, die mit diesem speziellen CIM-Modell verbunden sind. Diese Funktion wird verwendet, um die richtige UUID zu erhalten, um die erforderlichen Dateien aus dem System zu exportieren.

### Bedienungsanleitung
In diesem Abschnitt werden die Schritte erläutert, die zur Verwendung dieser Funktion erforderlich sind.

###### Drei Punkte
> GET /api/odms/model-management/model/{id}

###### Autorität
- Authorization Type: "Bearer Token"
- Token: AccessToken [see here](../IdentityManagement/Authorization.md)

###### Parameter
- ID: UUID


###### Body
Body wird nicht verwendet

###### Zurückkehren
Diese Funktion gibt ein Objekt wie im folgenden Beispielobjekt beschrieben zurück.
```JSON
{
  "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "creationTime": "2021-04-27T07:34:50,858Z",
  "creatorId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "lastModificationTime": "2021-04-27T07:34:50,858Z",
  "lastModifierId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "schemaName": "Zeichenfolge",
  "serverName": "Zeichenfolge",
  "exports": [
    {
      "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "creationTime": "2021-04-27T07:34:50,858Z",
      "creatorId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "lastModificationTime": "2021-04-27T07:34:50,858Z",
      "lastModifierId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "fileId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "fileName": "string"
    }
  ],
  "imports": [
    {
      "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "creationTime": "2021-04-27T07:34:50,858Z",
      "creatorId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "lastModificationTime": "2021-04-27T07:34:50,858Z",
      "lastModifierId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
    }
  ]
}
````