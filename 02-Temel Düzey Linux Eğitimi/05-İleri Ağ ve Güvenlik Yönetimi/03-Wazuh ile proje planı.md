##1-  Wazuh: Açık Kaynak Güvenlik Platformu

## Wazuh Nedir?

**Wazuh**, **saldırı tespiti**, **tehdit istihbaratı** ve **log yönetimi** için tasarlanmış, açık kaynaklı bir güvenlik izleme platformudur. Güvenlik izleme, olay tespiti, uyumluluk yönetimi ve daha fazlası için kapsamlı bir çözüm sunar. Wazuh, uç noktaları, bulut ortamlarını ve yerel altyapıyı gerçek zamanlı izleyerek, sürekli tehdit algılama ve yanıt sağlamak amacıyla güvenliği temin eder.

### Ana Özellikler:

- **Saldırı Tespit Sistemi (IDS)**: Altyapınızda yetkisiz erişim veya saldırı belirtilerini izler.
- **Log Yönetimi**: Sistem ve uygulamalardan gelen günlükleri toplar, analiz eder ve saklar.
- **Tehdit İstihbaratı**: Yeni tehditlere karşı bilgi toplayarak hızlı yanıt ve savunma sağlar.
- **Uyumluluk Yönetimi**: Güvenlik ve uyumluluk standartlarını karşılamanıza yardımcı olur (PCI DSS, HIPAA, GDPR, vb.).
- **Güvenlik Olayı ve Olay Yanıtı (SIEM)**: Olayları analiz ederek, güvenlik olaylarını yönetir ve çözüm üretir.

## Wazuh Kurulumu

Aşağıda, Wazuh sunucusunun kurulumunu gerçekleştirmek için bir Bash scripti bulunmaktadır. Bu script, Wazuh'un en son sürümünü indirip gerekli bağımlılıkları kurarak sistemi hazır hale getirir.

### Kurulum Scripti:

```bash
#!/bin/bash

# Wazuh Sunucusunu Kurmak İçin Script
# Güncelleme ve gerekli paketlerin kurulumu
sudo apt-get update
sudo apt-get install -y curl apt-transport-https

# Wazuh depo anahtarlarını ekleme
curl -s https://packages.wazuh.com/key/GPG-KEY-WAZUH | sudo apt-key add -

# Wazuh deposunu ekleme
echo "deb https://packages.wazuh.com/4.x/apt/ stable main" | sudo tee /etc/apt/sources.list.d/wazuh.list

# Wazuh sunucusunun kurulumu
sudo apt-get update
sudo apt-get install -y wazuh-manager

# Wazuh sunucusunu başlatma
sudo systemctl enable wazuh-manager
sudo systemctl start wazuh-manager

# Kurulum tamamlandı!
echo "Wazuh sunucusu başarıyla kuruldu ve çalışıyor!"
```

### Kurulum Adımları:

1. **Adım 1:** Yukarıdaki scripti bir dosyaya kaydedin. Örneğin, `wazuh-kurulum.sh` olarak adlandırabilirsiniz.
   
2. **Adım 2:** Script dosyasını çalıştırılabilir hale getirin:
   ```bash
   chmod +x wazuh-kurulum.sh
   ```

3. **Adım 3:** Scripti çalıştırın:
   ```bash
   sudo ./wazuh-kurulum.sh
   ```

4. **Adım 4:** Kurulum tamamlandığında Wazuh sunucunuz çalışmaya başlayacak. Kontrol etmek için şu komutu kullanabilirsiniz:
   ```bash
   sudo systemctl status wazuh-manager
   ```

Kurulum tamamlandıktan sonra, Wazuh Web arayüzünü kurarak merkezi yönetim ve izleme işlevlerini de kullanabilirsiniz.
```


# 2- Ubuntu Üzerinde Syslog Yapılandırması ve Wazuh'a Log Yönlendirme

Bu belge, Ubuntu üzerinde **Rsyslog** kullanarak logların bir Wazuh sunucusuna nasıl yönlendirileceğini açıklamaktadır. Bu sayede, sistem günlüklerini merkezi olarak toplayıp analiz edebilirsiniz.

## 1. Rsyslog'un Kurulumu ve Yapılandırılması

### 1.1 Rsyslog Kurulumu

Ubuntu genellikle **Rsyslog** ile gelir. Ancak, Rsyslog kurulu değilse, şu komutla kurabilirsiniz:

```bash
sudo apt-get update
sudo apt-get install rsyslog
```

### 1.2 Rsyslog Yapılandırması

Logları Wazuh sunucusuna yönlendirmek için `/etc/rsyslog.d/` dizininde yeni bir yapılandırma dosyası oluşturmanız gerekmektedir:

```bash
sudo nano /etc/rsyslog.d/wazuh.conf
```

Bu dosyaya aşağıdaki satırları ekleyin:

#### UDP Üzerinden Log Yönlendirme:
```bash
*.*  @<WAZUH_IP>:514
```

#### TCP Üzerinden Log Yönlendirme:
```bash
*.*  @@<WAZUH_IP>:514
```

- `<WAZUH_IP>`: Wazuh sunucusunun IP adresi ile değiştirilmelidir.
- `@`: UDP protokolü için kullanılır.
- `@@`: TCP protokolü için kullanılır.

Bu yapılandırma, tüm logları (`*.*`) Wazuh sunucusuna yönlendirecektir. İsterseniz belirli bir log seviyesini veya kaynağı yönlendirebilirsiniz (örn. sadece hata loglarını).

### 1.3 Rsyslog Servisini Yeniden Başlatma

Yapılandırmayı uyguladıktan sonra Rsyslog servisini yeniden başlatın:

```bash
sudo systemctl restart rsyslog
```

## 2. Wazuh Sunucusunda Syslog Alımını Yapılandırma

Wazuh, syslog verilerini toplamak için yapılandırılabilir. Bunun için **Wazuh sunucusundaki** `ossec.conf` dosyasına bir yapılandırma eklemeniz gerekecektir.

### 2.1 Wazuh Yapılandırması

Wazuh sunucusunda `/var/ossec/etc/ossec.conf` dosyasını düzenleyin:

```bash
sudo nano /var/ossec/etc/ossec.conf
```

Dosyanın içine şu XML bloğunu ekleyin:

```xml
<remote>
  <connection>syslog</connection>
  <port>514</port>
  <protocol>udp</protocol>
</remote>
```

- **Port 514**: Varsayılan syslog portudur. Aynı portun Rsyslog yapılandırmasında da kullanıldığından emin olun.
- **UDP/TCP**: Kullanmak istediğiniz protokolü belirtin (`udp` veya `tcp`).

### 2.2 Wazuh Sunucusunu Yeniden Başlatma

Değişiklikleri uygulamak için Wazuh sunucusunu yeniden başlatın:

```bash
sudo systemctl restart wazuh-manager
```

## 3. Log Yönlendirme Doğrulaması

Ubuntu makinesinden gelen logların Wazuh sunucusuna ulaştığından emin olmak için birkaç adım izleyebilirsiniz:

1. **Manuel Log Oluşturma:**
   Bir test logu oluşturarak syslog'un doğru şekilde çalışıp çalışmadığını test edin:

   ```bash
   logger "Bu bir test log mesajıdır."
   ```

2. **Wazuh Sunucusunda Log Kontrolü:**
   Wazuh sunucusuna gidin ve şu dosyaları kontrol edin:

   - `/var/ossec/logs/ossec.log`
   - `/var/ossec/logs/alerts/alerts.log`

   Test mesajınızın burada görünüp görünmediğini kontrol edin.


