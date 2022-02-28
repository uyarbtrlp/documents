# Download nach Modellname

### Förderung
In diesem Abschnitt wird erläutert, wie Sie eine **namensgenerierte Datei** herunterladen, die im Dateiverwaltungssystem gespeichert ist.

### Workflow-Beschreibung
Diese Funktion gibt die vom Dateiverwaltungssystem angeforderte Datei zurück. Es verwendet den Modellnamen, um alle anderen Optionen zum Herunterladen einer Datei zu umgehen.

### Bedienungsanleitung
In diesem Abschnitt werden die Schritte erläutert, die zur Verwendung dieser Funktion erforderlich sind.

###### Drei Punkte
> GET /api/odms/xml/download-model/{name}

###### Autorität
- Authorization Type: "Bearer Token"
- Token: AccessToken [see here](../IdentityManagement/Authorization.md)

###### Parameter
- name: Der vollständige Name des Modells, das von den Renderfunktionen zurückgegeben wird

###### Body
kein Body erforderlich

###### Return
Gibt die angeforderte Datei zurück