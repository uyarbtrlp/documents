# Kimliğe göre Dizin Alın

### Tanıtım
Bu bölüm, Ağ Modeli Yönetimi platformundan erişilebilen **belirli bir dizinin nasıl alınacağını** açıklamaktadır.

### İş Akışı Açıklaması
Bu işlev belirli bir dizini döndürür. Bu, sistemdeki belirli bir klasör hakkında ek bilgi almak için kullanılır.


### İşlev Açıklaması
Bu bölüm, bu işlevi kullanmak için gerekli adımları açıklar.


###### Uç nokta
> GET /api/file-management/directory-descriptor/{id}

###### Yetki
- Authorization Type: "Bearer Token"
- Token: AccessToken [see here](../IdentityManagement/Authorization.md)

###### Parametreler
- id: UUID

###### Body
Body kullanılmaz

###### Return
Bu işlev, aşağıdaki örnekte açıklandığı gibi bir nesne döndürür.
````JSON
{
    "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "creationTime": "2021-04-23T11:53:59.012Z",
    "creatorId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "lastModificationTime": "2021-04-23T11:53:59.012Z",
    "lastModifierId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "name": "string",
    "parentId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}
````