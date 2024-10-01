# 02 - Temel Ağ Kavramları ve Yapılandırması

Linux sistemlerinde ağ yönetimi, sunucuların ve istemcilerin internet ve yerel ağlar üzerinden iletişim kurmasını sağlar. Ağ yapılandırması, IP adresleri, DNS ayarları, ağ arayüzleri ve yönlendirme gibi temel ağ bileşenlerini içerir.

Bu bölümde temel ağ kavramları ve yapılandırma adımlarını ele alacağız.

---

## 1. Ağ Kavramları

### 1.1 IP Adresleri

IP adresleri, bir cihazın ağ üzerindeki kimliğidir. İki tür IP adresi vardır:

- **IPv4**: 32-bit uzunluğunda, dört oktetli adreslerdir. Örnek: `192.168.1.1`
- **IPv6**: 128-bit uzunluğunda daha yeni bir standarttır. Örnek: `2001:0db8:85a3:0000:0000:8a2e:0370:7334`

### 1.2 Ağ Maskesi

Ağ maskesi, bir IP adresinin hangi kısmının ağ adresi olduğunu ve hangi kısmının cihaz adresi olduğunu belirler. Örneğin, `255.255.255.0` ağ maskesi, bir ağın ilk üç oktetinin ağ adresi olduğunu ifade eder.

### 1.3 Gateway (Ağ Geçidi)

Ağ geçidi, bir yerel ağdan diğer ağlara (genellikle internete) çıkışı sağlayan cihazdır. Gateway genellikle yönlendiricidir ve ağdaki cihazların internet erişimi sağlamasına olanak tanır.

### 1.4 DNS (Domain Name System)

DNS, alan adlarını IP adreslerine çeviren sistemdir. Örneğin, `www.google.com` adresini IP adresine dönüştürerek tarayıcının bu siteye ulaşmasını sağlar.

---

## 2. Ağ Yapılandırması

### 2.1 IP Adresi Yapılandırma

Linux sistemlerinde ağ yapılandırması, `/etc/network/interfaces` dosyası (Debian tabanlı sistemler) veya `nmcli`, `nmtui` gibi araçlar aracılığıyla yapılır.

#### Statik IP Adresi Ayarlama (Debian/Ubuntu)

1. Ağ yapılandırma dosyasını düzenleyin:
   ```bash
   sudo nano /etc/network/interfaces
   ```

2. Şu şekilde statik IP ayarı yapın:
   ```bash
   auto eth0
   iface eth0 inet static
   address 192.168.1.100
   netmask 255.255.255.0
   gateway 192.168.1.1
   dns-nameservers 8.8.8.8 8.8.4.4
   ```

3. Değişiklikleri kaydedip çıkın ve ağı yeniden başlatın:
   ```bash
   sudo systemctl restart networking
   ```

#### DHCP ile IP Almak (Debian/Ubuntu)

1. Ağ yapılandırma dosyasını düzenleyin:
   ```bash
   sudo nano /etc/network/interfaces
   ```

2. Şu şekilde DHCP ayarını yapın:
   ```bash
   auto eth0
   iface eth0 inet dhcp
   ```

3. Değişiklikleri kaydedip çıkın ve ağı yeniden başlatın:
   ```bash
   sudo systemctl restart networking
   ```

### 2.2 IP Adresini Görüntüleme

Linux’ta IP adreslerini ve ağ arayüzlerini görüntülemek için `ip` veya `ifconfig` komutları kullanılır.

- **ip komutu**:
  ```bash
  ip addr show
  ```

- **ifconfig komutu** (eski yöntem):
  ```bash
  ifconfig
  ```

### 2.3 Ağ Geçidi ve DNS Ayarları

Ağ geçidi ve DNS ayarları ağ dosyalarında tanımlanabilir ya da dinamik olarak ağ yapılandırma araçlarıyla belirlenir.

#### Ağ Geçidi Ayarları

Varsayılan ağ geçidini görüntülemek için:
```bash
ip route
```

Ağ geçidini elle ayarlamak için:
```bash
sudo ip route add default via <gateway_ip>
```

#### DNS Ayarları

DNS ayarları genellikle `/etc/resolv.conf` dosyasında bulunur. Örnek:
```bash
nameserver 8.8.8.8
nameserver 8.8.4.4
```

### 2.4 SSH ile Uzak Bağlantılar

SSH (Secure Shell), uzak bir makineye güvenli bir şekilde bağlanmak için kullanılan bir protokoldür.

- SSH ile uzak bir sunucuya bağlanmak için:
  ```bash
  ssh kullanıcıadı@sunucu_ip_adresi
  ```

- SSH servisini başlatmak veya durdurmak:
  ```bash
  sudo systemctl start ssh
  sudo systemctl stop ssh
  ```

### 2.5 Temel Ağ Sorun Giderme

#### Ping Komutu

Bağlantıyı test etmek için `ping` komutu kullanılır:
```bash
ping 8.8.8.8
```

#### Traceroute Komutu

Ağdaki paketlerin hangi yollardan geçtiğini görmek için `traceroute` komutu kullanılır:
```bash
traceroute www.google.com
```

#### Netstat Komutu

Ağ bağlantılarını ve portları görmek için `netstat` komutu kullanılır:
```bash
netstat -tuln
```

#### Nslookup/Dig Komutu

DNS sorguları için `nslookup` veya `dig` kullanılabilir:
```bash
nslookup www.google.com
dig www.google.com
```

