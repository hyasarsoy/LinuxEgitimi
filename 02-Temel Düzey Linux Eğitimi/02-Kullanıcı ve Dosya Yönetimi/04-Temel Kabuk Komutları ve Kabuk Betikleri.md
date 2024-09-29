## Kabuk (Shell) Nedir?

Kabuk (shell), kullanıcının işletim sistemi ile etkileşim kurmasını sağlayan bir komut satırı aracıdır. Linux'ta en yaygın kullanılan kabuk, **Bash** (Bourne Again Shell) olup, kullanıcıların komutlar yazarak işletim sistemi üzerinde işlemler yapmasına olanak tanır. Kabuk, hem etkileşimli komutlar çalıştırmak hem de betikler (scripts) oluşturmak için kullanılabilir.

## Temel Kabuk Komutları

Linux kabuğunda sıkça kullanılan bazı temel komutlar şunlardır:

1. **`ls`**: Dizin içeriklerini listelemek için kullanılır.
   - `ls -l`: Dosyaların ayrıntılı listesini gösterir.
   - `ls -a`: Gizli dosyaları da listeye ekler.

2. **`cd`**: Dizin değiştirmek için kullanılır.
   - `cd /home/kullanıcı`: Belirtilen dizine gider.
   - `cd ..`: Bir üst dizine çıkar.

3. **`pwd`**: Bulunduğunuz mevcut dizini (print working directory) gösterir.

4. **`cp`**: Dosya veya dizinleri kopyalamak için kullanılır.
   - `cp kaynak hedef`: Kaynak dosyasını hedefe kopyalar.

5. **`mv`**: Dosya veya dizin taşımak ya da yeniden adlandırmak için kullanılır.
   - `mv eski_ad yeni_ad`: Dosyayı yeniden adlandırır.
   - `mv dosya /hedef_dizin`: Dosyayı belirtilen dizine taşır.

6. **`rm`**: Dosya veya dizin silmek için kullanılır.
   - `rm dosya`: Dosyayı siler.
   - `rm -r dizin`: Dizin ve içindeki tüm dosyaları siler.

7. **`mkdir`**: Yeni bir dizin oluşturmak için kullanılır.
   - `mkdir yeni_dizin`: Yeni bir dizin oluşturur.

8. **`rmdir`**: Boş bir dizini silmek için kullanılır.
   - `rmdir dizin_adı`: Boş dizini siler.

9. **`echo`**: Metni ya da değişkenleri ekrana yazdırmak için kullanılır.
   - `echo "Merhaba Dünya"`: "Merhaba Dünya" yazdırır.

10. **`cat`**: Dosya içeriğini ekranda görüntülemek için kullanılır.
    - `cat dosya`: Dosyanın içeriğini gösterir.

## Kabuk Betikleri (Shell Scripts)

Kabuk betikleri, Linux'ta ardışık komutları otomatik olarak çalıştırmak için kullanılan metin dosyalarıdır. Betikler, tekrarlanan görevleri otomatikleştirmeye yardımcı olur. Kabuk betikleri `.sh` uzantısıyla kaydedilebilir ve aşağıdaki gibi çalıştırılabilir.

### Basit Bir Kabuk Betiği Oluşturma

1. Yeni bir betik dosyası oluşturun:
   ```bash
   nano basit_betik.sh
   ```

2. Dosya içerisine aşağıdaki gibi basit bir betik yazın:
   ```bash
   #!/bin/bash
   echo "Bu basit bir kabuk betiğidir."
   ```

3. Betiği çalıştırılabilir hale getirin:
   ```bash
   chmod +x basit_betik.sh
   ```

4. Betiği çalıştırın:
   ```bash
   ./basit_betik.sh
   ```

Bu betik çalıştırıldığında ekrana `"Bu basit bir kabuk betiğidir."` yazdıracaktır.

### Değişkenler ve Kontrol Yapıları

Kabuk betiklerinde değişkenler ve kontrol yapıları kullanarak daha karmaşık işlemler gerçekleştirilebilir.

#### Değişkenler:
```bash
#!/bin/bash
ad="Ahmet"
echo "Merhaba, $ad!"
```

#### Koşullu İfadeler (if-else):
```bash
#!/bin/bash
sayi=10

if [ $sayi -gt 5 ]
then
   echo "Sayı 5'ten büyük."
else
   echo "Sayı 5'ten küçük veya eşit."
fi
```

#### Döngüler:
```bash
#!/bin/bash
for i in {1..5}
do
   echo "Sayı: $i"
done
```

### Betiklerin Kullanım Alanları
Kabuk betikleri çeşitli alanlarda kullanılır, örneğin:
- Sistem yönetim görevlerini otomatikleştirmek.
- Yedekleme işlemlerini gerçekleştirmek.
- Ağ yapılandırmalarını kontrol etmek.
- Rutin görevleri zamanlamak ve otomatikleştirmek.
