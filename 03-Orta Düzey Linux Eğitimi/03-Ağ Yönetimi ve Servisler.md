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

## Özet

Bu bölümde, ağ yönetimi ve çeşitli sunucu yapılandırmaları ele alınmaktadır. DHCP, DNS, web sunucuları (Apache/Nginx), FTP, Samba, güvenlik duvarı, VPN, ve dosya paylaşım protokolleri hakkında temel ve ileri seviye bilgiler sunulmuştur. Ağ güvenliği ve istemci ağı yönetimi konularında ise güvenlik önlemleri ve kimlik doğrulama yöntemleri ele alınmıştır.

## Ek Kaynaklar
- [DHCP ve DNS Yapılandırmaları](https://wiki.debian.org/DHCP_Server)
- [Apache ve Nginx Belgeleri](https://httpd.apache.org/docs/)
- [Samba Belgeleri](https://www.samba.org/samba/docs/)
- [UFW Güvenlik Duvarı](https://help.ubuntu.com/community/UFW)
