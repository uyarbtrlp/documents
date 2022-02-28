# Mevcut bir Klasörü yeniden adlandırın

### Tanıtım
Bu bölüm, Ağ Modeli Yönetimi platformundan erişilebilen **mevcut bir klasörün nasıl yeniden adlandırılacağını** açıklar.

### İş Akışı Açıklaması
Bu işlev, yeniden adlandırılan klasörün bilgilerini döndürür.


### İşlev Açıklaması
Bu bölüm, bu işlevi kullanmak için gerekli adımları açıklar.


###### Uç nokta
> POST /api/file-management/directory-descriptor/{id}

###### Yetki
- Authorization Type: "Bearer Token"
- Token: AccessToken [see here](../IdentityManagement/Authorization.md)

###### Parametreler
- id: UUID

###### Body
Bu örnek istek gövdesine bakın.
````JSON
{
    "name": "string"
}
````

###### Return
Bu işlev, aşağıda örnek nesne tarafından açıklandığı gibi bir nesne döndürür.
````JSON
{
    "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "creationTime": "2021-04-23T11:56:33.125Z",
    "creatorId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "lastModificationTime": "2021-04-23T11:56:33.125Z",
    "lastModifierId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "name": "string",
    "parentId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}
````