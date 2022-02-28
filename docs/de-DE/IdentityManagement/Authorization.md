# Autorität

### Förderung
In diesem Abschnitt wird erläutert, wie Sie sich mit einer externen Anwendung **autorisieren** und das bereitgestellte **Zugriffstoken** für die weitere Verwendung verwenden.

### Workflow-Beschreibung
Der Standardansatz **OAuth2.0** wird verwendet, um jeden API-Aufruf zu autorisieren. Daher bietet PSS®NMM einen Endpunkt, der ein Zugriffstoken für den Zugriff auf jede API bereitstellt. Weitere Informationen finden Sie hier ([Microsoft Documentation](https://docs.microsoft.com/en-us/azure/active-directory/develop/v2-oauth2-auth-code-flow)).

![](/Images/Authorization.png)

### Bedienungsanleitung
In diesem Abschnitt werden die erforderlichen Schritte zum Abrufen eines Zugriffstokens vom System beschrieben.

###### Drei Punkte
> POST /connect/token

Die Token-Methode erfordert verschiedene Attribute:
###### Autorität
- Authorization Type: "Basic Auth"
- Username: "NMM_App"
- Password: "password" (dies muss das im System definierte gemeinsame Geheimnis sein)


###### Header
- Content-Type: "application/x-www-form-urlencoded"
- __tenant: "TenantName" (sistemde tanımlanan kiracı adıdır)


###### Body
    {
    "grant_type" : "password",
        "username" : "username",
        "password" : "password"
    }

###### Return
Diese Funktion gibt ein Objekt zurück, das das erforderliche Zugriffstoken für andere API-Aufrufe enthält.

    {
        "accesstoken" : string,
        "expires_in" : int,
        "token_type" : string,
        "refresh_token" : string,
        "scope" : string
    }