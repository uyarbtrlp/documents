# Tüm Dizinleri Listele

### Tanıtım
Bu bölüm, Ağ Modeli Yönetimi platformunda erişilebilir olan **tüm dizinlerin nasıl listeleneceğini** açıklar.

### İş Akışı Açıklaması
Bu işlev, sistemdeki tüm erişilebilir dizinleri listeler. Sistemde gezinmeye yardımcı olur. Alt dizinlere gitmek için başka işlevler kullanılabilir.


### İşlev Açıklaması
Bu bölüm, bu işlevi kullanmak için gerekli adımları açıklar.

###### Uç nokta
> GET /api/file-management/directory-descriptor

###### Yetki
- Authorization Type: "Bearer Token"
- Token: AccessToken [see here](../IdentityManagement/Authorization.md)

###### Parametreler
- Filter: string
- Sorting: string
- Id: UUID

###### Body
Body kullanılmaz

###### Return
Bu işlev, aşağıdaki örnek nesne tarafından açıklandığı gibi bir nesne döndürür.
````JSON
{
    "items": [
        {
        "name": "string",
        "isDirectory": true,
        "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
        "size": 0,
        "iconInfo": {
            "icon": "string",
            "type": 0
        }
        }
    ],
    "totalCount": 0
}
````