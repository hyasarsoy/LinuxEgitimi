# Sistemi Başlatma

Linux sistemlerinde sistemin nasıl başlatıldığı, hangi adımların takip edildiği ve bu süreçte hangi servislerin çalıştırıldığı oldukça önemlidir. Sistemin başlatılması sırasında çekirdek yüklenir, gerekli sürücüler yüklenir ve sistem hizmetleri (servisler) devreye alınır. Bu süreci anlamak, sorun giderme ve yapılandırma açısından faydalıdır.

## 1. Boot Süreci

Linux sisteminin başlatılma süreci, birkaç adımı içerir:

### 1.1. BIOS/UEFI
Sistem açıldığında ilk olarak BIOS (Basic Input/Output System) veya UEFI (Unified Extensible Firmware Interface) devreye girer. Bu adımda donanım bileşenleri tanımlanır ve sistemin başlatılabileceği bir aygıt aranır (genellikle sabit disk).

### 1.2. Bootloader (Önyükleyici)
BIOS/UEFI, önyükleyici yazılımını (genellikle GRUB - GRand Unified Bootloader) sabit diskte bulur ve yükler. Önyükleyici, Linux çekirdeğini başlatmaktan sorumludur.

### 1.3. Linux Çekirdeği (Kernel)
Önyükleyici, Linux çekirdeğini belleğe yükler ve başlatır. Çekirdek, donanım bileşenleriyle iletişimi sağlar ve sistemin geri kalanını yüklemek için temel altyapıyı sunar.

### 1.4. Init Sistemleri
Çekirdek yüklendikten sonra, sistemdeki servisleri ve işlemleri yöneten `init` sistemi devreye girer. Modern Linux sistemlerinde bu görev genellikle **systemd** tarafından yapılır. Daha eski sistemlerde ise **SysVinit** kullanılabilir.

## 2. Runlevel / Boot Hedefleri

Linux sistemlerinde farklı çalışma seviyeleri (runlevel) veya boot hedefleri kullanılır. Bu seviyeler, sistemin ne kadar işlevselliğe sahip olacağını belirler.

### 2.1. Runlevel Nedir?

Runlevel, Linux sisteminin belirli bir çalışma seviyesini ifade eder. Her runlevel, sistemin hangi hizmetlerinin yükleneceğini belirler.

- **Runlevel 0**: Sistemin kapatılması.
- **Runlevel 1**: Tek kullanıcı modu (genellikle bakım modu olarak kullanılır).
- **Runlevel 3**: Çok kullanıcılı mod, ağ servisleriyle birlikte (grafik arayüz olmadan).
- **Runlevel 5**: Çok kullanıcılı mod, ağ servisleri ve grafik arayüz (GUI) ile birlikte.
- **Runlevel 6**: Sistemin yeniden başlatılması (reboot).

### 2.2. Systemd Boot Hedefleri

Modern sistemlerde **systemd** runlevel yerine "target" (hedef) kavramını kullanır. Örnek hedefler şunlardır:

- **poweroff.target**: Sistemin kapatılması.
- **rescue.target**: Tek kullanıcı modu.
- **multi-user.target**: Çok kullanıcılı mod (grafik arayüz olmadan).
- **graphical.target**: Grafik arayüz ile çok kullanıcılı mod.
- **reboot.target**: Sistemin yeniden başlatılması.

### 2.3. Runlevel / Hedef Değiştirme

Çalışan bir sistemde runlevel veya boot hedefi şu komutla değiştirilebilir:

```bash
sudo systemctl isolate <hedef>
```

Örneğin, sistemi çok kullanıcılı moda (grafik arayüz olmadan) geçirmek için:

```bash
sudo systemctl isolate multi-user.target
```

Sistemi kapatmak için:

```bash
sudo systemctl isolate poweroff.target
```

## 3. Sistemi Yeniden Başlatma ve Kapatma

Sistemin kapatılması veya yeniden başlatılması komut satırından yapılabilir. Bu işlemler root yetkileri gerektirir.

### 3.1. Sistemi Kapatma

Sistemi güvenli bir şekilde kapatmak için şu komutu kullanabilirsiniz:

```bash
sudo shutdown -h now
```

Alternatif olarak, systemd kullanarak:

```bash
sudo systemctl poweroff
```

### 3.2. Sistemi Yeniden Başlatma

Sistemi yeniden başlatmak için şu komutu kullanabilirsiniz:

```bash
sudo reboot
```

Alternatif olarak, systemd ile:

```bash
sudo systemctl reboot
```

## 4. Servislerin Yönetimi

Sistem başlatıldığında birçok servis otomatik olarak başlatılır. Bu servisler, sistemin düzgün çalışması için kritik olabilir. Servisleri yönetmek için `systemctl` komutu kullanılır.

### 4.1. Servis Başlatma

Bir servisi başlatmak için:

```bash
sudo systemctl start <servis_adı>
```

### 4.2. Servis Durdurma

Bir servisi durdurmak için:

```bash
sudo systemctl stop <servis_adı>
```

### 4.3. Servis Durumunu Kontrol Etme

Bir servisin çalışıp çalışmadığını kontrol etmek için:

```bash
sudo systemctl status <servis_adı>
```

### 4.4. Servislerin Otomatik Başlatılması

Bir servisin sistem her açıldığında otomatik olarak başlatılmasını sağlamak için:

```bash
sudo systemctl enable <servis_adı>
```

Aynı şekilde, otomatik başlatmayı devre dışı bırakmak için:

```bash
sudo systemctl disable <servis_adı>
```

## 5. Sistemi Başlatma Sorunlarını Giderme

Sistem başlatma sırasında meydana gelen sorunlar çeşitli nedenlerden kaynaklanabilir. Bu tür sorunları gidermek için bazı ipuçları şunlardır:

- **Başlangıç Günlüklerini İnceleme**: `journalctl` komutu ile sistem günlüklerine erişerek hataları inceleyebilirsiniz.
  
  ```bash
  sudo journalctl -b
  ```

- **Kurtarma Moduna Geçiş**: Sistem açılmadığında, önyükleme sırasında GRUB menüsünden "Recovery Mode" (Kurtarma Modu) seçeneği ile sisteme tek kullanıcı modunda giriş yapabilir ve sorunları düzeltebilirsiniz.

