### **Orta Düzey Linux Eğitimi**

---

#### **1. Gün: İleri Dosya Sistemi ve Depolama Yönetimi**

1. **Dosya Sistemleri: ext4, XFS (2 saat)**
   - ext4 ve XFS dosya sistemlerinin yapısı, özellikleri ve kullanım alanları.
   - Biçimlendirme, bağlama (mount), ve performans farklılıkları.
   - Uygulama: ext4 ve XFS dosya sistemlerini kurma ve yapılandırma.

2. **Dosya Sistemlerinin Yedeklenmesi ve Kurtarılması (2 saat)**
   - `rsync`, `tar`, `dd` gibi yedekleme araçları.
   - Yedekleme stratejileri ve yedeklerden veri kurtarma işlemleri.
   - Uygulama: Yedekleme işlemi gerçekleştirme ve yedekten geri yükleme.

3. **RAID ve LVM Yapılandırması (2 saat)**
   - RAID seviyeleri (RAID 0, 1, 5, 6) ve LVM (Logical Volume Manager) yapısı.
   - Uygulama: RAID yapılandırması ve LVM oluşturma.

4. **Dosya Sistemi Bütünlüğünü Koruma (1 saat)**s
   - Dosya sistemi kontrol araçları (`fsck`, `smartctl`).
   - Dosya sistemini koruma ve hata tespiti.
   - Uygulama: Dosya sistemi kontrolü ve bakım işlemleri.

5. **Disk/Depolama Yönetimi (1 saat)**
   - Depolama aygıtları, erişim izinleri, depolama bölümlerini yönetme.
   - Uygulama: RAID yapılandırması ve mantıksal hacim (LVM) ayarları.

---

#### **2. Gün: Ağ Yönetimi ve Servisler - 1. Bölüm**

1. **Gelişmiş Ağ Yapılandırması (1 saat)**
   - IP adresleme, ağ maskesi, ağ geçidi, DNS ayarları.
   - Ağ yapılandırma araçları (ifconfig, ip).
   - Uygulama: Ağ ayarlarını yapılandırma ve test etme.

2. **DHCP ve DNS Yapılandırması (2 saat)**
   - DHCP ve DNS sunucu kurulumu ve yapılandırması.
   - `isc-dhcp-server` ve `BIND` DNS kurulumu.
   - Uygulama: DHCP ve DNS yapılandırması.

3. **Apache ve Nginx Web Sunucusu Kurulumu ve Yapılandırması (3 saat)**
   - Apache ve Nginx kurulumu, temel ayarları, yapılandırma dosyaları.
   - Uygulama: Apache ve Nginx üzerinde basit web sayfaları yayımlama.

4. **FTP ve Samba Sunucu Yapılandırması (2 saat)**
   - FTP sunucusu kurulumu (`vsftpd`), kullanıcı erişim ayarları.
   - Samba sunucu yapılandırması ile dosya paylaşımı.
   - Uygulama: FTP ve Samba üzerinde dosya paylaşımı yapılandırması.

---

#### **3. Gün: Ağ Yönetimi ve Servisler - 2. Bölüm**

1. **Ağ Güvenliği: Güvenlik Duvarı ve VPN (3 saat)**
   - Güvenlik duvarı yapılandırması (UFW, iptables).
   - VPN kurulumu ve yapılandırması (OpenVPN).
   - Uygulama: Güvenlik duvarı kuralları oluşturma ve VPN bağlantısı kurma.

2. **HTTP Servisleri (3 saat)**
   - Temel Apache/Nginx yapılandırması, HTTPS ayarları.
   - Squid proxy sunucu kurulumu ve caching proxy olarak yapılandırma.
   - Nginx'i reverse proxy olarak yapılandırma.
   - Uygulama: HTTPS sertifikası ekleme, caching ve reverse proxy yapılandırması.

3. **Dosya Paylaşımı: Samba ve NFS (2 saat)**
   - Samba ve NFS yapılandırması, paylaşım izinleri.
   - Uygulama: Dosya paylaşım protokolleri üzerinde çalışma ve dosya erişim testi.

---

#### **4. Gün: İstemci Ağı Yönetimi ve E-posta Hizmetleri**

1. **İstemci Ağı Yönetimi (4 saat)**
   - DHCP yapılandırması, istemci ayarları.
   - PAM (Pluggable Authentication Modules) kimlik doğrulama mekanizmaları.
   - LDAP istemci yapılandırması ve OpenLDAP sunucu kurulumu.
   - Uygulama: LDAP ve PAM yapılandırması ile merkezi kimlik doğrulama kurulumu.

2. **E-posta Hizmetleri (4 saat)**
   - E-posta sunucuları kurulumu (Postfix, Dovecot).
   - E-posta teslimatını yönetme, SMTP ve IMAP/POP3 yapılandırması.
   - Mailbox erişimini yönetme ve güvenlik ayarları.
   - Uygulama: Postfix ve Dovecot ile e-posta sistemi oluşturma ve test etme.

---

#### **5. Gün: Sistem Yönetimi ve Bakımı - 1. Bölüm**

1. **Otomatikleştirilmiş Görevler: cron (1 saat)**
   - Crontab ile görev zamanlama ve otomasyon.
   - Uygulama: Otomatik sistem yedekleme ve bakım görevleri oluşturma.

2. **Sistem İzleme ve Performans Ölçümleri (2 saat)**
   - Sistem izleme araçları (top, htop, vmstat).
   - Performans ölçümleri ve kaynak kullanımı analizi.
   - Uygulama: Sistem izleme ve performans testi.

3. **Sistem Günlüğü ve Log Yönetimi (2 saat)**
   - Syslog yapılandırması ve log dosyalarının yönetimi.
   - `journalctl`, `logrotate` ile log yönetimi.
   - Uygulama: Sistem loglarını kontrol etme ve belirli olayları izleme.

4. **Yedekleme ve Geri Yükleme Stratejileri (3 saat)**
   - Yedekleme türleri ve stratejileri.
   - `rsync`, `tar`, `dd` ile yedekleme işlemleri.
   - Uygulama: Yedekleme ve geri yükleme stratejileri uygulama.

---

#### **6. Gün: Sistem Yönetimi ve Bakımı - 2. Bölüm**

1. **Paket Yönetimi ve Yazılım Güncellemeleri (2 saat)**
   - Paket yönetimi (`apt`, `yum`, `dnf`), yazılım güncellemeleri.
   - Uygulama: Yazılım güncellemeleri ve paket yönetimi uygulamaları.

2. **E-posta Sistem Hizmetleri (2 saat)**
   - Sistem zamanını koruma, sistem günlüğü ve e-posta hizmetleri.
   - Mail Transfer Agent (MTA) temelleri, sistem uyarıları için e-posta gönderme.
   - Uygulama: MTA yapılandırma ve sistem bildirimleri için e-posta kurulumu.

3. **Kapasite Planlama (4 saat)**
   - Kaynak kullanımını ölçme, kapasite planlama ve gelecekteki ihtiyaçları tahmin etme.
   - CPU, bellek ve disk kullanımını analiz etme.
   - Uygulama: Kaynak kullanımını izleme, sistem büyüme planları ve gelecekteki gereksinimleri tahmin etme.

---

