### "Süper Gizli" Projesi Özeti

#### Görev 1:
Bu görevde, aşağıdaki adımları gerçekleştireceksiniz:

1. **super_secret_stuff** adında bir klasör oluşturun ve bu klasörün içine **top_secret.txt** adlı bir dosya koyun.
   - Dosyanın içeriği tamamen sizin tercihinize bağlıdır.
2. **updatedb** komutunu kullanarak sisteminizdeki dosya veritabanını güncelleyin (bu komut sudo ayrıcalıkları gerektirecektir).
3. **locate** komutunu kullanarak **top_secret.txt** dosyasının bulunduğu yolu bulun.
4. **locate** komutunun çıktısını kullanarak, bulduğunuz bu yolu **secret_place.txt** adlı yeni bir dosyaya, ev dizininizde (home directory) yönlendirin.

**İpucu:** `sudo` komutu ile veritabanını güncellerken süper kullanıcı haklarına sahip olmanız gerektiği için `sudo updatedb` komutunu kullanmalısınız.

#### Görev 2:

**Bölüm A:**

1. **find** komutunu kullanarak, sistemdeki 1 MebiByte'tan büyük dosyaları bulun.
   - Aramaya kök dizin (`/`) ile başlayın.
   - Aramanızı yalnızca 4 seviye derinliğe kadar sınırlayın (yani en fazla 4 alt dizine kadar).
   - Sadece **dosyaları** gösterin, dizinleri (klasörleri) göstermeyin.
   
2. **find** komutunun sonuçlarını elde ettiğiniz her dosya için **ls -lh** komutunu çalıştırın.
   - Bu komutla dosyaların boyutlarını da "insan tarafından okunabilir" (human-readable) formatta görmüş olacaksınız.

**İpucu:** Bu komutu çalıştırırken, tüm gerekli klasörlere erişim sağlamak için `sudo` komutunu kullanmanız gerekecek.

**Bölüm B:**

1. **Bölüm A'daki** çıktıyı **sort** komutunu kullanarak sıralayın.
   - Dosya boyutlarına göre sıralama yapmalısınız. En büyük dosyalar listenin en üstünde, en küçük dosyalar en altta olmalıdır.
   
2. **filesizes.txt** adında bir dosya oluşturun ve sıralanmış sonuçları bu dosyaya yönlendirin (output).
   
**İpucu 1:** `sort` komutu için **–k** seçeneğini kullanarak doğru sütunu (KEYDEF) belirlemelisiniz.  
**İpucu 2:** Dosya boyutları, `ls -lh` çıktısında 5. sütunda yer alır.  
**İpucu 3:** `sort` komutuna "human-readable" verileri işleyebilmesi için doğru parametreyi vermelisiniz. (Örneğin: `-h`)


**Sonuç: Kullandığınız bütün komutları iletebilirsiniz**
