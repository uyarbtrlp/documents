# ID'ye Göre Modeli Sil

### Tanıtım
Bu bölüm, CIM veritabanından **belirli bir modelin nasıl silineceğini** açıklar.

### İş Akışı Açıklaması
Bu, belirli bir modeli siler. Bu, modeli CIM veritabanından ve bu modelle ilişkili tüm dışa aktarma ve içe aktarma işlemlerini kaldıracaktır.

### İşlev Açıklaması
Bu bölüm, bu işlevi kullanmak için gerekli adımları açıklar.

###### Uç nokta
> DELETE /api/odms/model-management/model/{id}

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