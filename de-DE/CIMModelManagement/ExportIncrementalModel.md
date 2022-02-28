# Inkrementelles Modell exportieren

### Förderung
In diesem Abschnitt wird erklärt, **wie ein inkrementelles Modell** exportiert wird, das in der CIM-Datenbank (PSS®ODMS) gespeichert ist.

### Workflow-Beschreibung
Diese Funktion exportiert ein inkrementelles Modell aus einer Modellhistorie in CIM/XML inkrementell und speichert das Ergebnis im Dateiverwaltungssystem. Diese Funktion gibt Informationen über die in der Dateiverwaltung erstellte Datei zurück.
Folgende Angaben sind im Anfragetext erforderlich:
- dbType: Aufzählung des Datenbanktyps (1=Oracle, 2=MSSQL)
- serverName: Servername oder Adresse
- schemaName: Der Schemaname der ODMS-Instanz auf dem Server
- operationId: Diese ID wird intern verwendet, um den Vorgang zu verfolgen, sie fließt auch in die Benennung der generierten Datei ein.
- password: Standard-Leerzeichenfolge, wenn nur verwendet
- fromRevision: Revisions-ID für das Originalmodell
- toRevision: Revisions-ID des modifizierten Modells

Die folgenden Informationen sind im Anfragetext optional:
- modelAuthoritySet: Option zum Filtern von Modellinhalten mit einem einzigen Modellierungsautoritätssatz

### Bedienungsanleitung
In diesem Abschnitt werden die Schritte erläutert, die zur Verwendung dieser Funktion erforderlich sind.

###### Drei Punkte
> POST /api/odms/model-management/export/incremental-xml

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
  "fromRevision": 0,
  "toRevision": 0,
  "modelAuthoritySet": "string"
}
````

###### Return
Diese Funktion gibt ein Objekt wie im folgenden Beispielobjekt beschrieben zurück.
```JSON
{
  "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "creationTime": "2021-04-27T07:51:54.126Z",
  "creatorId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "lastModificationTime": "2021-04-27T07:51:54.126Z",
  "lastModifierId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "fileId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "fileName": "string"
}
````