# Yeni bir Klasör oluştur

### Tanıtım
Bu bölüm, Ağ Modeli Yönetimi platformundan erişilebilen **yeni bir klasörün nasıl oluşturulacağını** açıklamaktadır.

### İş Akışı Açıklaması
Bu işlev, yeni oluşturulan klasörün bilgilerini döndürür.


### İşlev Açıklaması
Bu bölüm, bu işlevi kullanmak için gerekli adımları açıklar.


###### Uç nokta
> POST /api/file-management/directory-descriptor

###### Yetki
- Authorization Type: "Bearer Token"
- Token: AccessToken [see here](../IdentityManagement/Authorization.md)

###### Parametreler
hiçbir parametre kullanılmaz

###### Body
Bu örnek istek gövdesine bakın.
````JSON
{
    "parentId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "name": "string"
}
````

###### Return
Bu işlev, aşağıda örnek nesne tarafından açıklandığı gibi bir nesne döndürür.
````JSON
{
    "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "creationTime": "2021-04-23T11:51:17.879Z",
    "creatorId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "lastModificationTime": "2021-04-23T11:51:17.879Z",
    "lastModifierId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "name": "string",
    "parentId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}
````