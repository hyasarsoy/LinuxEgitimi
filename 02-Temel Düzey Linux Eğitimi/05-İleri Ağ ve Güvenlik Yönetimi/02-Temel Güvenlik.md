# Temel Güvenlik

Temel güvenlik, bir sistemin ve ağın güvenliğini sağlamak için uygulanması gereken en iyi uygulamaları ve teknikleri içerir. Bu bölümde SSH güvenliği, güvenlik duvarı yapılandırmaları ve ağ güvenliği konularına odaklanacağız.

## 1. SSH Güvenliği ve Anahtar Yönetimi

**SSH (Secure Shell)**, güvenli bir ağ üzerinden başka bir bilgisayara erişim sağlamak için kullanılan bir protokoldür. SSH'nin güvenliğini artırmak için bazı en iyi uygulamalar:

- **Anahtar Tabanlı Kimlik Doğrulama**: Parola yerine anahtar kullanmak, daha güvenli bir bağlantı sağlar. Anahtar çiftleri (özel ve genel anahtar) kullanılır.
  - Anahtar oluşturma:
    ```bash
    ssh-keygen -t rsa -b 4096
    ```
  - Genel anahtarın uzak sunucuya kopyalanması:
    ```bash
    ssh-copy-id user@remote-server
    ```

- **Parola Güvenliği**: Parolalar karmaşık ve güçlü olmalı, gereksiz yere uzun süre kullanılmamalıdır.

- **SSH Yapılandırması**: `/etc/ssh/sshd_config` dosyasında yapılacak ayarlar ile SSH güvenliği artırılabilir. Örneğin:
  - Parola kimlik doğrulamasını devre dışı bırakmak:
    ```plaintext
    PasswordAuthentication no
    ```

---

## 2. Güvenlik Duvarı Yapılandırmaları

Güvenlik duvarı, bir ağın dışarıdan gelen ve giden trafiğini kontrol eden bir güvenlik sistemidir. Linux sistemlerinde yaygın olarak kullanılan güvenlik duvarı araçları arasında **iptables** ve **firewalld** bulunmaktadır.

### Iptables Kullanımı
- **Kural ekleme**: Belirli bir portu açmak için:
  ```bash
  iptables -A INPUT -p tcp --dport 22 -j ACCEPT
  ```

- **Kural silme**: Belirli bir kuralı silmek için:
  ```bash
  iptables -D INPUT -p tcp --dport 22 -j ACCEPT
  ```

- **Tüm kuralları listeleme**:
  ```bash
  iptables -L -v
  ```

### Firewalld Kullanımı
- **Port açma**: Firewalld kullanarak belirli bir portu açmak için:
  ```bash
  firewall-cmd --zone=public --add-port=22/tcp --permanent
  firewall-cmd --reload
  ```

- **Tüm kuralları listeleme**:
  ```bash
  firewall-cmd --list-all
  ```

---

## 3. Ağ Güvenliği ve İzinsiz Giriş Tespiti

Ağ güvenliği, ağın yetkisiz erişim ve saldırılara karşı korunmasını sağlar. Bu, izinsiz giriş tespit sistemleri (IDS) ve diğer güvenlik çözümleri ile sağlanabilir.

### İzinsiz Giriş Tespit Sistemleri (IDS)
IDS, ağ trafiğini izler ve potansiyel güvenlik tehditlerini tespit eder. Popüler IDS araçları arasında **Snort** ve **Suricata** bulunur.

- **Snort Kullanımı**:
  - Snort'ı kurmak ve yapılandırmak için:
    ```bash
    apt install snort
    ```

  - Temel bir Snort komutuyla ağ trafiğini izlemek:
    ```bash
    snort -i eth0 -c /etc/snort/snort.conf
    ```

### Güvenlik İpuçları
- **Güvenlik güncellemeleri**: Sistemdeki yazılımları ve güvenlik yamalarını düzenli olarak güncelleyin.
- **Zayıf Parolalar**: Parola politikalarını uygulayın ve zayıf parolaların kullanımını engelleyin.
- **Güvenli Protokoller**: HTTPS, FTPS gibi güvenli protokollerin kullanılmasını teşvik edin.

Bu temel güvenlik önlemleri, sistemlerinizi ve ağlarınızı korumak için önemli birer adımdır.
```