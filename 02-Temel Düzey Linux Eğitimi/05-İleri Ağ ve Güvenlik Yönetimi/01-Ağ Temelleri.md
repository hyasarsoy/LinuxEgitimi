# Ağ Temelleri

Linux sistemlerinde ağ yönetimi, hem sistem yöneticileri hem de ağ yöneticileri için kritik bir beceridir. Bu bölümde, temel ağ kavramları, yapılandırmaları ve ağ sorun giderme tekniklerine odaklanacağız.

## 1. İnternet Protokolleri (TCP/IP, UDP)

İnternet üzerindeki veri iletimi **TCP/IP** ve **UDP** protokolleri aracılığıyla gerçekleşir. Her iki protokol de veri iletimini sağlar, ancak çalışma prensipleri farklıdır.

- **TCP (Transmission Control Protocol)**: Bağlantı temelli bir protokoldür. Verilerin güvenli bir şekilde iletilmesini sağlar. Hata kontrolü yapar ve paketlerin sırasını garanti eder.
- **UDP (User Datagram Protocol)**: Bağlantısız bir protokoldür. Veriler hızlı bir şekilde iletilir ancak hata kontrolü ve sıralama garantisi yoktur. Genellikle video akışı ve oyunlar gibi gerçek zamanlı uygulamalarda kullanılır.

### Örnek:
- TCP bağlantısı ile bir siteye bağlanmak için:
  ```bash
  telnet example.com 80
  ```

- UDP bağlantısı test etmek için `nc` (netcat) kullanılabilir:
  ```bash
  nc -u example.com 1234
  ```

---

## 2. Kalıcı Ağ Yapılandırması

Linux'ta ağ ayarları kalıcı hale getirilebilir. Bu sayede, sistem yeniden başlatılsa bile yapılandırmalar korunur.

- **Debian/Ubuntu** sistemlerinde ağ yapılandırmaları `/etc/netplan/` dizininde yapılır. Örneğin:
  ```yaml
  network:
    version: 2
    ethernets:
      eth0:
        dhcp4: true
  ```

- **CentOS/RHEL** tabanlı sistemlerde ise, yapılandırmalar `/etc/sysconfig/network-scripts/ifcfg-eth0` dosyasında yapılır:
  ```bash
  DEVICE=eth0
  BOOTPROTO=dhcp
  ONBOOT=yes
  ```

Bu ayarlar sayesinde ağ yapılandırmaları kalıcı hale getirilir ve sistem yeniden başlatıldığında otomatik olarak yüklenir.

---

## 3. Temel Ağ Sorun Giderme Teknikleri

Ağ sorunları, sistemin işleyişini olumsuz etkileyebilir. Bu tür sorunları gidermek için kullanılabilecek birkaç temel komut vardır:

- **ping**: Ağda bir hedefe ulaşıp ulaşmadığınızı kontrol etmek için kullanılır:
  ```bash
  ping 8.8.8.8
  ```

- **traceroute**: Veri paketinin hangi yolları izlediğini görmek için kullanılır:
  ```bash
  traceroute example.com
  ```

- **netstat**: Aktif ağ bağlantılarını ve portları listelemek için kullanılır:
  ```bash
  netstat -tuln
  ```

- **ip a**: Ağ arayüzlerini ve IP yapılandırmalarını görüntülemek için kullanılır:
  ```bash
  ip a
  ```

---

## 4. DNS Yapılandırma

DNS (Domain Name System), alan adlarını IP adreslerine dönüştürür. DNS yapılandırması doğru yapılmadığında, alan adlarına ulaşımda sorunlar yaşanabilir.

- DNS ayarları `/etc/resolv.conf` dosyasında yapılır. Örnek bir DNS yapılandırması:
  ```bash
  nameserver 8.8.8.8
  nameserver 8.8.4.4
  ```

- DNS sorunlarını gidermek için **dig** ve **nslookup** gibi araçlar kullanılabilir:
  ```bash
  dig example.com
  nslookup example.com
  ```

---

## 5. İleri Ağ Yapılandırması

İleri ağ yapılandırması, daha karmaşık ağ topolojileri ve güvenlik yapılandırmalarını içerir. Örneğin, bir ağ arabirimine birden fazla IP adresi atamak veya statik yönlendirme kuralları eklemek ileri yapılandırmalar arasında yer alır.

- Birden fazla IP adresi atamak:
  ```bash
  ip addr add 192.168.1.10/24 dev eth0
  ```

- Statik bir rota eklemek:
  ```bash
  ip route add 192.168.2.0/24 via 192.168.1.1
  ```

---

## 6. Ağ Sorunlarını Giderme

Ağ sorunlarını gidermek için izlenecek adımlar:

- **Bağlantı kontrolü**: Sistem hedefe ulaşabiliyor mu? `ping` veya `traceroute` ile kontrol edilir.
- **DNS kontrolü**: DNS yapılandırması doğru mu? `dig` ve `nslookup` komutlarıyla test edilir.
- **Yönlendirme kontrolü**: Yönlendirme tabloları doğru mu? `ip route` komutu ile kontrol edilir.
- **Port kontrolü**: Servisler doğru portlarda dinliyor mu? `netstat` veya `ss` komutlarıyla kontrol edilir.

Bu adımlar ağ sorunlarını teşhis etmek ve çözmek için temel bir rehber sağlar.
```