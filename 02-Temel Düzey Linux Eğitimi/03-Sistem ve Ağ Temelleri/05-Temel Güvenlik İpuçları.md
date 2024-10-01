# 05 - Temel Güvenlik İpuçları

Linux sistemlerinde güvenlik, kullanıcıların ve yöneticilerin dikkat etmesi gereken önemli bir konudur. Sistemlerinize yetkisiz erişimleri engellemek ve hassas verileri korumak için belirli güvenlik önlemlerini almanız gerekir. Bu kılavuzda, Linux sistemleri için temel güvenlik ipuçlarına yer verilecektir.

---

## 1. Kullanıcı Hesaplarını ve Yetkilerini Yönetme

### 1.1 Güçlü Parolalar Kullanma

- **Parola politikaları:** Tüm kullanıcıların karmaşık ve güçlü parolalar kullanmasını sağlamak için parola politikaları uygulayın.
- **Parola süresi:** Parolaların belirli bir süre sonra yenilenmesini zorunlu kılın.

Komut örneği:
```bash
sudo passwd [kullanıcı_adı]
```

### 1.2 Root Kullanıcısını Kısıtlayın

- Root kullanıcısını doğrudan kullanmak yerine, `sudo` komutunu kullanarak gerekli izinleri geçici olarak elde edin.
- Root erişimini sınırlandırmak için /etc/sudoers dosyasını düzenleyin.

---

## 2. Güvenlik Güncellemelerini Düzenli Yapma

### 2.1 Paket Yöneticisi ile Güncellemeler

Sisteminizdeki yazılımların en güncel sürümlerini kullanmak, bilinen güvenlik açıklarını kapatır.

- Debian tabanlı sistemlerde:
  ```bash
  sudo apt update && sudo apt upgrade
  ```

- Red Hat tabanlı sistemlerde:
  ```bash
  sudo yum update
  ```

### 2.2 Otomatik Güncelleme Ayarlama

Sisteminizin güvenliğini sağlamak için otomatik güncelleme yapılandırabilirsiniz.

---

## 3. Güvenlik Duvarı (Firewall) Kullanın

### 3.1 `ufw` (Uncomplicated Firewall) Kullanın

`ufw`, kullanıcı dostu bir güvenlik duvarı yönetim aracıdır. Temel ağ bağlantılarını sınırlandırmak ve istenmeyen trafiği engellemek için `ufw`'yi kullanabilirsiniz.

- `ufw`'yi etkinleştirmek:
  ```bash
  sudo ufw enable
  ```

- Belirli bir portu açmak:
  ```bash
  sudo ufw allow 22/tcp
  ```

### 3.2 `iptables` ile Güvenlik Duvarı Yönetimi

Daha gelişmiş güvenlik duvarı ayarları yapmak için `iptables` kullanılabilir.

---

## 4. SSH Güvenliği

### 4.1 Varsayılan Portu Değiştirin

SSH servisinin çalıştığı varsayılan portu değiştirmek, saldırganların sisteminizi keşfetmesini zorlaştırır.

- `/etc/ssh/sshd_config` dosyasını düzenleyerek SSH portunu değiştirin:
  ```bash
  sudo nano /etc/ssh/sshd_config
  ```
  ```
  Port 2222
  ```

### 4.2 SSH Anahtar Doğrulaması Kullanın

Parola yerine SSH anahtarlarıyla giriş yapmak daha güvenlidir.

- SSH anahtar çifti oluşturmak:
  ```bash
  ssh-keygen -t rsa
  ```

---

## 5. Log ve İzleme

### 5.1 Log Dosyalarını Takip Etme

Sistemde meydana gelen olayları takip etmek için log dosyalarını düzenli olarak kontrol edin.

- `/var/log` dizinindeki dosyaları incelemek:
  ```bash
  sudo tail -f /var/log/syslog
  ```

### 5.2 Fail2Ban Kullanımı

Fail2Ban, başarısız oturum açma denemelerine karşı koruma sağlar ve belirli bir sayıdaki başarısız denemeden sonra IP adreslerini engeller.

- Fail2Ban'i yüklemek:
  ```bash
  sudo apt install fail2ban
  ```

- Varsayılan ayarları yapılandırmak için `/etc/fail2ban/jail.conf` dosyasını düzenleyin.

---

## 6. Yedekleme Stratejileri

### 6.1 Yedekleme Yapın

Her zaman önemli dosyalarınızın yedeklerini alın ve kritik sistem verilerini güvenli bir şekilde saklayın. Yedekleme stratejisi, olası veri kayıplarına karşı koruma sağlar.

### 6.2 Otomatik Yedekleme

Düzenli olarak yedek almak için `cron` ile otomatik yedekleme görevleri ayarlayın.

---
