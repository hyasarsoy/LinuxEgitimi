# Yönetimsel İşlemler

Linux sistemlerinde yönetimsel işlemler, bir sistem yöneticisinin günlük olarak gerçekleştirdiği temel görevlerden bazılarını içerir. Bu görevler, kullanıcı ve grup hesaplarını yönetme, sistemin otomatikleştirilmiş işlevlerini kontrol etme ve yerelleştirme gibi işlemleri kapsar.

## 1. Kullanıcı ve Grup Hesaplarını ve İlgili Sistem Dosyalarını Yönetme

Kullanıcı ve grup hesaplarının yönetimi, sistemdeki kullanıcıların güvenli ve etkili bir şekilde çalışmasını sağlar. Aşağıdaki temel komutlar, kullanıcı ve grup yönetimi için yaygın olarak kullanılır:

### Kullanıcı Hesapları:
- Yeni bir kullanıcı oluşturmak:
  ```bash
  sudo adduser [kullanıcı_adı]
  ```

- Kullanıcıyı silmek:
  ```bash
  sudo deluser [kullanıcı_adı]
  ```

### Grup Yönetimi:
- Yeni bir grup oluşturmak:
  ```bash
  sudo addgroup [grup_adı]
  ```

- Kullanıcıyı gruba eklemek:
  ```bash
  sudo usermod -aG [grup_adı] [kullanıcı_adı]
  ```

### Sistem Dosyaları:
Kullanıcı ve grup bilgileri genellikle `/etc/passwd`, `/etc/shadow` ve `/etc/group` dosyalarında saklanır.

---

## 2. Sistem Yönetim Görevlerini Otomatikleştirme (Cron İşleri)

Sistem yöneticileri, belirli görevlerin otomatik olarak yapılmasını sağlamak için zamanlanmış işlerle (`cron`) çalışırlar. Bu, günlük yedekleme işlemleri, sistem güncellemeleri gibi görevlerin belirli zamanlarda çalıştırılmasını sağlar.

### Cron İşleri:
- `crontab` dosyasını düzenlemek için:
  ```bash
  crontab -e
  ```

- Örnek cron görevi: Her gün saat 3'te bir yedekleme komutunu çalıştırmak:
  ```bash
  0 3 * * * /usr/local/bin/backup.sh
  ```

Cron görevleri zamanlanırken şu format kullanılır:
```
* * * * * komut
| | | | |
| | | | +-- Yılın günü (0-7) (0 ve 7 Pazar anlamına gelir)
| | | +---- Ay (1 - 12)
| | +------ Ayın günü (1 - 31)
| +-------- Saat (0 - 23)
+---------- Dakika (0 - 59)
```

---

## 3. Yerelleştirme ve Uluslararasılaştırma İşlemleri

Yerelleştirme, bir sistemin dil, saat dilimi ve diğer bölgesel ayarlarını yapılandırmayı içerir. Bu işlemler, sistemin bulunduğu bölgeye göre çalışmasını sağlar.

### Saat Dilimi Ayarları:
- Saat dilimini ayarlamak için:
  ```bash
  sudo timedatectl set-timezone Europe/Istanbul
  ```

### Dil ve Yerelleştirme:
- Yerelleştirme ayarlarını yapılandırmak için:
  ```bash
  sudo dpkg-reconfigure locales
  ```

Sistem yöneticileri bu ayarları yaparak, kullanıcıların ve sistemin bulunduğu coğrafi bölgeye uygun çalışmasını sağlayabilirler.
