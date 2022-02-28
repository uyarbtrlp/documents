## Netzwerkmodellverwaltungs-API
Diese Dokumentation behandelt die API-Beschreibung der Tools zur Netzwerkmodellverwaltung.
Es wird in verschiedene Kapitel unterteilt, die verschiedene Module der Lösung darstellen:

### Identitätsmanagement
###### GET
- [Authorization](IdentityManagement/Authorization.md)

Dateiverwaltung - Verzeichnis
###### GET
- [Alle Verzeichnisse auflisten](Filemanagement/ListAllDirectories.md)
- [Verzeichnis nach ID abrufen](Filemanagement/GetDirectoryByID.md)
- [Alle Unterverzeichnisse abrufen](Filemanagement/GetAllSubdirectories.md)
###### DELETE
- [Verzeichnis nach ID löschen](Filemanagement/DeleteDirectoryByID.md)
###### POST
- [Neuen Ordner erstellen](Filemanagement/CreateNewFolder.md)
- [Ordner umbenennen](Filemanagement/RenameFolder.md)
- [Ordner verschieben](Filemanagement/MoveFolder.md)

### Dateiverwaltung - Datei
###### GET
- Alle Dateien in einem Verzeichnis auflisten
- Holen Sie sich eine Datei nach ID
- Dateiinhalt abrufen
- Datei nach ID herunterladen
###### DELETE
- Datei nach ID löschen
###### POST
- Datei hochladen ????
- Erstellen Sie eine neue Datei
- Datei in einen anderen Ordner verschieben
- Eine Datei umbenennen

### ODMS Funktion
###### GET
- [Alle Modelle abrufen](CIMModelManagement/ListAllModels.md)
- [Modell nach ID abrufen](CIMModelManagement/GetModelByID.md)
###### DELETE
- [Modell nach ID löschen](CIMModelManagement/DeleteModelByID.md)
###### POST
- [Inkrementelles Modell exportieren](CIMModelManagement/ExportIncrementalModel.md)
- [Ein vollständiges Modell exportieren](CIMModelManagement/ExportFullModel.md)