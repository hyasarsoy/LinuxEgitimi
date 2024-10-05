# Input ve Output (Girdi ve Çıktı) Kullanımı

Linux ve Unix tabanlı sistemlerde `input` (girdi) ve `output` (çıktı) yönetimi, komut satırı kullanırken temel bir rol oynar. Komutlar çalıştırıldığında, girdiler alabilir ve çıktılar üretebilir. Bu rehberde, girdilerin nasıl yönlendirileceği ve çıktıların nasıl işleneceği detaylandırılacaktır.

## 1. Input ve Output Kavramları

- **Input (Girdi):** Bir komutun veya programın çalışması için gereken veriler. Genellikle klavye veya bir dosyadan alınır.
- **Output (Çıktı):** Bir komut veya programın çalıştıktan sonra ürettiği sonuçlar. Genellikle ekrana (standart çıkışa) yazdırılır.

## 2. Standart Akışlar

Bir Unix programı genellikle üç standart akış kullanır:

1. **Standart Girdi (stdin)**:
   - Dosya tanımlayıcısı: `0`
   - Programın giriş verilerini aldığı akış. Varsayılan olarak klavyeden gelir.
   
2. **Standart Çıktı (stdout)**:
   - Dosya tanımlayıcısı: `1`
   - Programın normal çıktısını gönderdiği akış. Varsayılan olarak terminale (ekrana) yazdırılır.
   
3. **Standart Hata (stderr)**:
   - Dosya tanımlayıcısı: `2`
   - Programın hata mesajlarını gönderdiği akış. Varsayılan olarak terminale yazdırılır.

## 3. Girdi ve Çıktı Yönlendirme

Linux'ta, girdiyi bir dosyadan almak veya çıktıyı bir dosyaya yazmak için yönlendirme operatörleri kullanılır.

### 3.1. Çıktı Yönlendirme (Output Redirection)

Bir komutun çıktısını bir dosyaya yönlendirmek için `>` kullanılır.

#### Örnek:
```bash
echo "Merhaba Dünya" > cikti.txt
```
Bu komut, `"Merhaba Dünya"` mesajını ekrana yazdırmak yerine `cikti.txt` dosyasına yönlendirir. Eğer dosya varsa üzerine yazar; yoksa yeni bir dosya oluşturur.

#### Ek: Üzerine Yazmadan Dosyaya Eklemek

Çıktıyı bir dosyaya eklemek için `>>` kullanılır.

#### Örnek:
```bash
echo "Yeni Satır" >> cikti.txt
```
Bu komut, `"Yeni Satır"` ifadesini `cikti.txt` dosyasının sonuna ekler.

### 3.2. Girdi Yönlendirme (Input Redirection)

Bir komutun girdisini bir dosyadan almak için `<` kullanılır.

#### Örnek:
```bash
sort < dosya.txt
```
Bu komut, `dosya.txt` dosyasındaki verileri alır ve sıralar.

### 3.3. Standart Hata Yönlendirme (Error Redirection)

Bir komutun hata mesajlarını bir dosyaya yönlendirmek için `2>` kullanılır. Bu, hata çıktılarını belirli bir dosyaya yönlendirmeyi sağlar.

#### Örnek:
```bash
ls dosyaolmayan 2> hata.txt
```
Bu komut, var olmayan bir dosyayı listelemeye çalışırken oluşan hata mesajını `hata.txt` dosyasına yazacaktır.

### 3.4. Standart Çıktı ve Hata Yönlendirme

Standart çıktıyı ve hatayı aynı anda yönlendirmek için `&>` kullanılır.

#### Örnek:
```bash
komut &> cikti_ve_hata.txt
```
Bu komut, hem standart çıktıyı hem de hata mesajlarını `cikti_ve_hata.txt` dosyasına yönlendirecektir.

### 3.5. /dev/null Kullanımı

