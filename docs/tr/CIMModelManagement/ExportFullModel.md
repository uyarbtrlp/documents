# Tam Modeli Dışa Aktar

### Tanıtım
Bu bölüm, CIM veritabanında (PSS®ODMS) saklanan **tam bir modelin nasıl dışa aktarılacağını** açıklar.

### İş Akışı Açıklaması
Bu işlev, tam bir modeli CIM veritabanından CIM/XML olarak dışa aktarır ve sonucu dosya yönetim sisteminde saklar. Bu işlev, dosya yönetiminde oluşturulan dosya hakkında bilgi döndürür.
Talep gövdesinde aşağıdaki bilgiler gereklidir:
- dbType: Veritabanı türünün numaralandırılması (1=Oracle, 2=MSSQL)
- serverName: Sunucuadı veya Adres
- schemaName: Sunucudaki ODMS örneğinin şema adı
- password: yalnızca kullanımdaysa, varsayılan boş dize
- operationId: Bu kimlik, işlemi izlemek için dahili olarak kullanılacaktır, ayrıca oluşturulan dosyanın adlandırılmasında da sona erecektir.

İstek gövdesinde aşağıdaki bilgiler isteğe bağlıdır:
- profileType: Profillere göre filtrelemek için profil kimliklerinin kombinasyonu
- modelAuthoritySet: Model içeriğini tek bir modelleme otorite seti ile filtreleme seçeneği

### İşlev Açıklaması
Bu bölüm, bu işlevi kullanmak için gerekli adımları açıklar.

###### Uç nokta
> POST /api/odms/model-management/export/full-xml

###### Yetki
- Authorization Type: "Bearer Token"
- Token: AccessToken [see here](../IdentityManagement/Authorization.md)

###### Parametreler
Parametre kullanılmaz

###### Body
````JSON
{
   "dbType": 0,
  "serverName": "string",
  "schemaName": "string",
  "password": "string",
  "operationId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "profileType": 0,
  "modelAuthoritySet": "string"
}
````

###### Return
Bu işlev, aşağıdaki örnek nesne tarafından açıklandığı gibi bir nesne döndürür.
````JSON
{
"id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "creationTime": "2021-04-27T07:45:02.543Z",
  "creatorId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "lastModificationTime": "2021-04-27T07:45:02.543Z",
  "lastModifierId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "fileId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "fileName": "string"
}
````