# 3. Gün: Ağ Yönetimi ve Servisler

Bu bölüm, ağ yönetimi, gelişmiş servisler ve sunucu yapılandırmaları ile ilgili konuları kapsamaktadır. Bu konularla, Linux sistemlerde DHCP, DNS, Apache, Nginx, FTP, Samba ve ağ güvenliği gibi temel ve ileri seviye ağ servislerinin kurulumu ve yapılandırması ele alınacaktır.

---

## İçindekiler
1. [Gelişmiş Ağ Yapılandırması](#gelişmiş-ağ-yapılandırması)
2. [DHCP ve DNS Yapılandırması](#dhcp-ve-dns-yapılandırması)
3. [Apache ve Nginx Web Sunucusu Kurulumu ve Yapılandırması](#apache-ve-nginx-web-sunucusu-kurulumu-ve-yapılandırması)
4. [FTP ve Samba Sunucu Yapılandırması](#ftp-ve-samba-sunucu-yapılandırması)
5. [Ağ Güvenliği: Güvenlik Duvarı ve VPN](#ağ-güvenliği-güvenlik-duvarı-ve-vpn)
6. [HTTP Servisleri](#http-servisleri)
7. [Dosya Paylaşımı](#dosya-paylaşımı)
8. [İstemci Ağı Yönetimi](#istemci-ağı-yönetimi)
9. [E-posta Hizmetleri](#e-posta-hizmetleri)

---

### 1. Gelişmiş Ağ Yapılandırması

- **Ağ yapılandırması**: IP adresleme, ağ maskesi, ağ geçidi ve DNS ayarları gibi temel ve gelişmiş ağ yapılandırmalarını içerir.
- **Komutlar**:
  ```bash
  # Ağ ayarlarını görmek için
  ifconfig
  
  # IP adresi yapılandırma (geçici olarak)
  sudo ip addr add 192.168.1.100/24 dev eth0
  
  # Ağ geçidi ekleme
  sudo route add default gw 192.168.1.1
  ```

### 2. DHCP ve DNS Yapılandırması

- **DHCP (Dynamic Host Configuration Protocol)**: Ağdaki cihazlara otomatik olarak IP adresi dağıtmak için kullanılır.
- **DNS (Domain Name System)**: Alan adlarını IP adreslerine çevirmek için kullanılan sistemdir.
  
  - **DHCP Sunucu Yapılandırması**:
    ```bash
    # DHCP Sunucusu Kurulumu
    sudo apt install isc-dhcp-server
    
    # DHCP yapılandırma dosyasını düzenleme
    sudo nano /etc/dhcp/dhcpd.conf
    ```

  - **DNS Yapılandırması**:
    ```bash
    # BIND9 DNS Sunucu kurulumu
    sudo apt install bind9
    
    # Ana DNS yapılandırması
    sudo nano /etc/bind/named.conf.options
    ```

### 3. Apache ve Nginx Web Sunucusu Kurulumu ve Yapılandırması

- **Apache**: Yaygın olarak kullanılan bir web sunucusu.
  ```bash
  # Apache kurulumu
  sudo apt install apache2
  
  # Apache varsayılan yapılandırma dosyası
  sudo nano /etc/apache2/apache2.conf
  ```

- **Nginx**: Apache’den daha hafif bir web sunucusu ve aynı zamanda bir reverse proxy olarak kullanılabilir.
  ```bash
  # Nginx kurulumu
  sudo apt install nginx
  
  # Nginx yapılandırma dosyası
  sudo nano /etc/nginx/nginx.conf
  ```

### 4. FTP ve Samba Sunucu Yapılandırması

- **FTP (File Transfer Protocol)**: Dosya transferi için kullanılan bir protokol.
  ```bash
  # vsftpd FTP sunucusu kurulumu
  sudo apt install vsftpd
  
  # FTP yapılandırma dosyası
  sudo nano /etc/vsftpd.conf
  ```

- **Samba**: Linux ve Windows sistemler arasında dosya paylaşımı için kullanılır.
  ```bash
  # Samba kurulumu
  sudo apt install samba
  
  # Samba yapılandırma dosyası
  sudo nano /etc/samba/smb.conf
  ```

### 5. Ağ Güvenliği: Güvenlik Duvarı ve VPN

- **Güvenlik Duvarı (Firewall)**: UFW (Uncomplicated Firewall) kullanarak basit güvenlik duvarı kuralları oluşturulabilir.
  ```bash
  # UFW kurulumu ve etkinleştirilmesi
  sudo apt install ufw
  sudo ufw enable
  
  # HTTP, HTTPS ve SSH için izin verme
  sudo ufw allow http
  sudo ufw allow https
  sudo ufw allow ssh
  ```

- **VPN (Virtual Private Network)**: Özel bir ağ üzerinden güvenli bağlantı sağlar. OpenVPN yaygın olarak kullanılır.
  ```bash
  # OpenVPN kurulumu
  sudo apt install openvpn
  ```

### 6. HTTP Servisleri

- **Temel Apache/Nginx Yapılandırması**: Web sunucularında sanal ana bilgisayarlar, bağlantı noktaları ve kök dizinleri yapılandırma.
- **HTTPS Yapılandırması**: SSL sertifikaları ile HTTPS kurulumları.
  ```bash
  # Let's Encrypt ile SSL kurulumu (Certbot)
  sudo apt install certbot python3-certbot-apache
  sudo certbot --apache
  ```

- **Squid ile Proxy Kurulumu**: Squid caching proxy kurulumu.
  ```bash
  sudo apt install squid
  sudo nano /etc/squid/squid.conf
  ```

### 7. Dosya Paylaşımı

- **Samba Sunucu Yapılandırması**: Windows ve Linux arasında dosya paylaşımı.
- **NFS (Network File System)**: Linux sistemler arasında dosya paylaşımı.
  ```bash
  # NFS Sunucusu kurulumu
  sudo apt install nfs-kernel-server
  
  # NFS yapılandırma
  sudo nano /etc/exports
  ```

### 8. İstemci Ağı Yönetimi

- **DHCP Yapılandırması**: Ağ istemcileri için DHCP istemcisi olarak yapılandırma.
- **PAM Kimlik Doğrulama**: Pluggable Authentication Module ile kimlik doğrulama yönetimi.
- **LDAP İstemci Kullanımı**: Merkezi kimlik doğrulama için LDAP istemci yapılandırması.
- **OpenLDAP Sunucusu**: Linux için LDAP sunucusu kurulumu ve yapılandırması.
  ```bash
  # OpenLDAP sunucu kurulumu
  sudo apt install slapd ldap-utils
  ```

### 9. E-posta Hizmetleri

- **E-posta Sunucuları**: Postfix gibi e-posta sunucuları kurulumu ve yönetimi.
- **E-posta Teslimatını Yönetme**: SMTP ve IMAP/POP3 ile e-posta dağıtımının yönetimi.
- **Mailbox Erişimi**: Mailbox ayarlarını ve izinlerini yönetme.

  ```bash
  # Postfix E-posta sunucusu kurulumu
  sudo apt install postfix
  ```

---

# **Birden Çok Ağ Adaptörü Eklemek ve Belirli IP Blokları için Route Yazmak**

Bu bölümde, bir Linux sunucusunda birden çok ağ adaptörü (örneğin, `eth0`, `eth1`, `eth2`) yapılandırmayı ve belirli IP adresleri veya IP blokları için özel yönlendirme kurallarını (static routes) yapılandırmayı öğreneceğiz.

---

## **1. Ağ Adaptörlerini Yapılandırma**
Linux'ta, ağ adaptörlerini manuel olarak yapılandırabilir veya ağ yapılandırma araçları (NetworkManager, `netplan`, `ifconfig`, vs.) kullanabilirsiniz.

### **Örnek Senaryo:**
- **eth0:** Varsayılan ağ trafiği.
- **eth1:** IP adresi `192.168.1.10`, yalnızca `10.10.0.34` IP'sine trafik göndermek için.
- **eth2:** IP adresi `192.168.2.10`, yalnızca `10.50.40.0/24` ağına trafik göndermek için.

### **Adımlar:**

#### **1.1 Ağ Adaptörlerini Eklemek**
1. Ağ adaptörlerini tanımlamak için `/etc/network/interfaces` dosyasını düzenleyin:
   ```bash
   sudo nano /etc/network/interfaces
   ```

2. Aşağıdaki yapılandırmayı ekleyin:
   ```plaintext
   # eth0 - Varsayılan ağ
   auto eth0
   iface eth0 inet dhcp

   # eth1 - Özel yönlendirme için
   auto eth1
   iface eth1 inet static
       address 192.168.1.10
       netmask 255.255.255.0
       gateway 192.168.1.1

   # eth2 - Özel yönlendirme için
   auto eth2
   iface eth2 inet static
       address 192.168.2.10
       netmask 255.255.255.0
       gateway 192.168.2.1
   ```

3. Değişiklikleri uygulamak için ağ servislerini yeniden başlatın:
   ```bash
   sudo systemctl restart networking
   ```

#### **1.2 Ağ Adaptörlerinin Durumunu Kontrol Etmek**
Ağ adaptörlerini kontrol etmek için:
```bash
ip addr
```
Çıktıda `eth0`, `eth1`, ve `eth2` adaptörlerini ve IP adreslerini görebilirsiniz.

---

## **2. Belirli IP Blokları için Route Yazmak**

### **2.1 Statik Route Ekleme**
Belirli IP adresleri veya ağlar için rotaları `ip route` komutuyla ekleyebilirsiniz.

#### **2.1.1 Örnek 1: 10.10.0.34 IP'si için eth1 üzerinden yönlendirme**
```bash
sudo ip route add 10.10.0.34 via 192.168.1.1 dev eth1
```

#### **2.1.2 Örnek 2: 10.50.40.0/24 ağı için eth2 üzerinden yönlendirme**
```bash
sudo ip route add 10.50.40.0/24 via 192.168.2.1 dev eth2
```

### **2.2 Route Kalıcılığını Sağlamak**
Yukarıdaki komutlar sistemi yeniden başlattığınızda kaybolur. Statik rotaları kalıcı hale getirmek için, aşağıdaki yöntemleri kullanabilirsiniz.

#### **2.2.1 `/etc/network/interfaces` Dosyasında Route Tanımlama**
`/etc/network/interfaces` dosyasına rotaları ekleyin:
```plaintext
# eth1 rotası
up ip route add 10.10.0.34 via 192.168.1.1 dev eth1

# eth2 rotası
up ip route add 10.50.40.0/24 via 192.168.2.1 dev eth2
```

#### **2.2.2 Kalıcı Route Dosyaları**
Bazı Linux dağıtımlarında `/etc/network/interfaces` yerine, `/etc/sysconfig/network-scripts/` veya `/etc/netplan/` gibi yollar kullanılabilir.

**Örnek:** Netplan kullanan Ubuntu dağıtımı için:
1. `/etc/netplan/01-netcfg.yaml` dosyasını düzenleyin:
   ```yaml
   network:
       version: 2
       renderer: networkd
       ethernets:
           eth1:
               addresses:
                   - 192.168.1.10/24
               routes:
                   - to: 10.10.0.34
                     via: 192.168.1.1

           eth2:
               addresses:
                   - 192.168.2.10/24
               routes:
                   - to: 10.50.40.0/24
                     via: 192.168.2.1
   ```

2. Değişiklikleri uygulayın:
   ```bash
   sudo netplan apply
   ```

---

## **3. Rotaları ve Trafiği Doğrulama**

### **3.1 Rotaları Kontrol Etmek**
Ağ yönlendirme tablosunu görmek için:
```bash
ip route show
```

### **3.2 Trafik Doğrulama**
Belirli bir IP'ye trafik gönderilip gönderilmediğini doğrulamak için `ping` komutunu kullanabilirsiniz:
```bash
ping 10.10.0.34
ping 10.50.40.1
```

### **3.3 tcpdump ile Trafik İzleme**
Hangi adaptör üzerinden trafik gittiğini görmek için `tcpdump` kullanabilirsiniz:
```bash
sudo tcpdump -i eth1 host 10.10.0.34
sudo tcpdump -i eth2 net 10.50.40.0/24
```

---

## Özet

Bu bölümde, ağ yönetimi ve çeşitli sunucu yapılandırmaları ele alınmaktadır. DHCP, DNS, web sunucuları (Apache/Nginx), FTP, Samba, güvenlik duvarı, VPN, ve dosya paylaşım protokolleri hakkında temel ve ileri seviye bilgiler sunulmuştur. Ağ güvenliği ve istemci ağı yönetimi konularında ise güvenlik önlemleri ve kimlik doğrulama yöntemleri ele alınmıştır.

## Ek Kaynaklar
- [DHCP ve DNS Yapılandırmaları](https://wiki.debian.org/DHCP_Server)
- [Apache ve Nginx Belgeleri](https://httpd.apache.org/docs/)
- [Samba Belgeleri](https://www.samba.org/samba/docs/)
- [UFW Güvenlik Duvarı](https://help.ubuntu.com/community/UFW)
