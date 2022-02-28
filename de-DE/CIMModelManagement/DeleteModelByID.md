# Modell nach ID löschen

### Förderung
In diesem Abschnitt wird erläutert, wie Sie **ein bestimmtes Modell aus der CIM-Datenbank löschen**.

### Workflow-Beschreibung
Dadurch wird ein bestimmtes Modell gelöscht. Dadurch werden das Modell aus der CIM-Datenbank und alle mit diesem Modell verknüpften Exporte und Importe entfernt.

### Bedienungsanleitung
In diesem Abschnitt werden die Schritte erläutert, die zur Verwendung dieser Funktion erforderlich sind.

###### Drei Punkte
> DELETE /api/odms/model-management/model/{id}

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