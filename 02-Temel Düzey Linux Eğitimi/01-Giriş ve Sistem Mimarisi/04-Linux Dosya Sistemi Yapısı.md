# Linux Dosya Sistemi Yapısı

## 1. Linux Dosya Sistemi Nedir?

Linux dosya sistemi, dosyaların ve dizinlerin organize edildiği bir yapıdır. Tüm dosyalar, kök dizin (`/`) altında düzenlenir ve bir hiyerarşi halinde alt dizinlere ayrılır. Bu yapı, kullanıcılara ve sistem yöneticilerine dosya ve klasörlerin sistemdeki yerini daha iyi anlamalarını sağlar.

## 2. Dosya Sistemi Hiyerarşisi

Linux’te tüm dosya ve dizinler, kök dizin (`/`) altında yer alır. Dosya sistemi, farklı görevler için kullanılan çeşitli dizinler içerir.

### Temel Dizinler:

1. **/** - Kök dizin. Linux dosya sistemi hiyerarşisinin başladığı yerdir.
2. **/bin** - Temel kullanıcı komutları. Tüm kullanıcılar tarafından erişilebilen temel sistem komutlarını içerir (örn. `ls`, `cp`, `mv`).
3. **/boot** - Sistemin açılışı için gerekli dosyalar. Önyükleyici ve çekirdek dosyaları içerir.
4. **/dev** - Donanım cihazlarına erişim sağlayan özel dosyalar. Cihaz dosyaları burada bulunur (örn. sabit diskler, USB sürücüler).
5. **/etc** - Sistem yapılandırma dosyaları. Tüm sistemdeki servis ve uygulamaların yapılandırmaları bu dizindedir.
6. **/home** - Kullanıcıların kişisel dizinleri. Her kullanıcı için bir dizin oluşturulur (örn. `/home/kullaniciadi`).
7. **/lib** - Sistem kütüphaneleri. Çekirdek ve temel sistem işlevleri için kullanılan kütüphane dosyalarını içerir.
8. **/media** ve **/mnt** - Harici depolama aygıtları için bağlama noktaları. CD, DVD, USB sürücüler bu dizinlerde bağlanır.
9. **/opt** - Opsiyonel yazılımlar ve uygulamalar. Üçüncü parti uygulamalar genellikle burada depolanır.
10. **/proc** - Sanal dosya sistemi. Çekirdek ve sistem süreçlerine ilişkin bilgileri sağlar.
11. **/root** - Root kullanıcısının (süper kullanıcı) ana dizini. Normal kullanıcıların ana dizinlerinden farklıdır.
12. **/sbin** - Yalnızca yönetici (root) tarafından kullanılan sistem yönetim komutları.
13. **/tmp** - Geçici dosyalar. Sistem yeniden başlatıldığında bu dizindeki dosyalar silinir.
14. **/usr** - İkincil hiyerarşi. Kullanıcı programları, kütüphaneler, belgeler ve kaynak kodları içerir. Ayrıca sistemin kullanıcı alanı yazılımları burada bulunur.
15. **/var** - Değişken veriler. Sistem logları, e-posta kuyruğu, önbellek dosyaları gibi sürekli değişen veriler burada saklanır.

### Örnek Dosya Sistemi Yapısı:
```
/
├── bin
├── boot
├── dev
├── etc
├── home
│   └── kullanıcıadi
├── lib
├── media
├── mnt
├── opt
├── proc
├── root
├── sbin
├── tmp
├── usr
└── var
```

## 3. Linux Dosya Türleri

Linux'ta dosyalar sadece "klasik" anlamda dosya değildir. Farklı türde dosyalar vardır:

1. **Normal Dosyalar**: Düz metin dosyaları, ikili dosyalar veya veri dosyaları (örn. `*.txt`, `*.bin`).
2. **Dizinler (Directories)**: Diğer dosyaları içeren klasörlerdir.
3. **Bağlantı Dosyaları (Links)**: Dosya veya dizinlere işaret eden kısayol dosyalarıdır. İki türü vardır:
   - **Sabit Bağlantı (Hard Link)**: Aynı dosyaya birden fazla isim vermek.
   - **Sembolik Bağlantı (Symbolic Link)**: Dosyanın veya dizinin bir referansı.
4. **Cihaz Dosyaları**: Donanım cihazlarına erişim sağlayan dosyalardır (örn. `/dev/sda`).
   - **Karakter Cihazları**: Veri akışı karakter akışı olarak işlenir (örn. klavyeler).
   - **Blok Cihazları**: Veri bloklar halinde işlenir (örn. sabit diskler).
5. **FIFO Dosyaları**: Bir işlemden diğerine veri akışını sağlayan boru hatları (aynı anda tek yönlü veri iletimi).
6. **Soket Dosyaları**: Ağ üzerinden veya yerel makineler arasında iki yönlü iletişimi sağlayan dosyalardır.

## 4. Bağlama (Mounting) ve Bağlantıyı Kesme (Unmounting)

Linux dosya sisteminde depolama aygıtları bağlama işlemiyle sisteme entegre edilir. Bu süreç, cihazın bir dizin altında görünmesini sağlar.

### Cihazı Bağlama:

- **mount** komutu ile:
  ```bash
  sudo mount /dev/sda1 /mnt
  ```
  Bu komut, `/dev/sda1` aygıtını `/mnt` dizinine bağlar.

### Cihazın Bağlantısını Kesme:

- **umount** komutu ile:
  ```bash
  sudo umount /mnt
  ```
  Bu komut, `/mnt` dizinindeki bağlı aygıtın bağlantısını keser.

## 5. Dosya Sistemi Türleri

Linux, birçok dosya sistemi türünü destekler. Yaygın dosya sistemleri şunlardır:

1. **ext4**: En yaygın kullanılan Linux dosya sistemidir.
2. **XFS**: Büyük veri ve yüksek performans gerektiren sistemlerde kullanılır.
3. **Btrfs**: Modern ve özellik zengini bir dosya sistemidir, özellikle yedekleme ve hata toleransı için idealdir.
4. **NTFS**: Windows işletim sistemi dosya sistemi. Linux'ta da desteklenir.
5. **FAT32/exFAT**: Taşınabilir depolama aygıtlarında yaygın olarak kullanılır.


