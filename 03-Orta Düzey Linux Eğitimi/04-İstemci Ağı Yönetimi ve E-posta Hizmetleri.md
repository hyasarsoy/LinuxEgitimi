# **4. Gün: İstemci Ağı Yönetimi ve E-posta Hizmetleri**

## **1. İstemci Ağı Yönetimi**

### **1.1 DHCP Yapılandırması ve İstemci Ayarları**

#### **DHCP Nedir?**
- Dynamic Host Configuration Protocol (DHCP), istemcilerin ağ üzerindeki IP adreslerini otomatik olarak almasını sağlar.

#### **DHCP Sunucu Kurulumu**
1. Gerekli paketlerin kurulumu:
   ```bash
   sudo apt install isc-dhcp-server
   ```
2. DHCP yapılandırma dosyasını düzenleme:
   ```bash
   sudo nano /etc/dhcp/dhcpd.conf
   ```
   Örnek yapılandırma:
   ```bash
   subnet 192.168.1.0 netmask 255.255.255.0 {
       range 192.168.1.100 192.168.1.200;
       option routers 192.168.1.1;
       option domain-name-servers 8.8.8.8, 8.8.4.4;
   }
   ```
3. Servisi başlatma ve test etme:
   ```bash
   sudo systemctl start isc-dhcp-server
   ```

---

### **1.2 PAM (Pluggable Authentication Modules) Yapılandırması**

#### **PAM Nedir?**
- PAM, kimlik doğrulama işlemlerini yönetmek için kullanılan modüler bir yapıdır.

#### **PAM Modül Dosyalarının Düzenlenmesi**
- PAM yapılandırma dosyaları `/etc/pam.d/` dizininde bulunur.
- Örnek `/etc/pam.d/common-auth` dosyası:
   ```plaintext
   auth required pam_unix.so
   ```

#### **Uygulama:**
- SSH bağlantısı için PAM ayarlarını kontrol edin:
   ```bash
   sudo nano /etc/ssh/sshd_config
   ```
   PAM'ı etkinleştirmek için şu satırı kontrol edin:
   ```plaintext
   UsePAM yes
   ```

---

### **1.3 LDAP İstemci ve OpenLDAP Sunucu Kurulumu**

#### **LDAP Nedir?**
- Lightweight Directory Access Protocol, merkezi kimlik doğrulama ve dizin hizmetleri sağlar.

#### **OpenLDAP Sunucu Kurulumu**
1. OpenLDAP paketini yükleme:
   ```bash
   sudo apt install slapd ldap-utils
   ```
2. OpenLDAP yapılandırmasını başlatma:
   ```bash
   sudo dpkg-reconfigure slapd
   ```
   - Domain adı: `example.com`
   - Admin şifresi: **Belirleyin.**

#### **LDAP İstemci Kurulumu**
1. İstemci paketlerini yükleme:
   ```bash
   sudo apt install libnss-ldap libpam-ldap ldap-utils
   ```
2. Yapılandırma sırasında:
   - LDAP sunucu URI: `ldap://<sunucu_adresi>`
   - Base DN: `dc=example,dc=com`

#### **Uygulama:**
- LDAP ile kimlik doğrulamayı test etmek için bir kullanıcı ekleyin:
   ```bash
   ldapadd -x -D "cn=admin,dc=example,dc=com" -W -f user.ldif
   ```

---

## **2. E-posta Hizmetleri**

### **2.1 E-posta Sunucusu Kurulumu (Postfix ve Dovecot)**

#### **Postfix Nedir?**
- SMTP protokolünü kullanarak e-posta gönderim işlemlerini yönetir.

#### **Postfix Kurulumu**
1. Postfix paketini yükleyin:
   ```bash
   sudo apt install postfix
   ```
2. Yapılandırma sırasında:
   - Genel e-posta sunucusu türü: "Internet Site".
   - Mail adı: `mail.example.com`.

#### **Dovecot Nedir?**
- IMAP ve POP3 protokollerini destekleyen bir e-posta sunucusudur.

#### **Dovecot Kurulumu**
1. Dovecot paketlerini yükleyin:
   ```bash
   sudo apt install dovecot-core dovecot-imapd dovecot-pop3d
   ```
2. Dovecot yapılandırmasını düzenleyin:
   ```bash
   sudo nano /etc/dovecot/dovecot.conf
   ```
   - `protocols = imap pop3` satırını kontrol edin.

#### **Uygulama:**
- E-posta sistemini test etmek için bir kullanıcı oluşturun ve e-posta gönderin.

---

### **2.2 E-posta Teslimatı ve Güvenlik Ayarları**

#### **SMTP Güvenlik Yapılandırması**
- TLS/SSL yapılandırması:
   ```bash
   sudo nano /etc/postfix/main.cf
   ```
   - `smtpd_tls_cert_file=/etc/ssl/certs/mail_cert.pem`
   - `smtpd_tls_key_file=/etc/ssl/private/mail_key.pem`

#### **IMAP/POP3 Güvenlik Ayarları**
- Dovecot SSL yapılandırması:
   ```bash
   sudo nano /etc/dovecot/conf.d/10-ssl.conf
   ```
   - `ssl = required`

#### **Uygulama:**
- OpenSSL ile e-posta sunucusu bağlantısını test edin:
   ```bash
   openssl s_client -starttls smtp -connect mail.example.com:587
   ```

---

### **2.3 Mailbox Yönetimi ve Test Etme**

#### **Kullanıcı Ekleme**
- Yeni bir kullanıcı ekleyin:
   ```bash
   sudo useradd -m emailuser
   sudo passwd emailuser
   ```

#### **E-posta Gönderimi ve Alımı**
- Postfix ve Dovecot'u test etmek için bir istemci (ör. Thunderbird) bağlayın.
- Örnek test e-postası gönderimi:
   ```bash
   echo "Test email" | mail -s "Subject" user@example.com
   ```

---

