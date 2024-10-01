# 04 - Basit Ağ Sorun Giderme

Ağ sorunları, günlük sistem yönetimi ve kullanıcı deneyiminde sıkça karşılaşılan problemlerdendir. Basit ağ sorunlarını hızlı bir şekilde teşhis edebilmek ve çözebilmek, sistem yöneticileri için önemli bir beceridir. Bu kılavuzda, temel ağ sorunlarını gidermek için kullanabileceğiniz komutlar ve yöntemler ele alınacaktır.

---

## 1. Ağ Bağlantısını Kontrol Etme

Ağ sorunlarını giderirken öncelikle ağ bağlantısının var olup olmadığını kontrol etmelisiniz. Bunun için aşağıdaki adımları izleyebilirsiniz:

### 1.1 `ping` Komutu

`ping`, belirli bir IP adresine ya da ana makine adına ICMP (Internet Control Message Protocol) paketleri göndererek, hedefe ulaşılıp ulaşılamadığını kontrol eder.

- Bir ana bilgisayara ping atmak:
  ```bash
  ping 8.8.8.8
  ```
  Bu komut, Google DNS sunucusuna ping gönderir. Cevap alıyorsanız, internet bağlantınızın olduğunu gösterir.

- Bir ana makine adına ping atmak:
  ```bash
  ping www.example.com
  ```

**Ping zaman aşıyor veya cevap vermiyorsa**, ağ bağlantısında bir sorun olabilir. Bu durumda, yerel ağ yapılandırmasını ve yönlendirici ayarlarını kontrol etmek gerekir.

### 1.2 `ifconfig` ve `ip` Komutları

Ağ arayüzünüzün doğru şekilde yapılandırıldığından emin olmak için `ifconfig` veya `ip` komutlarını kullanabilirsiniz.

- `ifconfig` komutu:
  ```bash
  ifconfig
  ```
  Bu komut, ağ arayüzlerinin IP adreslerini, ağ maskesini ve diğer bilgilerini gösterir.

- `ip` komutu:
  ```bash
  ip addr show
  ```
  `ip` komutu, modern Linux dağıtımlarında `ifconfig` komutuna alternatif olarak kullanılmaktadır.

Eğer ağ arayüzünüzün IP adresi yoksa, DHCP ayarlarını kontrol etmeli veya statik bir IP adresi tanımlamalısınız.

### 1.3 `netstat` ve `ss` Komutları

Ağ bağlantılarını ve port durumlarını görmek için `netstat` veya `ss` komutlarını kullanabilirsiniz.

- `netstat` komutu:
  ```bash
  netstat -tuln
  ```
  Bu komut, aktif olan bağlantı noktalarını ve açık portları listeler.

- `ss` komutu:
  ```bash
  ss -tuln
  ```
  `ss`, `netstat` komutuna benzer fakat daha hızlıdır ve daha detaylı bilgi sunar.

---

## 2. DNS Sorunlarını Giderme

DNS (Domain Name System) sorunları, bir alan adının IP adresine çözülememesiyle ortaya çıkar. Bu durumda, DNS ayarlarını kontrol etmek ve gerekirse başka bir DNS sunucusu kullanmak gerekebilir.

### 2.1 `nslookup` Komutu

`nslookup` komutu, bir alan adının DNS çözümlemesini yapar.

- Bir alan adını çözümlemek:
  ```bash
  nslookup www.example.com
  ```

Eğer DNS sunucusu cevap vermiyorsa, DNS ayarlarınızı gözden geçirin ve alternatif bir DNS sunucusu kullanmayı deneyin (örneğin Google DNS: 8.8.8.8).

### 2.2 `dig` Komutu

`dig` komutu, daha ayrıntılı DNS sorguları yapar.

- Bir alan adını çözümlemek:
  ```bash
  dig www.example.com
  ```

`dig` komutu ile DNS sunucularından alınan ayrıntılı cevapları görebilirsiniz.

---

## 3. Ağ Yolunu Kontrol Etme

Bağlantı sorunlarının hangi aşamada yaşandığını görmek için ağ yolunu kontrol edebilirsiniz. Bunun için en yaygın kullanılan komutlar `traceroute` ve `tracepath` komutlarıdır.

### 3.1 `traceroute` Komutu

`traceroute`, paketlerin hedefe ulaşana kadar geçtiği yönlendiricileri listeler.

- Bir hedefe traceroute komutuyla yol izleme:
  ```bash
  traceroute www.example.com
  ```

### 3.2 `tracepath` Komutu

`tracepath`, `traceroute` komutuna benzer ancak bazı ek özelliklere sahiptir.

- Bir hedefe tracepath komutuyla yol izleme:
  ```bash
  tracepath www.example.com
  ```

Bu komutlar sayesinde ağ üzerindeki gecikme ve bağlantı kopukluklarının nerede meydana geldiğini tespit edebilirsiniz.

---

## 4. Ağ Ayarlarını Yenileme

Ağ bağlantınızda sorun yaşıyorsanız, ağ ayarlarını yenilemek sorunu çözebilir.

### 4.1 `dhclient` Komutu

Eğer DHCP kullanıyorsanız, IP adresi almak için `dhclient` komutunu kullanabilirsiniz.

- IP adresini yenilemek:
  ```bash
  sudo dhclient
  ```

Bu komut, mevcut DHCP ayarlarını yenileyerek yeni bir IP adresi almanızı sağlar.

---

## 5. Log Dosyalarını İnceleme

Ağ sorunlarının kaynağını bulmak için sistem log dosyalarını inceleyebilirsiniz. Ağ ile ilgili hatalar genellikle `/var/log` dizininde bulunur.

- Sistem loglarını incelemek:
  ```bash
  cat /var/log/syslog | grep "network"
  ```

Ağ bağlantısı ile ilgili daha fazla bilgi almak için `journalctl` komutunu da kullanabilirsiniz:
```bash
journalctl -u NetworkManager
```

---
