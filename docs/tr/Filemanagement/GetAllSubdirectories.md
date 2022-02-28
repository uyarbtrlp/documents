# Tüm Alt Dizinleri Alın

### Tanıtım
Bu bölüm, Ağ Modeli Yönetimi platformunda erişilebilen belirli bir üst dizinin tüm alt dizinlerinin nasıl **listeleneceğini açıklar.

### İş Akışı Açıklaması
Bu işlev, belirli bir dizinin tüm dubdizinlerini listeler. Bu, sistemin klasör yapısında gezinmeye yardımcı olur.


### İşlev Açıklaması
Bu bölüm, bu işlevi kullanmak için gerekli adımları açıklar.


###### Uç nokta
> GET /api/file-management/directory-descriptor/sub-directories

###### Yetki
- Authorization Type: "Bearer Token"
- Token: AccessToken [see here](../IdentityManagement/Authorization.md)

###### Parametreler
- parentd: UUID

###### Body
Body kullanılmaz

###### Return
Bu işlev, aşağıdaki örnekte açıklandığı gibi bir nesne döndürür.
````JSON
{
    "items": [
        {
        "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
        "name": "string",
        "parentId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
        "hasChildren": true
        }
    ]
}
````