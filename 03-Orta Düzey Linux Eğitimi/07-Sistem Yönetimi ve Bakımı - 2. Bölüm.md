# **6. Gün: Sistem Yönetimi ve Bakımı - 2. Bölüm**

## **1. Paket Yönetimi ve Yazılım Güncellemeleri**

### **1.1 Paket Yönetimi Nedir?**
- Paket yöneticileri, yazılımları yüklemek, güncellemek, kaldırmak ve yönetmek için kullanılan araçlardır.
- Yaygın kullanılan paket yöneticileri:
  - Debian tabanlı sistemler için `apt`
  - Red Hat tabanlı sistemler için `yum` ve `dnf`

### **1.2 Paket Yönetim Komutları**
#### **Debian Tabanlı Sistemlerde (apt)**
- Paket listesini güncelle:
  ```bash
  sudo apt update
  ```
- Paketleri yükselt:
  ```bash
  sudo apt upgrade
  ```
- Yeni bir paket yükle:
  ```bash
  sudo apt install <paket_adı>
  ```

#### **Red Hat Tabanlı Sistemlerde (yum/dnf)**
- Paket listesini güncelle:
  ```bash
  sudo yum update
  ```
- Yeni bir paket yükle:
  ```bash
  sudo yum install <paket_adı>
  ```

### **1.3 Uygulama: Yazılım Güncellemeleri ve Paket Yönetimi**
- Tüm sistem güncellemelerini tek bir komutla gerçekleştirin:
  ```bash
  sudo apt update && sudo apt upgrade -y
  ```
- Gereksiz paketleri temizleyin:
  ```bash
  sudo apt autoremove
  ```

---

## **2. E-posta Sistem Hizmetleri**

### **2.1 Mail Transfer Agent (MTA) Nedir?**
- MTA, e-postaların bir sistemden başka bir sisteme taşınmasını sağlar.
- Yaygın kullanılan MTA’lar: `Postfix`, `Sendmail`, `Exim`.

### **2.2 Postfix ile E-posta Hizmetleri**
#### **Postfix Kurulumu**
- Postfix'i yükleyin:
  ```bash
  sudo apt install postfix
  ```
- Ana yapılandırma dosyasını düzenleyin:
  ```plaintext
  /etc/postfix/main.cf
  ```

#### **Sistem Bildirimleri için E-posta**
- Test e-postası gönderme:
  ```bash
  echo "Test mesajı" | mail -s "Test Başlığı" user@example.com
  ```

### **2.3 Uygulama: Sistem Uyarıları için E-posta**
1. Sistem loglarında belirli olayları izleyin.
2. Belirli bir olay gerçekleştiğinde bir uyarı e-postası gönderin:
   ```bash
   echo "Dikkat! Disk kullanımı kritik seviyeye ulaştı." | mail -s "Disk Uyarısı" admin@example.com
   ```

---

## **3. Kapasite Planlama (4 Saat)**

### **3.1 Kapasite Planlama Nedir?**
- Sistem kaynaklarının mevcut kullanımını ölçerek gelecekteki ihtiyaçları tahmin etme.
- Kritik sistem kaynakları:
  - CPU
  - RAM
  - Disk alanı
  - Ağ bant genişliği

### **3.2 Kaynak Kullanımını İzleme**
#### **CPU Kullanımı**
- `mpstat` komutu:
  ```bash
  mpstat
  ```

#### **RAM Kullanımı**
- Bellek kullanımını kontrol etme:
  ```bash
  free -h
  ```

#### **Disk Kullanımı**
- Disk doluluğunu izleme:
  ```bash
  df -h
  ```

#### **Ağ Kullanımı**
- Bant genişliği kullanımı:
  ```bash
  iftop
  ```

### **3.3 Kapasite Planlama için Örnekler**
#### **Günlük Sistem Kaynak Kullanımı Raporu**
1. Kaynak kullanımını bir dosyaya kaydetmek için bir cron görevi ekleyin:
   ```bash
   0 * * * * top -b -n1 >> /var/log/system_usage.log
   ```

#### **Büyüme Planları için Tahmin**
- Disk büyümesini analiz etmek için geçmiş kullanım verilerini toplayın.
- Yeni kullanıcıların eklenmesi veya uygulama yükünün artışı gibi senaryolara göre kaynak ihtiyaçlarını hesaplayın.

### **3.4 Uygulama: Kaynak Kullanımını İzleme ve Gelecekteki Gereksinimleri Tahmin Etme**
1. CPU, RAM ve disk kullanımını ölçen bir betik yazın.
   ```bash
   echo "CPU Kullanımı:" && mpstat
   echo "Bellek Kullanımı:" && free -h
   echo "Disk Kullanımı:" && df -h
   ```
2. Verileri bir dosyada saklayarak uzun dönemli analiz yapın.

---
