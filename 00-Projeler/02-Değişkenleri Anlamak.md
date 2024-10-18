Here’s a detailed explanation of the text in Turkish:
# Ortam Değişkenleri

Temel değişkenleri anladıktan sonra, ortam değişkenlerini inceleyelim. Ortam değişkenleri, kabuğun alt işlemlerine sunulan değişkenlerdir. Yani, bu değişkenler kabuktan çalıştırılan komut dosyaları ve programlar tarafından erişilebilir.

```bash
Degisken="Merhaba, Linux"
```

```bash
echo $Degisken
```

Tüm mevcut ortam değişkenlerini görmek için `env` komutunu kullanın:

```bash
env
```

### Kodu Açıklayın
Bu komut, uzun bir değişken listesi gösterecektir. Henüz hepsini anlamamanız sorun değil - daha sonra en önemlilerinden bazılarını ele alacağız.

En önemli ortam değişkenlerinden biri `PATH`'dir. Ona bir göz atalım:

```bash
echo $PATH
```

### Kodu Açıklayın
`PATH` değişkeni, sistemin çalıştırılabilir programları aradığı dizinleri listeler. Her dizin iki nokta üst üste `(:)` ile ayrılır.

Şimdi kendi ortam değişkenimizi oluşturalım. Ortam değişkeni oluşturmak için `export` komutunu kullanırız:

```bash
export MY_ENV_VAR="Bu bir ortam değişkenidir"
```

### Kodu Açıklayın
`export` komutu, değişkeni alt işlemlere erişilebilir hale getirir. Bu, kabuk değişkenleri ile ortam değişkenleri arasındaki temel farktır.

Bu farkı göstermek için, hem normal bir kabuk değişkenine hem de ortam değişkenine erişmeye çalışan bir kabuk komut dosyası oluşturalım:

```bash
echo '#!/bin/bash
echo "Kabuk değişkeni: $my_var"
echo "Ortam değişkeni: $MY_ENV_VAR"' > test_vars.sh
```

### Kodu Açıklayın
Bu komut, basit bir kabuk komut dosyası oluşturur. Komut dosyası içinde hem bir kabuk değişkeni (`my_var`) hem de bir ortam değişkeni (`MY_ENV_VAR`) kullanılır.

Komut dosyasını çalıştırılabilir hale getirin:

```bash
chmod +x test_vars.sh
```

### Kodu Açıklayın
Bu komut, `test_vars.sh` komut dosyasını çalıştırılabilir hale getirir.

Şimdi komut dosyasını çalıştırın:

```bash
./test_vars.sh
```

### Kodu Açıklayın
Komut dosyasını çalıştırdığınızda, ortam değişkenine (`MY_ENV_VAR`) erişebildiğinizi, ancak kabuk değişkenine (`my_var`) erişemediğinizi göreceksiniz.

`MY_ENV_VAR`'ın artık bir ortam değişkeni olduğunu doğrulamak için, tekrar `env` komutunu kullanabiliriz, ancak bu sefer çıktıyı `grep` ile filtreleyeceğiz:

```bash
env | grep MY_ENV_VAR
```

### Kodu Açıklayın
Bu komut, yeni ortam değişkeninizi çıktıda gösterecektir.

Yeni ortam değişkeninizin değerini doğrudan kontrol edebilirsiniz:

```bash
echo $MY_ENV_VAR
```

### Kodu Açıklayın
Harika! Artık ilk ortam değişkeninizi oluşturdunuz ve bunun kabuk değişkeninden nasıl farklı olduğunu gördünüz. Temel fark, `export` ile oluşturulan ortam değişkenlerinin alt işlemlere erişilebilir olması, kabuk değişkenlerinin ise olmamasıdır.
`