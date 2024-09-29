
Linux işletim sisteminde dosya yapısı ve hiyerarşi, benzersiz bir yapıya sahiptir. Bu bölümde, Linux'ta dosya sisteminin nasıl organize edildiğini, dosya hiyerarşisinin nasıl çalıştığını ve dosya sistemleri ile ilgili önemli yönetim komutlarını öğreneceğiz.

## Linux Dosya Sistemi Yapısı

Linux dosya sistemi, kök dizin (`/`) ile başlar ve tüm dosyalar ve dizinler bu kök dizine bağlıdır. Diğer işletim sistemlerinden farklı olarak, Linux'ta harflerle temsil edilen sürücüler bulunmaz (örneğin, Windows'taki C:, D: gibi). Bunun yerine, her şey kök dizininden dallanarak devam eder.

### Ana Diziler ve Fonksiyonları

- **/** : Kök dizini. Tüm dosya sisteminin en üst seviyesidir.
- **/bin** : Temel kullanıcı komutları. Sistemin çalışması için gerekli olan temel ikili dosyalar burada bulunur.
- **/boot** : Linux çekirdeği ve sistemin açılması için gerekli dosyalar burada yer alır.
- **/dev** : Donanım cihaz dosyaları burada bulunur. Tüm donanım bileşenleri bir dosya olarak temsil edilir.
- **/etc** : Konfigürasyon dosyaları. Sistemle ilgili tüm yapılandırma dosyaları bu dizindedir.
- **/home** : Kullanıcıların kişisel dizinleri. Her kullanıcının kendine ait bir dizini vardır.
- **/lib** : Sistem ve uygulamalar için gerekli paylaşılan kütüphaneler.
- **/media** : Taşınabilir medya cihazlarının bağlandığı yer. USB bellekler veya CD-ROM'lar burada otomatik olarak bağlanır.
- **/mnt** : Geçici olarak bağlanan dosya sistemleri için kullanılan dizin.
- **/opt** : Opsiyonel yazılımlar için kullanılan dizin.
- **/proc** : Çalışan işlemler ve sistem bilgileri hakkında sanal dosyalar içerir.
- **/root** : Root kullanıcısının ana dizini.
- **/sbin** : Sistem yönetimi için gerekli olan temel komut dosyaları.
- **/srv** : Sunucular tarafından sunulan hizmetlerle ilgili veriler.
- **/tmp** : Geçici dosyalar için kullanılan dizin.
- **/usr** : Kullanıcı uygulamaları ve dosyaları için ayrılmış alan.
- **/var** : Değişken dosyalar. Log dosyaları ve e-posta kuyruğu gibi veriler burada saklanır.

## Dosya Sisteminin Hiyerarşisi

Linux dosya sistemi hiyerarşisi, sistemdeki tüm dosyaların ve dizinlerin organize edildiği bir yapıdır. Bu hiyerarşi, sistemin nasıl yapılandırıldığını anlamak ve dosya sisteminde etkin bir şekilde gezinmek için önemlidir. Kök dizin en üst düzeyde yer alır ve diğer tüm dizinler bu dizine bağlıdır.

### Örnek Dosya Yolu

Aşağıdaki dosya yolunu inceleyelim:

```bash
/home/kullanici/dokumanlar/rapor.txt
```

Bu dosya yolunu aşağıdaki gibi parçalayabiliriz:

- `/` : Kök dizini
- `/home/` : Kullanıcı dizinlerini içeren dizin
- `/home/kullanici/` : "kullanici" adlı bir kullanıcının kişisel dizini
- `/home/kullanici/dokumanlar/` : Kullanıcının "dokumanlar" adlı alt dizini
- `/home/kullanici/dokumanlar/rapor.txt` : "rapor.txt" adlı dosya

### Dosya Sistemi Özellikleri

- **Hiyerarşik Yapı**: Dosyalar ve dizinler, mantıksal bir hiyerarşi içinde düzenlenir. Bu, dosyaların kolayca bulunabilmesini sağlar.
- **Her Şey Bir Dosyadır**: Linux'ta, donanım bileşenleri de dahil olmak üzere her şey bir dosya olarak temsil edilir.
- **Mutlak ve Göreli Yollar**: 
  - **Mutlak Yol**: Kök dizininden başlayan dosya yoludur. Örneğin, `/home/kullanici/dokumanlar/rapor.txt`.
  - **Göreli Yol**: Bulunduğunuz dizine göre verilen dosya yoludur. Örneğin, şu anda `/home/kullanici/` dizinindeyseniz, `dokumanlar/rapor.txt` göreli bir yol olur.

## Dosya Sistemleri

Linux, farklı dosya sistemlerini destekler ve her dosya sistemi, depolama aygıtlarını yönetmenin farklı yollarını sunar. Yaygın olarak kullanılan dosya sistemleri şunlardır:

- **ext4**: Linux'ta en yaygın kullanılan dosya sistemi. Hızlı, güvenilir ve büyük dosyaları destekler.
- **XFS**: Büyük ölçekli depolama sistemleri için optimize edilmiştir.
- **Btrfs**: Yeni nesil dosya sistemi, gelişmiş özellikler sunar (anlık görüntüler, veri sıkıştırma, vb.).
- **vfat**: Windows ile uyumlu dosya sistemi.

## Dosya Sisteminin Bağlanması ve Çıkarılması

### Bağlama (Mount)

Bir dosya sistemi, belirli bir dizine bağlandığında (`mount` işlemi), o dosya sistemi kullanıma hazır hale gelir.

Bağlamak için:

```bash
sudo mount /dev/sdX1 /mnt
```

Bu komut, `/dev/sdX1` aygıtını `/mnt` dizinine bağlar.

### Çıkarma (Unmount)

Bağlı bir dosya sistemini çıkarmak için:

```bash
sudo umount /mnt
```

Bu komut, `/mnt` dizinindeki dosya sistemini güvenli bir şekilde çıkarır.

## Sabit ve Sembolik Bağlantılar

### Sabit Bağlantı (Hard Link)

Bir dosyanın birden fazla ismi olabilir ve bu isimler sabit bağlantılar olarak adlandırılır. Sabit bağlantı, aynı dosyayı işaret eden başka bir dosya oluşturarak yapılır.

Sabit bağlantı oluşturmak için:

```bash
ln dosya_adı yeni_bağlantı_adı
```

### Sembolik Bağlantı (Symbolic Link)

Sembolik bağlantılar, bir dosyaya veya dizine işaret eden özel bir dosya türüdür. Bu bağlantılar, asıl dosyanın konumunu gösterir.

Sembolik bağlantı oluşturmak için:

```bash
ln -s dosya_adı sembolik_bağlantı
```

