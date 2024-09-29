## Shell Script Nedir?

Shell script, Linux sistemlerinde komutların bir dosyada toplu olarak yürütülmesini sağlayan betik dosyalarıdır. Bu betik dosyaları, sıklıkla sistem yönetimi görevlerini otomatikleştirmek, rutin işleri kolaylaştırmak ve kullanıcı etkileşimi olmadan komutların çalışmasını sağlamak için kullanılır.

Linux'ta en yaygın kullanılan kabuk (shell) **Bash**'dir. Bash shell'de yazılan betiklere **Bash Script** denir, ancak başka kabuklar da (örn. zsh, ksh, fish) script yazmak için kullanılabilir.

## Shell Script Dosyasının Yapısı

Bir shell script dosyası genellikle `.sh` uzantısına sahiptir ve aşağıdaki genel yapı ile oluşturulur:

1. **Shebang (#!)**
   - Bir shell script dosyası, ilk satırında kabuğu belirten bir shebang ifadesi ile başlar. Bu ifade, betiğin hangi yorumlayıcı (shell) tarafından çalıştırılacağını belirtir.
   
   Örneğin:
   ```bash
   #!/bin/bash
   ```

2. **Yorum Satırları**
   - Satır başına `#` işareti koyarak, betik içerisinde açıklamalar ve notlar ekleyebilirsiniz. Bu satırlar çalıştırılmaz.
   
   Örneğin:
   ```bash
   # Bu betik sistem bilgilerini toplar.
   ```

3. **Komutlar**
   - Betik içerisine Linux komutlarını yazarak bu komutların sırayla yürütülmesini sağlayabilirsiniz.

   Örneğin:
   ```bash
   echo "Merhaba, dünya!"
   ```

4. **Değişkenler**
   - Shell script içinde değişkenler tanımlayabilir ve bu değişkenlerle işlem yapabilirsiniz.
   
   Örneğin:
   ```bash
   isim="Halil"
   echo "Merhaba, $isim!"
   ```

## Shell Script Örneği

Aşağıda, basit bir sistem bilgilerini görüntüleyen shell script örneği bulunmaktadır:

```bash
#!/bin/bash

# Sistem bilgilerini gösteren basit bir betik

echo "Sistem Bilgileri:"
echo "Kullanıcı: $(whoami)"
echo "Tarih: $(date)"
echo "Çalışan süreçler:"
ps -e
```

### Çalıştırma İzni Verme

Bir shell script oluşturduktan sonra, bu betiğin çalıştırılabilir olması için izin vermeniz gerekir. Bunu yapmak için şu komutu kullanabilirsiniz:

```bash
chmod +x betik_adi.sh
```

Bu komut, betiğe çalıştırma izni (execute permission) verecektir.

### Shell Script'i Çalıştırma

Bir shell script'i çalıştırmak için, betik dosyasını şu şekilde çalıştırabilirsiniz:

```bash
./betik_adi.sh
```

## Değişkenler ve Parametreler

Shell script'lerde değişkenler kullanarak değerleri saklayabilir ve kullanabilirsiniz. Değişkenler bir komutun sonucu olarak atanabilir, sabit değerler saklanabilir veya kullanıcı girdisi olarak alınabilir.

Örneğin:

```bash
#!/bin/bash

ad="Gökalp"
echo "Merhaba, $ad!"
```

### Özel Parametreler

Shell script'ler parametreler alabilir. Script'inizin çalıştırılması sırasında komut satırında verilen parametreler, sırasıyla `$1`, `$2`, `$3` gibi değişkenler ile tutulur.

Örneğin:

```bash
#!/bin/bash

echo "Birinci parametre: $1"
echo "İkinci parametre: $2"
```

Bu betik şu şekilde çalıştırılabilir:

```bash
./betik.sh parametre1 parametre2
```

Çıktısı ise şöyle olacaktır:

```
Birinci parametre: parametre1
İkinci parametre: parametre2
```

## Koşullu İfadeler

Koşullu ifadeler, belirli bir koşulun doğru olup olmadığını kontrol etmek için kullanılır. `if`, `else`, `elif` yapıları en yaygın kullanılan koşullu yapılardır.

Örneğin:

```bash
#!/bin/bash

sayi=10

if [ $sayi -gt 5 ]; then
    echo "Sayı 5'ten büyük."
else
    echo "Sayı 5'ten küçük veya eşit."
fi
```

Bu örnekte, eğer `sayi` 5'ten büyükse, "Sayı 5'ten büyük." yazdırılacaktır.

## Döngüler

Linux shell script'lerde döngüler kullanılarak tekrar eden işlemler yapılabilir. En yaygın kullanılan döngü yapıları `for`, `while` ve `until` döngüleridir.

### `for` Döngüsü

Bir listedeki her bir eleman üzerinde işlem yapmak için kullanılır.

```bash
#!/bin/bash

for dosya in *.txt; do
    echo "Dosya adı: $dosya"
done
```

Bu betik, bulunduğu dizindeki tüm `.txt` dosyalarının isimlerini ekrana yazdırır.

### `while` Döngüsü

Belirli bir koşul sağlandığı sürece işlemleri tekrarlayan döngüdür.

```bash
#!/bin/bash

sayi=1

while [ $sayi -le 5 ]; do
    echo "Sayı: $sayi"
    sayi=$((sayi + 1))
done
```

Bu betik, 1'den 5'e kadar olan sayıları ekrana yazdıracaktır.

## Fonksiyonlar

Shell script'lerde fonksiyonlar kullanarak tekrarlayan işlemleri bir kez tanımlayıp, ihtiyaç duyduğunuzda çağırabilirsiniz.

Örneğin:

```bash
#!/bin/bash

# Fonksiyon tanımı
fonksiyon_adi() {
    echo "Bu bir fonksiyondur."
}

# Fonksiyon çağrısı
fonksiyon_adi
```

Bu betik çalıştırıldığında, fonksiyonun içerisindeki komutlar çalıştırılır ve "Bu bir fonksiyondur." yazısı ekrana basılır.

