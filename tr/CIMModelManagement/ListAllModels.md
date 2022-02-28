# Tüm Modelleri Listele

### Tanıtım
Bu bölüm, CIM veritabanında (PSS®ODMS) depolanan **tüm modellerin nasıl listeleneceğini** açıklar.

### İş Akışı Açıklaması
Bu işlev, sistemdeki tüm erişilebilir modelleri listeler. Belirli bir CIM modeliyle ilişkili tüm dışa aktarma ve içe aktarma işlemlerine ilişkin bir genel bakış sağlar. Bu işlev, gerekli dosyaları sistemden dışa aktarmak için doğru UUID'yi almak için kullanılır.

### İşlev Açıklaması
Bu bölüm, bu işlevi kullanmak için gerekli adımları açıklar.

###### Uç nokta
> GET /api/odms/model-management/models

###### Yetki
- Authorization Type: "Bearer Token"
- Token: AccessToken [see here](../IdentityManagement/Authorization.md)

###### Parametreler
- Filter: string
- Sorting: string
- SkipCount: integer
- MaxResultCount: integer

###### Body
Body kullanılmaz

###### Return
Bu işlev, aşağıdaki örnek nesne tarafından açıklandığı gibi bir nesne döndürür.
````JSON
{
     "items": [
        {
        "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
        "creationTime": "2021-04-27T07:28:07.795Z",
        "creatorId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
        "lastModificationTime": "2021-04-27T07:28:07.795Z",
        "lastModifierId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
        "schemaName": "string",
        "serverName": "string",
        "exports": [
            {
            "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
            "creationTime": "2021-04-27T07:28:07.795Z",
            "creatorId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
            "lastModificationTime": "2021-04-27T07:28:07.795Z",
            "lastModifierId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
            "fileId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
            "fileName": "string"
            }
        ],
        "imports": [
            {
            "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
            "creationTime": "2021-04-27T07:28:07.795Z",
            "creatorId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
            "lastModificationTime": "2021-04-27T07:28:07.795Z",
            "lastModifierId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
            }
        ]
        }
    ],
    "totalCount": 0
}
````