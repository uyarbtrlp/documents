# Vollständiges Modell exportieren

### Förderung
In diesem Abschnitt wird beschrieben, **wie ein vollständiges Modell** exportiert wird, das in der CIM-Datenbank (PSS®ODMS) gespeichert ist.

### Workflow-Beschreibung
Diese Funktion exportiert ein vollständiges Modell aus der CIM-Datenbank als CIM/XML und speichert das Ergebnis im Dateiverwaltungssystem. Diese Funktion gibt Informationen über die in der Dateiverwaltung erstellte Datei zurück.
Folgende Angaben sind im Anfragetext erforderlich:
- dbType: Aufzählung des Datenbanktyps (1=Oracle, 2=MSSQL)
- serverName: Servername oder Adresse
- schemaName: Der Schemaname der ODMS-Instanz auf dem Server
- password: Standard-Leerzeichenfolge, wenn nur verwendet
- operationId: Diese ID wird intern verwendet, um den Vorgang zu verfolgen, sie fließt auch in die Benennung der generierten Datei ein.

Die folgenden Informationen sind im Anfragetext optional:
- profileType: Kombination von Profil-IDs zum Filtern nach Profilen
- modelAuthoritySet: Option zum Filtern von Modellinhalten mit einem einzigen Modellierungsautoritätssatz

### Bedienungsanleitung
In diesem Abschnitt werden die Schritte erläutert, die zur Verwendung dieser Funktion erforderlich sind.

###### Drei Punkte
> POST /api/odms/model-management/export/full-xml

###### Autorität
- Authorization Type: "Bearer Token"
- Token: AccessToken [see here](../IdentityManagement/Authorization.md)

###### Parameter
Parameter nicht verwendet

###### Body
```JSON
{
   "dbType": 0,
  "serverName": "Zeichenfolge",
  "schemaName": "Zeichenfolge",
  "Passwort": "Zeichenfolge",
  "operationId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "profileType": 0,
  "modelAuthoritySet": "string"
}
````

###### Return
Diese Funktion gibt ein Objekt wie im folgenden Beispielobjekt beschrieben zurück.
```JSON
{
"id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "creationTime": "2021-04-27T07:45:02.543Z",
  "creatorId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "lastModificationTime": "2021-04-27T07:45:02.543Z",
  "lastModifierId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "fileId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "fileName": "string"
}
````