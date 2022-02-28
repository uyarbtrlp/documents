# Model Adına Göre İndir

### Tanıtım
Bu bölüm, dosya yönetim sisteminde depolanan **ada göre oluşturulan bir dosyanın nasıl indirileceğini** açıklar.

### İş Akışı Açıklaması
Bu işlev, dosya yönetim sisteminden istenen dosyayı döndürür. Herhangi bir dosyayı indirmek için diğer tüm seçenekleri atlamak için model adını kullanır.

### İşlev Açıklaması
Bu bölüm, bu işlevi kullanmak için gerekli adımları açıklar.

###### Uç nokta
> GET /api/odms/xml/download-model/{name}

###### Yetki
- Authorization Type: "Bearer Token"
- Token: AccessToken [see here](../IdentityManagement/Authorization.md)

###### Parametreler
- name: Oluşturma işlevleri tarafından döndürülen modelin tam adı

###### Body
Body gerekli değil

###### Return
İstenen dosyayı döndürür