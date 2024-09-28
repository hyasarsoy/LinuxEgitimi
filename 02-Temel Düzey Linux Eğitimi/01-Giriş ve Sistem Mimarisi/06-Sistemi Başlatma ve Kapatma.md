
# Sistemi Başlatma ve Kapatma

Linux işletim sisteminde, sistemi başlatma ve kapatma işlemleri oldukça kritik yönetimsel görevlerdir. Bu işlemler, sistem kararlılığını korumak ve sistemin sağlıklı bir şekilde çalışmasını sağlamak için dikkatli bir şekilde yapılmalıdır.

## 1. Sistemi Başlatma Süreci

Linux sistemleri, açılış sırasında birkaç aşamadan geçer. Bu süreçte, sistemin donanımı tanınır ve gerekli hizmetler başlatılır.

### 1.1. BIOS / UEFI
Sistem açıldığında, ilk olarak BIOS veya UEFI yüklenir ve donanım bileşenleri kontrol edilir. Ardından, işletim sistemi yükleme işlemi başlar.

### 1.2. Bootloader
BIOS/UEFI sonrası devreye giren **bootloader** (genellikle GRUB kullanılır), işletim sisteminin çekirdeğini (kernel) yüklemekten sorumludur. Çekirdek yüklendikten sonra, sistem başlatma süreci devam eder.

### 1.3. Kernel (Çekirdek)
Çekirdek, donanımla yazılım arasındaki köprü görevi görür. Çekirdek, sistemin donanımını tanır ve temel hizmetleri başlatır.

### 1.4. Init Sistemi
Linux çekirdeği yüklendikten sonra, init sistemi (systemd veya upstart gibi) devreye girer ve sistemde çalışacak olan servisleri başlatır. Systemd, modern Linux dağıtımlarında en yaygın kullanılan init sistemidir.

## 2. Sistemi Başlatma ile İlgili Komutlar

Linux'te sistemi başlatma ve yeniden başlatma işlemleri çeşitli komutlarla gerçekleştirilebilir.

### 2.1. `systemctl` ile Sistemi Başlatma ve Yeniden Başlatma

- **Sistemi Yeniden Başlatma**:
  
  ```bash
  sudo systemctl reboot
  ```

  Bu komut, sistemi güvenli bir şekilde yeniden başlatır.

- **Sistemi Kapatma**:
  
  ```bash
  sudo systemctl poweroff
  ```

  Sistemi kapatır ve tüm işlemleri sonlandırır.

### 2.2. `shutdown` Komutu

`shutdown` komutu, sistemin ne zaman kapanacağını planlamak için kullanılır.

- **Hemen Kapatma**:

  ```bash
  sudo shutdown now
  ```

  Sistemi hemen kapatır.

- **Belirli Bir Süre Sonra Kapatma**:

  ```bash
  sudo shutdown +10
  ```

  Sistemi 10 dakika sonra kapatır.

- **Yeniden Başlatma ile Kapatma**:

  ```bash
  sudo shutdown -r now
  ```

  Sistemi kapatıp yeniden başlatır.

### 2.3. `reboot` Komutu

`reboot` komutu, sistemi yeniden başlatmak için kullanılır.

```bash
sudo reboot
```

Bu komut, açık olan tüm işlemleri sonlandırır ve sistemi yeniden başlatır.

## 3. Runlevel / Hedefler (Boot Targets)

Linux sistemlerinde **runlevel** olarak bilinen sistem çalışma seviyeleri mevcuttur. Bu runlevel'lar, sistemin hangi modda çalışacağını belirler. Modern Linux dağıtımlarında systemd kullanıldığı için, bu runlevel'lar **target** (hedef) adı altında tanımlanır.

### 3.1. Yaygın Runlevel'lar ve Hedefler

- **Runlevel 0 (poweroff.target)**: Sistemi kapatır.
- **Runlevel 1 (rescue.target)**: Tek kullanıcı moduna geçer, sistem bakım modudur.
- **Runlevel 3 (multi-user.target)**: Grafiksel arayüz olmadan çoklu kullanıcı modu.
- **Runlevel 5 (graphical.target)**: Grafiksel kullanıcı arayüzü ile çoklu kullanıcı modu.
- **Runlevel 6 (reboot.target)**: Sistemi yeniden başlatır.

### 3.2. Mevcut Hedefi Görüntüleme

Şu anda kullanılan hedefi görüntülemek için aşağıdaki komutu kullanabilirsiniz:

```bash
systemctl get-default
```

### 3.3. Hedef Değiştirme

Sistemi farklı bir hedefte başlatmak için aşağıdaki komutlar kullanılabilir:

- **Tek Kullanıcı Moduna Geçme** (rescue mod):

  ```bash
  sudo systemctl isolate rescue.target
  ```

- **Grafiksel Modda Başlatma**:

  ```bash
  sudo systemctl isolate graphical.target
  ```

- **Sistemi Çoklu Kullanıcı Modunda Başlatma** (Grafik Arayüz Olmadan):

  ```bash
  sudo systemctl isolate multi-user.target
  ```

## 4. Sistemi Kapatma ve Yeniden Başlatma

### 4.1. Kapatma Süreci

Sistemi kapatmadan önce, tüm işlemlerin ve hizmetlerin düzgün bir şekilde sonlandırılması gerekir. Bu, veri kaybını önlemek ve sistemdeki açık dosyaların zarar görmesini engellemek için önemlidir.

- Sistemi kapatırken, tüm kullanıcı işlemleri sonlandırılır.
- Diskler ve diğer cihazlar güvenli bir şekilde kapatılır.
- Çekirdek, kapanma sinyalini gönderir ve sistem kapanır.

### 4.2. Yeniden Başlatma Süreci

Yeniden başlatma işlemi, sistemi kapatma sürecine benzerdir, ancak sistem kapandıktan sonra tekrar başlatılır. Bu süreçte:

- Sistemde çalışan tüm işlemler sonlandırılır.
- Diskler ve diğer cihazlar güvenli şekilde kapatılır.
- Çekirdek kapanış sinyali gönderir ve sistem yeniden başlar.

