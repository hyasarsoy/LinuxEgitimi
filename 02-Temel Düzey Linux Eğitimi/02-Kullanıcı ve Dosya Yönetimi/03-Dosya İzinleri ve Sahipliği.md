
# Dosya İzinleri ve Sahipliği

Linux işletim sistemlerinde, her dosya ve dizin bir kullanıcıya ve bir gruba ait olarak yapılandırılır. Dosya izinleri ve sahipliği, sistemdeki dosyalara kimlerin erişebileceğini ve hangi işlemleri gerçekleştirebileceğini belirler. Bu bölümde dosya izinleri ve sahipliği yönetimi üzerine temel bilgiler verilecektir.

## 1. Dosya İzinleri

Linux’ta her dosya ve dizin için üç temel izin türü vardır:

- **r**: Okuma (Read)
- **w**: Yazma (Write)
- **x**: Çalıştırma (Execute)

Bu izinler, üç farklı kullanıcı düzeyi için ayrı ayrı tanımlanır:

- **Sahip** (User): Dosyanın sahibi olan kullanıcı.
- **Grup** (Group): Dosyanın ait olduğu grup.
- **Diğer** (Others): Sahip ve grup dışındaki tüm kullanıcılar.

### 1.1. İzinleri Görüntüleme

Bir dosya veya dizinin izinlerini görüntülemek için `ls -l` komutu kullanılır:

```bash
ls -l <dosya_adı>
```

Çıktı şu şekilde olur:

```bash
-rw-r--r-- 1 kullanıcı grup 4096 Sep 12 12:00 dosya.txt
```

Bu çıktıda:

- İlk karakter (`-`), dosya türünü gösterir. Örneğin, `-` normal bir dosya, `d` ise bir dizini temsil eder.
- `rw-r--r--`: Bu bölüm dosyanın izinlerini temsil eder.
  - `rw-`: Sahip için okuma (r) ve yazma (w) izni var, çalıştırma izni yok (-).
  - `r--`: Grup için sadece okuma (r) izni var.
  - `r--`: Diğer kullanıcılar için de sadece okuma (r) izni var.

### 1.2. İzinleri Değiştirme

Bir dosya veya dizinin izinlerini değiştirmek için `chmod` komutu kullanılır. İzinler, ya sembolik (r, w, x) ya da sayısal (0-7 arası değerlerle) olarak belirtilebilir.

#### Sembolik İzin Değişiklikleri

Sahip, grup ve diğer kullanıcılar için izinleri sembolik olarak şu şekilde değiştirebilirsiniz:

- Sahibe yazma izni eklemek için:

```bash
chmod u+w <dosya_adı>
```

- Gruba çalıştırma izni eklemek için:

```bash
chmod g+x <dosya_adı>
```

- Diğer kullanıcılardan okuma iznini kaldırmak için:

```bash
chmod o-r <dosya_adı>
```

#### Sayısal İzin Değişiklikleri

Dosya izinleri, her izin türü için 0-7 arasında sayısal değerlerle de belirtilebilir:

- **r = 4**, **w = 2**, **x = 1**

Her biri toplandığında izinlerin sayısal karşılıkları elde edilir. Örneğin, `rwx` için değer 7 (4+2+1) olur. Tüm izinlerin sayısal formatı şu şekildedir:

- Sahip, grup ve diğer kullanıcılar için tüm izinleri (rwx) vermek:

```bash
chmod 777 <dosya_adı>
```

- Sahibe tüm izinleri, gruba sadece okuma izni, diğer kullanıcılara ise hiçbir izin vermemek:

```bash
chmod 740 <dosya_adı>
```

## 2. Dosya Sahipliği

Linux’ta her dosya ve dizin, bir kullanıcıya ve bir gruba ait olarak tanımlanır. Bu sahiplik bilgileri, dosyanın hangi kullanıcı ve grup tarafından yönetilebileceğini belirler.

### 2.1. Sahipliği Görüntüleme

Bir dosyanın sahipliğini görmek için `ls -l` komutu kullanılır. Komut çıktısında ikinci ve üçüncü sütunlar sırasıyla dosyanın sahibi ve grubunu gösterir:

```bash
ls -l <dosya_adı>
```

Örneğin:

```bash
-rw-r--r-- 1 ali kullanıcılar 4096 Sep 12 12:00 dosya.txt
```

Bu çıktıda, `ali` dosyanın sahibi, `kullanıcılar` ise dosyanın ait olduğu gruptur.

### 2.2. Sahipliği Değiştirme

Dosya veya dizin sahipliğini değiştirmek için `chown` komutu kullanılır. Örneğin, bir dosyanın sahipliğini değiştirmek için:

```bash
sudo chown yeni_sahip <dosya_adı>
```

Grup sahipliğini değiştirmek için:

```bash
sudo chown :yeni_grup <dosya_adı>
```

Hem sahip hem grup aynı anda değiştirilmek istenirse:

```bash
sudo chown yeni_sahip:yeni_grup <dosya_adı>
```

### 2.3. Dosya Grubunu Değiştirme

Sadece dosyanın grup sahipliğini değiştirmek için `chgrp` komutu kullanılabilir:

```bash
sudo chgrp <yeni_grup> <dosya_adı>
```

## 3. Özel İzinler

Linux’ta bazı dosyalar için özel izinler de tanımlanabilir:

- **SUID (Set User ID)**: Bir dosya çalıştırıldığında, çalıştıran kullanıcıya dosyanın sahibi yetkileri verilir.
- **SGID (Set Group ID)**: Bir dosya çalıştırıldığında, çalıştıran kullanıcıya dosyanın grup yetkileri verilir.
- **Sticky Bit**: Bu bit bir dizine uygulandığında, sadece dosyanın sahibi veya root kullanıcı dosyayı silebilir.

Bu özel izinleri eklemek için `chmod` komutunda şu sembolleri kullanabilirsiniz:

- SUID eklemek için:

```bash
chmod u+s <dosya_adı>
```

- SGID eklemek için:

```bash
chmod g+s <dosya_adı>
```

- Sticky Bit eklemek için:

```bash
chmod +t <dizin_adı>
```

