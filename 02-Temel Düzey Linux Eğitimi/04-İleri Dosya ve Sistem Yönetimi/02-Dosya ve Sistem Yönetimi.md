# Dosya ve Sistem Yönetimi

Linux sistemlerinde dosya ve disk yönetimi, sistem yöneticileri için temel görevlerden biridir. Bu görevler, dosya sistemlerini yapılandırmayı, bağlantılar oluşturmayı ve sistem loglarını izlemeyi içerir. Bu bölümde, dosya ve sistem yönetimiyle ilgili temel işlemler ele alınacaktır.

## 1. Dosya Sistemlerinin Yönetimi ve Disk Bölümleme

Disk bölümleme ve dosya sistemlerinin yönetimi, sistemdeki disklerin verimli kullanılmasını ve yapılandırılmasını sağlar. Linux'ta yaygın kullanılan dosya sistemleri **ext4**, **XFS**, **btrfs** gibi türlerdir.

### Disk Bölümleme:
- Yeni bir disk bölümü oluşturmak için:
  ```bash
  sudo fdisk /dev/sda
  ```

- Bölümleri görmek için:
  ```bash
  lsblk
  ```

- Disk bölümlerini biçimlendirmek (örneğin, `ext4` dosya sistemi ile):
  ```bash
  sudo mkfs.ext4 /dev/sda1
  ```

### Disk Bölümünü Bağlama:
- Bir dosya sistemini bağlamak için:
  ```bash
  sudo mount /dev/sda1 /mnt
  ```

- Otomatik bağlama için `fstab` dosyasına ekleme:
  ```bash
  /dev/sda1  /mnt  ext4  defaults  0  2
  ```

Bu işlemler, disklerin ve dosya sistemlerinin yönetimini kolaylaştırır ve dosya sistemlerinin sistem tarafından kullanılabilir hale gelmesini sağlar.

---

## 2. Sabit ve Sembolik Bağlantılar Oluşturma ve Yönetme

Linux dosya sisteminde, sabit bağlantılar (hard links) ve sembolik bağlantılar (symbolic links) dosyalar arasında referanslar oluşturur.

### Sabit Bağlantı:
- Bir sabit bağlantı oluşturmak için:
  ```bash
  ln /path/to/original /path/to/link
  ```

### Sembolik Bağlantı:
- Bir sembolik bağlantı oluşturmak için:
  ```bash
  ln -s /path/to/original /path/to/symlink
  ```

Sabit bağlantılar, aynı dosya üzerinde farklı adlar oluşturarak dosya içeriklerine doğrudan erişimi sağlar. Sembolik bağlantılar ise bir dosyaya veya dizine işaret eder ve daha esnek bir yapı sunar.

---

## 3. Sistem Loglarının İzlenmesi ve Yönetimi

Sistem logları, sistemin performansını ve güvenliğini izlemek için kritik bilgiler sunar. Log dosyaları, uygulamalar, kullanıcılar ve sistem süreçleri hakkında ayrıntılı bilgileri içerir.

### Log Dosyalarının İzlenmesi:
- Log dosyalarını görüntülemek için `journalctl` komutu kullanılabilir:
  ```bash
  sudo journalctl
  ```

- Örneğin, son boot'tan itibaren logları görüntülemek için:
  ```bash
  sudo journalctl -b
  ```

### Log Dosyalarının Yönetimi:
- Log dosyalarını sıkıştırmak ve yönetmek için **logrotate** aracı kullanılır. Konfigürasyon dosyası `/etc/logrotate.conf` dizinindedir.
  
  Örneğin, günlük olarak log döndürme ayarı yapmak için:
  ```bash
  /var/log/syslog {
      daily
      missingok
      rotate 7
      compress
      delaycompress
      notifempty
      create 0640 root adm
      sharedscripts
      postrotate
          /etc/init.d/rsyslog rotate > /dev/null
      endscript
  }
  ```

Log dosyalarının etkin bir şekilde yönetilmesi, sistem güvenliği ve performansının izlenmesi için kritik önem taşır.
