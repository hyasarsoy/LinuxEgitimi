# Dosya ve Dizin Yönetimi

## 1. Linux Dosya Sistemi ve Dizin Yapısı

Linux işletim sistemi, hiyerarşik bir dosya sistemi yapısına sahiptir. Tüm dosya ve dizinler, kök dizin (`/`) altında organize edilir. Bu yapı, dosya ve dizinlerin daha düzenli bir şekilde yönetilmesine yardımcı olur. Dosya ve dizin yönetimi, sistem yönetimi ve kullanıcı işlemlerinde oldukça önemlidir.

## 2. Temel Dosya ve Dizin Komutları

Linux’te dosya ve dizinlerle çalışmak için kullanılan temel komutlar şunlardır:

### 2.1. Dizin Listeleme - `ls`
Bir dizindeki dosya ve dizinleri listelemek için kullanılır.

```bash
ls
```

Bazı yaygın seçenekler:
- **`ls -l`**: Uzun formatta listeleme yapar (detaylı bilgi verir).
- **`ls -a`**: Gizli dosyaları da listeler.
- **`ls -lh`**: Dosya boyutlarını insan tarafından okunabilir formatta gösterir.

### 2.2. Dizin Değiştirme - `cd`
Bir dizinden diğerine geçiş yapmak için kullanılır.

```bash
cd /path/to/directory
```

- **`cd ~`**: Kullanıcının ana dizinine gider.
- **`cd ..`**: Bir üst dizine geçer.

### 2.3. Mevcut Dizin Görüntüleme - `pwd`
Mevcut çalışma dizinini (hangi dizinde olduğunuzu) gösterir.

```bash
pwd
```

### 2.4. Dosya ve Dizin Oluşturma

#### Dosya Oluşturma - `touch`
Yeni bir dosya oluşturmak için kullanılır.

```bash
touch dosya_adi.txt
```

#### Dizin Oluşturma - `mkdir`
Yeni bir dizin oluşturmak için kullanılır.

```bash
mkdir yeni_dizin
```

- **`mkdir -p /path/to/directory`**: Alt dizinlerle birlikte bir dizin oluşturur.

### 2.5. Dosya ve Dizin Kopyalama

#### Dosya Kopyalama - `cp`
Dosya kopyalamak için kullanılır.

```bash
cp dosya_adi.txt /hedef/dizin/
```

- **`cp -r dizin_adi /hedef/dizin/`**: Dizinleri ve içindeki dosyaları kopyalamak için kullanılır.

### 2.6. Dosya ve Dizin Taşıma - `mv`
Dosya veya dizin taşımak ve yeniden adlandırmak için kullanılır.

```bash
mv dosya_adi.txt /hedef/dizin/
```

- **`mv eski_isim.txt yeni_isim.txt`**: Bir dosyanın adını değiştirmek için.

### 2.7. Dosya ve Dizin Silme

#### Dosya Silme - `rm`
Dosya silmek için kullanılır.

```bash
rm dosya_adi.txt
```

- **`rm -f dosya_adi.txt`**: Kullanıcı onayı istemeden dosyayı zorla siler.
- **`rm -r dizin_adi/`**: Bir dizini ve içindekileri siler.

### 2.8. Boş Bir Dizin Silme - `rmdir`
Boş dizinleri silmek için kullanılır.

```bash
rmdir bos_dizin
```

## 3. Dosya ve Dizin İzinleri

Linux’te her dosya ve dizin, belirli kullanıcı izinlerine sahiptir. Bu izinler, dosyanın sahibi, grubu ve diğer kullanıcılar için belirlenebilir. İzinler, `r` (okuma), `w` (yazma) ve `x` (çalıştırma) olarak ifade edilir.

### 3.1. Dosya İzinlerini Görüntüleme - `ls -l`
Bir dosyanın veya dizinin izinlerini görüntülemek için kullanılır.

```bash
ls -l dosya_adi.txt
```

Çıktı örneği:

```bash
-rw-r--r-- 1 kullanıcı grup 0 Sep 23 10:00 dosya_adi.txt
```

- İlk karakter dosya türünü gösterir (`-` normal dosya, `d` dizin).
- Sonraki üçlüler sırasıyla sahibin, grubun ve diğer kullanıcıların izinlerini gösterir.

### 3.2. Dosya İzinlerini Değiştirme - `chmod`
Bir dosyanın veya dizinin izinlerini değiştirmek için kullanılır.

```bash
chmod 755 dosya_adi.txt
```

Bu örnek, dosya sahibine tüm izinleri (`rwx`), gruba ve diğer kullanıcılara ise okuma ve çalıştırma izni (`rx`) verir.

### 3.3. Dosya Sahipliğini Değiştirme - `chown`
Bir dosyanın veya dizinin sahipliğini değiştirmek için kullanılır.

```bash
chown yeni_sahip dosya_adi.txt
```

- **`chown yeni_sahip:yeni_grup dosya_adi.txt`**: Hem sahip hem grup değiştirilir.

## 4. Sabit ve Sembolik Bağlantılar

### 4.1. Sabit Bağlantı Oluşturma - `ln`
Aynı dosyaya birden fazla ad vermek için kullanılır.

```bash
ln dosya_adi.txt sabit_baglanti.txt
```

### 4.2. Sembolik Bağlantı Oluşturma - `ln -s`
Bir dosya veya dizine işaret eden sembolik bağlantı (kısayol) oluşturur.

```bash
ln -s /orijinal/yol/dosya_adi.txt sembolik_baglanti.txt
```

## 5. Dosya Arama

Linux sisteminde bir dosyayı bulmak için aşağıdaki komutları kullanabilirsiniz:

### 5.1. `find`
Belirli bir dizin altında dosya veya dizinleri arar.

```bash
find /arama_yolu -name dosya_adi.txt
```

- **`find / -type f -name "*.txt"`**: Tüm sistemde `.txt` uzantılı dosyaları arar.

### 5.2. `locate`
Önceden oluşturulmuş bir veritabanı kullanarak hızlı arama yapar.

```bash
locate dosya_adi.txt
```

### 5.3. `which`
Bir komutun hangi dizin altında olduğunu gösterir.

```bash
which ls
```

 

Bu içerik, dosya ve dizin yönetimi ile ilgili temel bilgileri ve komutları ayrıntılı bir şekilde sunmaktadır.
