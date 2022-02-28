# Verzeichnis nach ID löschen

### Förderung
In diesem Abschnitt wird erläutert, wie Sie **ein bestimmtes Verzeichnis löschen**, auf das über die Network Model Management-Plattform zugegriffen werden kann.

### Workflow-Beschreibung
Dadurch wird ein bestimmtes Verzeichnis gelöscht. Dies wird verwendet, um einen Ordner aus der Dateiverwaltungsstruktur zu entfernen.


### Bedienungsanleitung
In diesem Abschnitt werden die Schritte erläutert, die zur Verwendung dieser Funktion erforderlich sind.


###### Drei Punkte
> DELETE /api/file-management/directory-descriptor/{id}

###### Autorität
- Authorization Type: "Bearer Token"
- Token: AccessToken [see here](../IdentityManagement/Authorization.md)


###### Parameter
- ID: UUID

###### Body
Body wird nicht verwendet

###### Return
Diese Funktion generiert bei Erfolg einen HTTP-Statuscode.

      HTTP-200