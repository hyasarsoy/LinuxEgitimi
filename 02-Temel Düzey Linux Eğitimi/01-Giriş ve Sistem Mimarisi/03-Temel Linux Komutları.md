
# 03 - Temel Linux Komutları

Linux terminali, kullanıcılara işletim sistemi ile doğrudan iletişim kurma imkanı veren güçlü bir araçtır. Bu bölümde, en temel Linux komutlarını öğreneceğiz ve terminalde nasıl verimli bir şekilde çalışabileceğinizi göstereceğiz.

## 1. Dizinler ve Dosyalarla Çalışma

### `pwd` - Bulunduğunuz Dizini Göster
Bulunduğunuz mevcut dizini gösterir.
```bash
pwd
```

### `ls` - Dizin İçeriğini Listele
Bir dizindeki dosya ve dizinlerin listesini gösterir.
```bash
ls
```
Bazı yaygın kullanılan seçenekler:
- `ls -l`: Ayrıntılı listeleme modu (dosya izinleri, sahiplik, boyut ve tarih gibi bilgilerle birlikte)
- `ls -a`: Gizli dosyaları da gösterir (.` ile başlayan dosyalar)

### `cd` - Dizin Değiştir
Bir dizinden başka bir dizine geçiş yapmanızı sağlar.
```bash
cd /yol/dizine
```
Örnek: Ev dizinine gitmek için:
```bash
cd ~
```

### `cp` - Dosya veya Dizin Kopyalama
Bir dosyayı ya da dizini başka bir konuma kopyalar.
```bash
cp kaynak hedef
```
Örnek: `file.txt` dosyasını `backup/` dizinine kopyalamak için:
```bash
cp file.txt backup/
```

### `mv` - Dosya veya Dizin Taşıma
Dosyaları veya dizinleri taşımak ya da yeniden adlandırmak için kullanılır.
```bash
mv eski_isim yeni_isim
```
Örnek: `file.txt` dosyasını `documents/` dizinine taşımak için:
```bash
mv file.txt documents/
```

### `rm` - Dosya Silme
Dosyaları silmek için kullanılır. **Dikkatli kullanın, çünkü silinen dosyalar geri getirilemez.**
```bash
rm dosya_adi
```
Eğer bir dizini ve içeriğini silmek isterseniz, şu komut kullanılır:
```bash
rm -r dizin_adi
```

### `mkdir` - Dizin Oluşturma
Yeni bir dizin (klasör) oluşturur.
```bash
mkdir yeni_dizin
```

### `rmdir` - Boş Dizin Silme
Sadece boş dizinleri silmek için kullanılır.
```bash
rmdir dizin_adi
```

### `touch` - Dosya Oluşturma
Yeni boş bir dosya oluşturmak için kullanılır.
```bash
touch dosya_adi
```

## 2. Dosya İçeriğiyle İlgili Komutlar

### `cat` - Dosya İçeriğini Görüntüleme
Bir dosyanın içeriğini terminalde görüntülemek için kullanılır.
```bash
cat dosya_adi
```

### `head` - Dosyanın İlk Satırlarını Görüntüleme
Bir dosyanın başından itibaren belirli sayıda satırı görüntülemek için kullanılır. Varsayılan olarak ilk 10 satırı gösterir.
```bash
head dosya_adi
```

### `tail` - Dosyanın Son Satırlarını Görüntüleme
Bir dosyanın sonundan itibaren belirli sayıda satırı görüntülemek için kullanılır. Varsayılan olarak son 10 satırı gösterir.
```bash
tail dosya_adi
```

### `nano` ve `vim` - Metin Düzenleyiciler
Linux terminalinde dosyaları düzenlemek için kullanılan metin editörleridir. Örnek olarak:
- `nano dosya_adi`: Nano ile dosya düzenleme
- `vim dosya_adi`: Vim ile dosya düzenleme

## 3. Sistem Bilgileri ve Yönetim Komutları

### `uname` - Sistem Bilgilerini Görüntüleme
Kullanılan Linux çekirdeği ve sistem hakkında temel bilgileri verir.
```bash
uname -a
```

### `top` - Çalışan Süreçleri Görüntüleme
Anlık olarak çalışan işlemleri ve sistem kaynak kullanımını gösterir.
```bash
top
```

### `ps` - Süreçleri Görüntüleme
Çalışan süreçleri görüntüler.
```bash
ps aux
```

### `kill` - Süreç Sonlandırma
Bir süreç numarasına (PID) göre süreçleri sonlandırmak için kullanılır.
```bash
kill PID
```
Eğer süreç sonlanmazsa, şu komut ile zorla sonlandırabilirsiniz:
```bash
kill -9 PID
```

## 4. Yardım ve Manuel Sayfalar

### `man` - Komutlar için Kılavuz Sayfalarını Görüntüleme
Bir komutun kullanımına dair detaylı bilgi almak için kullanılır.
```bash
man komut_adi
```

### `--help` - Komutlar için Yardım
Bir komutun kullanımına dair hızlı bir yardım çıktısı almak için kullanılır.
```bash
komut_adi --help
```

## 5. Dosya ve Dizin İzinleri

### `chmod` - Dosya İzinlerini Değiştirme
Bir dosya veya dizinin erişim izinlerini değiştirmek için kullanılır.
```bash
chmod 755 dosya_adi
```

### `chown` - Dosya Sahipliğini Değiştirme
Bir dosya veya dizinin sahibi ve grubu değiştirmek için kullanılır.
```bash
chown kullanıcı:grup dosya_adi
```

## Sonuç
Bu bölümde, Linux terminalinde kullanılabilecek temel komutları öğrendik. Dosya ve dizinlerle çalışmak, süreçleri yönetmek ve sistem bilgilerini görüntülemek gibi temel işlemleri gerçekleştirdik. Bu komutlarla terminalde daha etkin bir şekilde çalışabilir ve sistem yönetimini daha iyi anlayabilirsiniz.
```

Bu içerik, **Temel Linux Komutları** konusunda kapsamlı bir rehber sağlayarak, eğitim sürecinde öğrencilerin terminalde temel işlemleri öğrenmelerini ve uygulamalarını sağlar.
