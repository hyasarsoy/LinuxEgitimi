Tabii ki! Aşağıda 5. gün ders içeriğini detaylandıran ve yönlendirici bir şekilde düzenlenmiş `.md` formatındaki açıklayıcı ve uygulamalı içerik bulunmaktadır:

```markdown
# **5. Gün: Sistem Yönetimi ve Bakımı - 1. Bölüm**

## **1. Otomatikleştirilmiş Görevler: cron (1 Saat)**

### **1.1 cron ve Crontab Nedir?**
- `cron`, zamanlanmış görevleri otomatik olarak çalıştıran bir sistem hizmetidir.
- `crontab`, zamanlanmış görevlerin listesini düzenlemek için kullanılan bir araçtır.

### **1.2 crontab Kullanımı**
#### **Temel crontab Komutları**
- Crontab dosyasını düzenlemek:
  ```bash
  crontab -e
  ```
- Zamanlanmış görevleri listelemek:
  ```bash
  crontab -l
  ```
- Tüm görevleri silmek:
  ```bash
  crontab -r
  ```

#### **Crontab Formatı**
```
* * * * * komut
- - - - -
| | | | +-- Hafta günü (0-7, 0 = Pazar)
| | | +---- Ay (1-12)
| | +------ Gün (1-31)
| +-------- Saat (0-23)
+---------- Dakika (0-59)
```

#### **Uygulama: Otomatik Sistem Yedekleme**
- Örnek yedekleme komutu:
  ```bash
  0 2 * * * tar -czf /backup/system_$(date +\%F).tar.gz /home
  ```
- Bu görev, her gün saat 02:00'de `/home` dizinini `/backup` içine yedekler.

---

## **2. Sistem İzleme ve Performans Ölçümleri (2 Saat)**

### **2.1 Sistem İzleme Araçları**
#### **top Komutu**
- Anlık CPU, bellek ve süreç durumlarını görüntüler.
- Kullanım:
  ```bash
  top
  ```

#### **htop Komutu**
- Daha kullanıcı dostu bir sistem izleme aracı.
- Kullanım:
  ```bash
  htop
  ```

#### **vmstat Komutu**
- Bellek, CPU ve G/Ç durumu hakkında bilgi verir.
- Kullanım:
  ```bash
  vmstat 1
  ```

### **2.2 Performans Ölçümleri**
#### **Disk Performansı**
- `iostat` komutu:
  ```bash
  iostat -x 1
  ```

#### **Uygulama: Sistem İzleme**
- Sistemin CPU ve bellek kullanımını kontrol edin.
- Hangi süreçlerin en çok kaynak kullandığını tespit edin.

---

## **3. Sistem Günlüğü ve Log Yönetimi (2 Saat)**

### **3.1 Syslog Yapılandırması**
- Syslog, sistem mesajlarının kayıt altına alınmasını sağlar.
- Ana yapılandırma dosyası:
  ```plaintext
  /etc/rsyslog.conf
  ```

#### **Uygulama: Syslog Yapılandırması**
- Logları bir dosyaya yönlendirmek için `/etc/rsyslog.conf` dosyasına şu satırı ekleyin:
  ```plaintext
  *.info /var/log/custom.log
  ```
- Rsyslog'u yeniden başlatın:
  ```bash
  sudo systemctl restart rsyslog
  ```

### **3.2 journalctl ile Log Yönetimi**
- Sistem loglarını görüntülemek:
  ```bash
  journalctl
  ```
- Belirli bir servisin loglarını görüntülemek:
  ```bash
  journalctl -u nginx
  ```

### **3.3 logrotate ile Log Yönetimi**
- Log dosyalarının boyutunu ve saklama süresini yönetir.
- Ana yapılandırma dosyası:
  ```plaintext
  /etc/logrotate.conf
  ```

#### **Uygulama: Log Yönetimi**
- `/var/log` dizinindeki logları kontrol edin ve belirli bir anahtar kelimeyi arayın:
  ```bash
  grep "error" /var/log/syslog
  ```

---

## **4. Yedekleme ve Geri Yükleme Stratejileri (3 Saat)**

### **4.1 Yedekleme Türleri**
- **Tam Yedekleme:** Tüm sistemin bir kopyasını alır.
- **Artımlı Yedekleme:** Son yedeklemeden bu yana değişen dosyaları yedekler.
- **Fark Yedekleme:** Son tam yedeklemeden bu yana değişen dosyaları yedekler.

### **4.2 rsync ile Yedekleme**
- `rsync`, dosyaları ve dizinleri senkronize etmek için kullanılır.
- Örnek:
  ```bash
  rsync -av /source /destination
  ```

### **4.3 tar ile Yedekleme**
- `tar`, dosyaları sıkıştırılmış bir arşive dönüştürür.
- Örnek:
  ```bash
  tar -czvf backup.tar.gz /home
  ```

### **4.4 dd ile Disk Yedekleme**
- `dd`, diskleri birebir kopyalamak için kullanılır.
- Örnek:
  ```bash
  dd if=/dev/sda of=/backup/disk.img
  ```

### **Uygulama: Yedekleme ve Geri Yükleme**
1. `/home` dizinini yedekleyin:
   ```bash
   tar -czvf home_backup.tar.gz /home
   ```
2. Yedeklenen dosyayı geri yükleyin:
   ```bash
   tar -xzvf home_backup.tar.gz -C /
   ```

---

#