`/dev/null` özel bir dosyadır ve içine yazılan her şeyi yok eder. Bu, çıktı veya hatayı tamamen göz ardı etmek için kullanılabilir.

#### Örnek:
```bash
ls dosyaolmayan 2> /dev/null
```
Bu komut, hata mesajlarını yok ederek ekrana hiçbir şey yazdırmaz.

## 4. Pipe (Boru) Kullanımı

Boru `|`, bir komutun çıktısını başka bir komuta girdi olarak yönlendirmek için kullanılır. Bu sayede, birden fazla komut ardışık olarak çalıştırılabilir.

#### Örnek:
```bash
ls | grep "dosya"
```
Bu komut, `ls` çıktısında "dosya" kelimesini arar ve sadece bu kelimeyi içeren satırları ekrana yazdırır.

## 5. Çeşitli Kullanım Örnekleri

### 5.1. Girdi Dosyasını Okuma ve Çıktıyı Bir Dosyaya Yönlendirme

```bash
grep "kelime" < dosya.txt > sonuc.txt
```
Bu komut, `dosya.txt` içinde `"kelime"`yi arar ve sonuçları `sonuc.txt` dosyasına yazdırır.

### 5.2. Hata ve Standart Çıktıyı Bir Dosyaya Yönlendirme

```bash
komut > cikti.txt 2> hata.txt
```
Bu komut, standart çıktıyı `cikti.txt` dosyasına, hataları ise `hata.txt` dosyasına yönlendirir.

### 5.3. Girdiyi Klavye Yerine Dosyadan Alma

```bash
cat < dosya.txt
```
Bu komut, `dosya.txt` dosyasının içeriğini ekrana yazdırır.

### 5.4. Pipe ile Birleştirme

```bash
cat dosya.txt | sort | uniq > sirali_tekil.txt
```
Bu komut, `dosya.txt` dosyasının içeriğini önce sıralar, sonra yinelenen satırları çıkarır ve sonuçları `sirali_tekil.txt` dosyasına yazar.

## 6. Özel Dosya Tanımlayıcıları ile Yönlendirme

### 6.1. Standart Çıktıyı (1) ve Hataları (2) Aynı Anda Yönlendirme

```bash
komut > cikti.txt 2>&1
```
Bu komut, hem standart çıktıyı hem de hata çıktısını aynı dosyaya (`cikti.txt`) yönlendirir.

### 6.2. Sadece Standart Hataları Yönlendirme

```bash
komut 2> hata.txt
```
Bu komut, sadece hata çıktılarını `hata.txt` dosyasına yönlendirir.

## 7. `tee` Komutu ile Hem Dosyaya Hem de Ekrana Yazdırma

`tee` komutu, çıktıyı hem ekrana yazdırır hem de dosyaya kaydeder. `tee`, boru ile kullanıldığında oldukça faydalıdır.

#### Örnek:
```bash
ls | tee dosya.txt
```
Bu komut, `ls` çıktısını ekrana yazdırırken aynı zamanda `dosya.txt` dosyasına da kaydeder.

## 8. Özet

- **`>`:** Standart çıktıyı bir dosyaya yönlendirir.
- **`>>`:** Çıktıyı dosyanın sonuna ekler.
- **`<`:** Girdiyi bir dosyadan alır.
- **`2>`:** Hata çıktılarını yönlendirir.
- **`|`:** Boru operatörü, bir komutun çıktısını diğerine girdi olarak verir.
- **`tee`:** Çıktıyı hem dosyaya hem de ekrana yönlendirir.

Girdi ve çıktıları etkili bir şekilde yönetmek, komut satırı işlemlerini daha esnek ve güçlü hale getirir. Yönlendirme ve boru kullanımıyla karmaşık işlemleri kolaylaştırabilir ve çıktılarınızı daha verimli yönetebilirsiniz.

https://www.gnu.org/software/bash/manual/html_node/Redirections.html

**tty**


