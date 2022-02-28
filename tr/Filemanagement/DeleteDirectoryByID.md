# Kimliğe göre Dizini Sil

### Tanıtım
Bu bölüm, Ağ Modeli Yönetimi platformundan erişilebilen **belirli bir dizinin nasıl silineceğini** açıklar.

### İş Akışı Açıklaması
Bu, belirli bir dizini siler. Bu, dosya yönetimi yapısından bir klasörü kaldırmak için kullanılır.


### İşlev Açıklaması
Bu bölüm, bu işlevi kullanmak için gerekli adımları açıklar.


###### Uç nokta
> DELETE /api/file-management/directory-descriptor/{id}

###### Yetki
- Authorization Type: "Bearer Token"
- Token: AccessToken [see here](../IdentityManagement/Authorization.md)


###### Parametreler
- id: UUID

###### Body
Body kullanılmaz

###### Return
Bu işlev, başarı durumunda bir HTTP durum kodu oluşturacaktır.

     HTTP 200