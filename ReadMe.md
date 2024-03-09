#KEYCLOAK

### Database sistemi uzerinden anlatim
database serveri --> realm
database --> client --> client ayni zamanda login islemleri icin bilgileri iceriyor(client_id,client_secret vb) bu yuzden client senin uygulamandir.

> Sirasi ile nelerin yapilacagini numaralarda

### Entegrasyon
1. keycloak icin dependencyler , docker compose , resource
```
<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-oauth2-resource-server</artifactId>
		</dependency>
```
```
services:
  keycloak:
    image: quay.io/keycloak/keycloak:22.0.5
    container_name: local-keycloak
    environment:
      - KEYCLOAK_ADMIN=admin
      - KEYCLOAK_ADMIN_PASSWORD=p@ssw0rD!
    ports:
      - "8082:8080"
    command: start-dev
```

```
spring:
  security:
    oauth2:
      resourceserver:
        jwt:
          issuer-uri: http://localhost:8082/realms/Demo
```
2. keycloak uini acip realm olustur ve bu realma bir client(proje) yarat.
   client yaratilirken redirect uriye giris yapildiktan sonra donecek uriyi giriyoruz yani
> http://localhost:8080/*

keycloak ui'n REALM SETTING kisminda OpenID Endpoint Configuration var ordan gerekli tum linklere ulasabilirsin.
> application.yml icersine yazacagin **issuer-uri** de burda bulunuyor.

3. bu yaptigin ayarlar ve securitye yazdigin kodlar sayesinde backendde kullanici authenticated kullanici statusune gelir.
> video 11




