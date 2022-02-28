## Ağ Modeli Yönetim API'sı
Bu belge, Ağ Modeli Yönetimi araçlarının API açıklamasını kapsayacaktır.
Çözümün farklı modüllerini temsil eden farklı bölümlerde ayrılacaktır:

### Kimlik yönetimi
###### GET
- [Yetkilendirme](IdentityManagement/Authorization.md)

### Dosya Yönetimi - Dizin
###### GET
- [Tüm Dizinleri Listele](Filemanagement/ListAllDirectories.md)
- [ID ye Göre Dizini Al](Filemanagement/GetDirectoryByID.md)
- [Tüm Alt Dizinleri Al](Filemanagement/GetAllSubdirectories.md)
###### DELETE
- [ID ye göre Dizini Sil](Filemanagement/DeleteDirectoryByID.md)
###### POST
- [Yeni Klasör Oluştur](Filemanagement/CreateNewFolder.md)
- [Klasörü Yeniden Adlandır](Filemanagement/RenameFolder.md)
- [Klasörü Taşı](Filemanagement/MoveFolder.md)

### Dosya Yönetimi - Dosya
###### GET
- Bir dizindeki tüm Dosyaları listelee
- ID ye göre bir Dosya alın
- Dosya içeriğini al
- ID ye göre Dosyayı İndir
###### DELETE
- ID ye göre Dosyayı Sil
###### POST
- Dosya yükleme ????
- Yeni bir Dosya oluştur
- Dosyayı başka bir klasöre taşı
- Bir Dosyayı Yeniden Adlandır

### ODMS İşlevi
###### GET
- [Tüm Modelleri Al](CIMModelManagement/ListAllModels.md)
- [ID ye Göre Bir Model Alın](CIMModelManagement/GetModelByID.md)
###### DELETE
- [ID ye Göre Modeli Sil](CIMModelManagement/DeleteModelByID.md)
###### POST
- [Bir Artımlı Modeli Dışa Aktar](CIMModelManagement/ExportIncrementalModel.md)
- [Tam Modeli Dışa Aktar](CIMModelManagement/ExportFullModel.md)