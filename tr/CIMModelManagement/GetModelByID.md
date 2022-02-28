# ID'ye Göre Model Al

### Tanıtım
Bu bölüm, CIM veritabanından (PSS®ODMS) belirli bir kimliğe sahip **bir modelin** nasıl alınacağını açıklar.

### İş Akışı Açıklaması
Bu işlev, sistemden tek bir model döndürür. Bu özel CIM modeliyle ilişkili tüm ihracat ve ithalatlar hakkında bir genel bakış sağlar. Bu işlev, gerekli dosyaları sistemden dışa aktarmak için doğru UUID'yi almak için kullanılır.

### İşlev Açıklaması
Bu bölüm, bu işlevi kullanmak için gerekli adımları açıklar.

###### Uç nokta
> GET /api/odms/model-management/model/{id}

###### Yetki
- Authorization Type: "Bearer Token"
- Token: AccessToken [see here](../IdentityManagement/Authorization.md)

###### Parametreler
- ID: UUID


###### Body
Body kullanılmaz

###### Return
Bu işlev, aşağıdaki örnek nesne tarafından açıklandığı gibi bir nesne döndürür.
````JSON
{
  "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "creationTime": "2021-04-27T07:34:50.858Z",
  "creatorId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "lastModificationTime": "2021-04-27T07:34:50.858Z",
  "lastModifierId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "schemaName": "string",
  "serverName": "string",
  "exports": [
    {
      "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "creationTime": "2021-04-27T07:34:50.858Z",
      "creatorId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "lastModificationTime": "2021-04-27T07:34:50.858Z",
      "lastModifierId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "fileId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "fileName": "string"
    }
  ],
  "imports": [
    {
      "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "creationTime": "2021-04-27T07:34:50.858Z",
      "creatorId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "lastModificationTime": "2021-04-27T07:34:50.858Z",
      "lastModifierId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
    }
  ]
}
````