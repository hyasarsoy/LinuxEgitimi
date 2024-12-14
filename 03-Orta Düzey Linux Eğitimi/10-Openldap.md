# OpenLDAP Sunucusu Kurulumu ve Yapılandırması (Ubuntu)

Bu kılavuz, Ubuntu üzerinde OpenLDAP sunucusunun kurulumu ve yapılandırılması için adım adım talimatları içerir.

## Ön Gereksinimler

- **Ubuntu Server:** 22.04 veya daha güncel bir sürüm.
- **Root veya Sudo Yetkisi:** Komutları çalıştırabilmek için gerekli.
- **Sabit IP Adresi:** OpenLDAP sunucusunun düzgün çalışabilmesi için.

---

## 1. Hostname Ayarları

OpenLDAP kurulumu sırasında hostname bilgisi kullanılacağı için öncelikle hostname yapılandırılmalıdır.

### A. Hostname Kontrolü

Mevcut hostname'i kontrol etmek için aşağıdaki komutu kullanabilirsiniz:

```bash
hostnamectl status
```

### B. Hostname Değiştirme

Hostname'i değiştirmek için:

```bash
sudo hostnamectl set-hostname ldap.example.com
```

Değişiklikleri yansıtmak için `/etc/hosts` dosyasını düzenleyin ve hostname'i IP adresinizle eşleştirin:

```bash
sudo nano /etc/hosts
```

Dosyanın içeriği şu şekilde olmalıdır:

```
127.0.0.1   localhost
192.168.1.100 ldap.example.com ldap
```

Değişiklikleri kaydedip kapatın.

---

## 2. OpenLDAP Sunucusunun Kurulumu

### A. Gerekli Paketlerin Yüklenmesi

```bash
sudo apt update
sudo apt install slapd ldap-utils -y
```

### B. OpenLDAP Yapılandırma Sihirbazı

Kurulum sırasında yapılandırma sihirbazı otomatik olarak başlatılabilir. Eğer başlamazsa aşağıdaki komutla çalıştırabilirsiniz:

```bash
sudo dpkg-reconfigure slapd
```

#### Sihirbazdaki Ayarlar:
1. **"Oluşturulacak yapılandırmaları kaldırmak ister misiniz?"**: Hayır.
2. **DNS Domain Adı:** Örneğin, `example.com`.
3. **Kuruluş Adı:** Örneğin, `Example Inc.`.
4. **Yönetici Şifresi:** Güçlü bir şifre belirleyin.
5. **Veritabanını yerel erişime sınırlandır?**: Evet.
6. **Eski veritabanını kaldır?**: Evet.
7. **HDB yerine MDB kullanılsın mı?**: Evet.

---

## 3. OpenLDAP Sunucusunun Temel Yapılandırması

### A. LDAP Sunucusunu Kontrol Etme

Kurulumdan sonra OpenLDAP hizmetinin durumunu kontrol edin:

```bash
sudo systemctl status slapd
```

### B. LDAP Şemasını Doğrulama

Aşağıdaki komutla yapılandırmayı kontrol edebilirsiniz:

```bash
sudo slapcat
```

Bu komut mevcut veritabanını LDIF formatında görüntüler.

---

## 4. LDAP Veritabanı Yönetimi

### A. LDAP Yapılandırmasını Güncelleme

OpenLDAP'ın yapılandırması `/etc/ldap/slapd.d/` dizininde saklanır. Güncellemeleri yapmak için LDIF dosyalarını kullanabilirsiniz.

Örneğin, yeni bir organizasyon birimi (OU) eklemek için:

**`add_ou.ldif` İçeriği:**

```ldif
dn: ou=users,dc=example,dc=com
objectClass: organizationalUnit
ou: users
```

Komutu çalıştırın:

```bash
sudo ldapadd -x -D "cn=admin,dc=example,dc=com" -W -f add_ou.ldif
```

Şifre sorulduğunda, kurulum sırasında belirlediğiniz yönetici şifresini girin.

---

## 5. LDAP Kullanıcıları Ekleme

Yeni bir kullanıcı eklemek için aşağıdaki örneği kullanabilirsiniz.

**`add_user.ldif` İçeriği:**

```ldif
dn: uid=jdoe,ou=users,dc=example,dc=com
objectClass: inetOrgPerson
uid: jdoe
sn: Doe
givenName: John
cn: John Doe
userPassword: {SSHA}şifre
mail: jdoe@example.com
```

LDIF dosyasını eklemek için:

```bash
sudo ldapadd -x -D "cn=admin,dc=example,dc=com" -W -f add_user.ldif
```

> **Not:** `userPassword` alanı için SSHA şifreleme kullanabilirsiniz. Şifre oluşturmak için:
>
> ```bash
> slappasswd
> ```

---

## 6. LDAP İstemci Kurulumu ve Testi

### A. İstemci Paketlerini Yükleme

LDAP istemci araçlarını yüklemek için:

```bash
sudo apt install ldap-utils -y
```

### B. LDAP Sunucusuna Bağlanma

LDAP sunucusuna bağlanmayı test edin:

```bash
ldapsearch -x -LLL -H ldap://localhost -b "dc=example,dc=com"
```

Bu komut, LDAP sunucusundaki tüm girdileri listeleyecektir.

---

## 7. Güvenlik ve SSL/TLS Ayarları

### A. Sertifika Oluşturma ve Yapılandırma

Self-signed sertifika oluşturmak için:

```bash
sudo openssl req -new -x509 -days 365 -nodes -out /etc/ssl/certs/ldap.pem -keyout /etc/ssl/private/ldap.key
```

OpenLDAP yapılandırmasına sertifikayı ekleyin. Yeni bir LDIF dosyası oluşturun:

**`tls_config.ldif` İçeriği:**

```ldif
dn: cn=config
changetype: modify
add: olcTLSCertificateFile
olcTLSCertificateFile: /etc/ssl/certs/ldap.pem
-
add: olcTLSCertificateKeyFile
olcTLSCertificateKeyFile: /etc/ssl/private/ldap.key
```

Yapılandırmayı uygulayın:

```bash
sudo ldapmodify -Y EXTERNAL -H ldapi:/// -f tls_config.ldif
```

OpenLDAP hizmetini yeniden başlatın:

```bash
sudo systemctl restart slapd
```

---

## 8. LDAP Yönetim Araçları

- **phpLDAPadmin:** Web tabanlı bir LDAP yönetim aracı.
  
  Kurulum:
  
  ```bash
  sudo apt install phpldapadmin -y
  ```

  Yapılandırma dosyasını düzenleyin:

  ```bash
  sudo nano /etc/phpldapadmin/config.php
  ```

  `"cn=admin,dc=example,dc=com"` yapılandırmasını uygun şekilde düzenleyin.

  Sunucuyu yeniden başlatın:

  ```bash
  sudo systemctl restart apache2
  ```

---

## 9. Sorun Giderme

### A. Logları İnceleme

Hataları çözmek için logları kontrol edin:

```bash
sudo tail -f /var/log/syslog
```

### B. Hizmet Durumu

OpenLDAP hizmetinin düzgün çalıştığından emin olun:

```bash
sudo systemctl status slapd
```
