### Proje: Kullanıcı Giriş ve Yetki Sistemi 

#### 1. Proje Tanımı:
Bu projede, kullanıcı adı ve şifre girişlerini kontrol eden bir Bash betiği oluşturacağız. Giriş yapan kullanıcının rolüne göre (Admin ya da Kullanıcı) yetki seviyesini belirleyen bir sistem olacak.

#### 2. Kullanılacak Değişkenler:
- **kullanici_adi**: Kullanıcının giriş için girdiği kullanıcı adı.
- **sifre**: Kullanıcının girdiği şifre.
- **kullanici_rolu**: Kullanıcının sistemdeki rolü (Admin veya Kullanıcı).
- **giris_basarili**: Girişin başarılı olup olmadığını belirten değişken.

#### 3. Bash Script Örneği:

```bash
#!/bin/bash

# Önceden tanımlanmış kullanıcı bilgileri
dogru_kullanici_adi="admin"
dogru_sifre="12345"
kullanici_rolu="Admin"  # Bu kullanıcı Admin yetkisine sahip

# Kullanıcıdan giriş bilgilerini alalım
read -p "Kullanıcı adınızı girin: " kullanici_adi
read -sp "Şifrenizi girin: " sifre
echo

# Giriş kontrolü
if [[ "$kullanici_adi" == "$dogru_kullanici_adi" && "$sifre" == "$dogru_sifre" ]]; then
    giris_basarili=true
    echo "Giriş başarılı!"
else
    giris_basarili=false
    echo "Kullanıcı adı veya şifre hatalı."
fi

# Eğer giriş başarılı ise kullanıcının yetkisini kontrol edelim
if [ "$giris_basarili" = true ]; then
    if [ "$kullanici_rolu" = "Admin" ]; then
        echo "Hoş geldiniz, Admin! Sistemde tam yetkiniz var."
    elif [ "$kullanici_rolu" = "Kullanıcı" ]; then
        echo "Hoş geldiniz, Kullanıcı! Sınırlı erişiminiz var."
    else
        echo "Hoş geldiniz! Yetkiniz belirsiz, lütfen yöneticinizle iletişime geçin."
    fi
else
    echo "Giriş başarısız, lütfen tekrar deneyin."
fi
```

#### 4. Proje Açıklaması:
- **Değişkenler**: `kullanici_adi`, `sifre`, ve `kullanici_rolu` gibi değişkenler kullanılarak giriş bilgileri ve rol kontrolü yapılır.
- **Kontroller**: Kullanıcıdan alınan veriler if-else yapıları ile kontrol edilir. Şifre doğru girilirse, `giris_basarili=true` olarak ayarlanır ve ardından rol kontrolü yapılır.
- **Yetkilendirme**: Eğer kullanıcı **Admin** ise tam yetki mesajı, **Kullanıcı** ise sınırlı erişim mesajı gösterilir.

#### 5. Proje Nasıl Çalışır?
1. Kullanıcıdan kullanıcı adı ve şifre girişleri istenir.
2. Giriş bilgileri doğru ise kullanıcıya rolüne göre bir mesaj gösterilir.
3. Yanlış bilgi girildiğinde hata mesajı verilir ve giriş tekrar denenebilir.

#### 6. Proje Genişletme Fikirleri:
- **Çoklu Kullanıcı Desteği**: Birden fazla kullanıcının bilgilerini bir dosyaya kaydederek sisteminizi genişletebilirsiniz.
- **Kayıt Tutma**: Başarısız giriş denemelerini bir dosyada log tutarak güvenliği artırabilirsiniz.
- **Güvenlik Önlemleri**: Yanlış şifre girişlerinde belirli bir deneme sayısından sonra hesabı kilitleme veya süreli olarak erişimi kapatma gibi güvenlik mekanizmaları ekleyebilirsiniz.

### Çalıştırma Adımları:
1. Bash scriptini bir dosyaya kaydedin, örneğin `giris_sistemi.sh`.
2. Terminalde aşağıdaki komut ile scriptin çalıştırılabilir olmasını sağlayın:

   ```bash
   chmod +x giris_sistemi.sh
   ```

3. Ardından scripti şu şekilde çalıştırabilirsiniz:

   ```bash
   ./giris_sistemi.sh
   ```


### Bütün bu adımları tamamladıktan sonra kendi sisteminizde yaptığınızda dair ekran görüntüleri ve script dosyasını bana iletmenizi rica ederim

