```markdown
# **Syslog Sunucusu Hazırlama Projesi**

Bu proje, bir Linux sunucusunda Syslog sunucusu kurulumunu ve yapılandırmasını içermektedir. Firewall loglarının yönlendirilmesi, gelen logların doğrulanması, yedeklenmesi ve 5651 sayılı kanuna uygun şekilde imzalanması hedeflenmiştir. Ayrıca tüm süreçlerin durumu e-posta ile raporlanacaktır.

---

## **Adımlar**

### **1. Firewall'dan Log Yönlendirme**
- Firewall üzerinde logların Syslog sunucusuna yönlendirilmesi için aşağıdaki adımlar izlenir:

#### **Firewall Yönlendirme Ayarları:**
1. Firewall cihazına erişim sağlayın.
2. Syslog sunucusunun IP adresini belirleyin (örnek: `192.168.1.100`).
3. Firewall üzerinde logları Syslog sunucusuna yönlendirmek için uygun ayarları yapılandırın:
   - **Örnek komut:**
     ```bash
     set logging server 192.168.1.100 514
     ```

4. Yönlendirme protokolü olarak TCP veya UDP kullanılabilir. TCP daha güvenli bir iletim sağlar.

---

### **2. Linux Üzerinde Syslog Server Kurulumu**
- **Rsyslog** en yaygın kullanılan Syslog sunucularından biridir ve kolayca yapılandırılabilir.

#### **Rsyslog Kurulumu:**
1. Rsyslog'u yükleyin:
   ```bash
   sudo apt update
   sudo apt install rsyslog -y
   ```

2. Rsyslog'u 514 numaralı portu dinleyecek şekilde yapılandırın:
   - `/etc/rsyslog.conf` dosyasını düzenleyin:
     ```bash
     sudo nano /etc/rsyslog.conf
     ```
   - Aşağıdaki satırların yorum işaretlerini kaldırın:
     ```plaintext
     # Provides TCP syslog reception
     module(load="imtcp")
     input(type="imtcp" port="514")
     ```

3. Rsyslog'u yeniden başlatın:
   ```bash
   sudo systemctl restart rsyslog
   ```

4. Firewall'da 514 portunu açın:
   ```bash
   sudo firewall-cmd --add-port=514/tcp --permanent
   sudo firewall-cmd --reload
   ```

---

### **3. TCPDUMP ile Portların Kontrolü**
1. 514 portuna logların gelip gelmediğini kontrol edin:
   ```bash
   sudo tcpdump -i any port 514
   ```
   - Gelen logları görmek için komutu çalıştırın. Eğer loglar geliyorsa, firewall yönlendirme işlemi başarıyla tamamlanmıştır.

---

### **4. Gelen Logların /var/log Altına Yedeklenmesi**
1. Gelen logların `/var/log` altına kaydedilmesi için aşağıdaki adımları izleyin:
   - `/etc/rsyslog.d/50-default.conf` dosyasını düzenleyin:
     ```bash
     sudo nano /etc/rsyslog.d/50-default.conf
     ```
   - Aşağıdaki kuralı ekleyin:
     ```plaintext
     if $fromhost-ip == 'firewall_ip' then /var/log/firewall.log
     & stop
     ```
   - Yerine `firewall_ip` kısmına firewall cihazınızın IP adresini yazın.

2. Rsyslog'u yeniden başlatın:
   ```bash
   sudo systemctl restart rsyslog
   ```

---

### **5. Logların Günlük İmzalanması (5651 Kanunu)**
1. Günlük log dosyalarını zaman damgası ile imzalamak için bir cron görevi oluşturun:
   - İmza için OpenSSL kullanabilirsiniz.

#### **Örnek Komutlar:**
1. Günlük log dosyasını imzalama:
   ```bash
   openssl dgst -sha256 -sign /path/to/private_key.pem -out /var/log/firewall_$(date +%F).sig /var/log/firewall.log
   ```
   - **private_key.pem:** İmza için kullanılan özel anahtar.

2. Günlük olarak otomatik çalıştırmak için cron görevi ekleyin:
   ```bash
   sudo crontab -e
   ```
   - Aşağıdaki satırı ekleyin:
     ```plaintext
     0 0 * * * openssl dgst -sha256 -sign /path/to/private_key.pem -out /var/log/firewall_$(date +%F).sig /var/log/firewall.log
     ```

---

### **6. E-posta İle Bildirim Gönderimi**
1. Sistemin e-posta gönderimi yapabilmesi için `mailutils` paketini yükleyin:
   ```bash
   sudo apt install mailutils -y
   ```

2. Başarılı veya başarısız durumlara göre e-posta göndermek için bir betik hazırlayın:

#### **Kontrol ve Bildirim Betiği:**
- `log_check.sh` adında bir dosya oluşturun:
  ```bash
  sudo nano /home/log_check.sh
  ```

- Betik içeriği:
  ```bash
  #!/bin/bash

  LOG_FILE="/var/log/firewall.log"
  SIGNATURE_FILE="/var/log/firewall_$(date +%F).sig"

  # Log dosyasını kontrol et
  if [ -f "$LOG_FILE" ] && [ -s "$LOG_FILE" ]; then
      echo "Log dosyası mevcut ve dolu." | mail -s "Log İşlemi Başarılı" admin@example.com
  else
      echo "Log dosyası mevcut değil veya boş." | mail -s "Log İşlemi Hatalı" admin@example.com
  fi

  # İmza dosyasını kontrol et
  if [ -f "$SIGNATURE_FILE" ]; then
      echo "İmza dosyası oluşturuldu." | mail -s "İmza İşlemi Başarılı" admin@example.com
  else
      echo "İmza dosyası oluşturulamadı." | mail -s "İmza İşlemi Hatalı" admin@example.com
  fi
  ```

3. Betiği çalıştırılabilir yapın:
   ```bash
   sudo chmod +x /home/log_check.sh
   ```

4. Bu betiği günlük olarak çalıştırmak için cron'a ekleyin:
   ```bash
   sudo crontab -e
   ```
   - Aşağıdaki satırı ekleyin:
     ```plaintext
     0 0 * * * /home/log_check.sh
     ```

---

## **Sonuç**
Bu proje tamamlandığında:
- Firewall logları Syslog sunucusuna başarıyla yönlendirilecektir.
- Gelen loglar doğrulanacak ve yedeklenecektir.
- Loglar her gece imzalanarak 5651 kanununa uygun şekilde saklanacaktır.
- Tüm süreçlerin durumu e-posta ile bildirilecektir.
```