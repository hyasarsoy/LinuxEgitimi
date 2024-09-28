# Donanım Ayarlarını Belirleme ve Yapılandırma

Linux sistemlerinde, donanım ayarlarını belirleme ve yapılandırma, sistemin performansını optimize etmek ve donanım bileşenlerinin doğru bir şekilde çalışmasını sağlamak için kritik bir adımdır. Donanım ayarları, işlemci, bellek, disk sürücüleri, ağ kartları gibi bileşenlerin yapılandırılmasını içerir.

## 1. Donanım Tanımlama ve İzleme

Linux, birçok araçla donanım bileşenlerini tanımlama ve izleme imkanı sunar. Bu araçlar sayesinde sistemdeki donanım bileşenleri hakkında bilgi alabilir ve gerektiğinde yapılandırma yapabilirsiniz.

### 1.1. `lshw` (List Hardware)

`lshw` komutu, sistemdeki donanım bileşenleri hakkında detaylı bilgi sağlar. Sisteminizdeki CPU, bellek, diskler ve ağ aygıtları gibi donanım bileşenlerinin özelliklerini görüntülemek için kullanılır.

```bash
sudo lshw
```

Komutun daha özet bir versiyonunu görmek için:

```bash
sudo lshw -short
```

### 1.2. `lscpu` (CPU Bilgileri)

`lscpu` komutu, işlemcinizin özelliklerini görüntülemek için kullanılır. Bu komut sayesinde CPU mimarisi, çekirdek sayısı, hız gibi bilgilere ulaşabilirsiniz.

```bash
lscpu
```

### 1.3. `lsblk` (Disk Bilgileri)

`lsblk` komutu, sistemdeki blok aygıtlarını (diskler, bölümler) görüntüler. Hangi disklerin bağlı olduğunu ve yapılandırılma durumlarını gösterir.

```bash
lsblk
```

### 1.4. `free` (Bellek Kullanımı)

`free` komutu, sistemdeki bellek kullanımını gösterir. RAM ve swap alanı hakkında bilgi sağlar.

```bash
free -h
```

### 1.5. `lspci` (PCI Aygıtları)

`lspci` komutu, PCI bus'a bağlı donanım aygıtlarını listeler. Ekran kartı, ses kartı ve diğer PCI aygıtlarının yapılandırmalarını görüntülemek için kullanılır.

```bash
lspci
```

### 1.6. `lsusb` (USB Aygıtları)

`lsusb` komutu, sisteminize bağlı olan USB cihazlarını listeler. USB aygıtlarının üreticisi ve modeli gibi bilgileri görüntülemek için kullanılır.

```bash
lsusb
```

## 2. Donanım Bileşenlerini Yapılandırma

Linux üzerinde donanım yapılandırması genellikle terminal üzerinden yapılır ve yapılandırma dosyaları kullanılarak donanım ayarları yönetilir.

### 2.1. CPU Yapılandırması

CPU'nun çalışma hızını ve performansını ayarlamak için CPU frekansı kontrol araçları kullanılabilir. Modern Linux dağıtımlarında `cpufreq` araçları bu işlevi sağlar.

- **CPU Frekansını Görüntüleme**:

  ```bash
  cpufreq-info
  ```

- **CPU Performansını Ayarlama**:

  CPU'yu performans moduna geçirmek için:

  ```bash
  sudo cpufreq-set -g performance
  ```

### 2.2. Disk ve Dosya Sistemi Yapılandırması

Disklerin doğru şekilde yapılandırılması ve dosya sistemlerinin optimize edilmesi, sistem performansını önemli ölçüde artırabilir.

- **Disklerin Bağlanması**:

  Yeni bir diski sisteme bağlamak için `mount` komutu kullanılır.

  ```bash
  sudo mount /dev/sdX /mnt/disk
  ```

- **Dosya Sistemini Kontrol Etme**:

  Dosya sistemi bütünlüğünü kontrol etmek için `fsck` komutu kullanılabilir.

  ```bash
  sudo fsck /dev/sdX
  ```

### 2.3. Ağ Kartı Yapılandırması

Ağ kartlarının yapılandırılması, sistemin internete veya yerel ağlara doğru bir şekilde bağlanmasını sağlar.

- **Ağ Arayüzlerini Görüntüleme**:

  `ip` komutu ile sistemdeki ağ arayüzlerini görüntüleyebilirsiniz.

  ```bash
  ip link show
  ```

- **Ağ Yapılandırmasını Değiştirme**:

  Ağ kartının IP adresini ayarlamak için:

  ```bash
  sudo ip addr add 192.168.1.100/24 dev eth0
  ```

### 2.4. Bellek Yapılandırması

Sistem belleğinin yönetimi, özellikle sunucu sistemlerinde kritik öneme sahiptir. Belleğin etkin kullanımı için swap alanı yapılandırması yapılabilir.

- **Swap Alanını Görüntüleme**:

  Swap alanını görmek için:

  ```bash
  swapon --show
  ```

- **Swap Alanı Eklemek**:

  Yeni bir swap dosyası oluşturup etkinleştirmek için:

  ```bash
  sudo fallocate -l 1G /swapfile
  sudo chmod 600 /swapfile
  sudo mkswap /swapfile
  sudo swapon /swapfile
  ```

## 3. Donanım Yapılandırma Dosyaları

Linux sistemlerinde donanım bileşenlerinin yapılandırması, genellikle `/etc` dizinindeki yapılandırma dosyaları aracılığıyla yapılır. Donanım ayarları için kullanılan bazı önemli dosyalar şunlardır:

- **/etc/fstab**: Disklerin ve dosya sistemlerinin otomatik olarak bağlanması için kullanılır.
- **/etc/network/interfaces**: Ağ yapılandırma dosyasıdır (debian tabanlı sistemlerde).
- **/etc/sysctl.conf**: Çekirdek parametrelerinin yapılandırılması için kullanılır.

## 4. Donanım Performansını İzleme

Linux'te donanım performansını izlemek için birçok araç mevcuttur. Bu araçlar sayesinde CPU, bellek, disk ve ağ kartı performansını sürekli izleyebilirsiniz.

### 4.1. `top` ve `htop`

`top` ve `htop` komutları, sistemde çalışan işlemleri ve kaynak kullanımını gerçek zamanlı olarak izler.

- **top**: Temel sistem performansı bilgilerini gösterir.
  ```bash
  top
  ```

- **htop**: `top` komutunun daha gelişmiş bir sürümüdür ve görsel olarak daha zengin bilgiler sunar.
  ```bash
  htop
  ```

### 4.2. `iostat` (Disk Performansı)

Disk performansını izlemek için `iostat` aracı kullanılır. Disk giriş/çıkış işlemlerini ve işlemci yükünü gösterir.

```bash
iostat
```

### 4.3. `vmstat` (Sistem Performansı)

`vmstat`, sistemdeki bellek, işlemci ve disk kullanımını izlemek için kullanılan bir araçtır.

```bash
vmstat
```

## 5. Donanım Yapılandırma Tavsiyeleri

- **Güncel Sürücüler Kullanın**: Donanımın en iyi performansını elde etmek için güncel sürücülerin kurulu olduğundan emin olun.
- **İzleme Araçlarını Kullanın**: Donanım performansını izlemek için yukarıda belirtilen araçları düzenli olarak kullanın.
- **Özelleştirilmiş Yapılandırmalar**: Özellikle sunucu sistemlerinde, sistem gereksinimlerine göre özelleştirilmiş donanım yapılandırmaları yapın.

