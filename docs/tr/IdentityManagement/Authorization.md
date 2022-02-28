# Yetki

### Tanıtım
Bu bölüm, harici bir uygulama ile nasıl **yetkilendirileceğini** ve daha fazla kullanım için sağlanan **erişim belirtecinin** nasıl kullanılacağını açıklar.

### İş Akışı Açıklaması
Herhangi bir API çağrısını yetkilendirmek için standart **OAuth2.0** yaklaşımı kullanılır. Bu nedenle PSS®NMM, herhangi bir API'ye erişmek için bir erişim belirteci sağlayan bir uç nokta sağlar. Daha fazla bilgiyi burada bulabilirsiniz ([Microsoft Documentation](https://docs.microsoft.com/en-us/azure/active-directory/develop/v2-oauth2-auth-code-flow)).

![](/Images/Authorization.PNG)

### İşlev Açıklaması
Bu bölüm, sistemden bir erişim belirteci almak için gerekli şeyleri açıklar.

###### Uç nokta
> POST /connect/token

Belirteç yöntemi farklı nitelikler gerektirir:
###### Yetki
- Authorization Type: "Basic Auth"
- Username: "NMM_App"
- Password: "password" (bu, sistemde tanımlanan paylaşılan gizli olmalıdır)

###### Header
- Content-Type: "application/x-www-form-urlencoded"
- __tenant: "TenantName" (sistemde tanımlanan kiracı adıdır)

###### Body
    {
    "grant_type" : "password",
        "username" : "username",
        "password" : "password"
    }

###### Return
Bu işlev, diğer API çağrıları için gerekli erişim belirtecini tutan bir nesne döndürür.

    {
        "accesstoken" : string,
        "expires_in" : int,
        "token_type" : string,
        "refresh_token" : string,
        "scope" : string
    }