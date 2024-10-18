
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


Bu komut, uzun bir değişken listesi gösterecektir. Henüz hepsini anlamamanız sorun değil - daha sonra en önemlilerinden bazılarını ele alacağız.

En önemli ortam değişkenlerinden biri `PATH`'dir. Ona bir göz atalım:

```bash
echo $PATH
```


`PATH` değişkeni, sistemin çalıştırılabilir programları aradığı dizinleri listeler. Her dizin iki nokta üst üste `(:)` ile ayrılır.

Şimdi kendi ortam değişkenimizi oluşturalım. Ortam değişkeni oluşturmak için `export` komutunu kullanırız:

```bash
export MY_ENV_VAR="Bu bir ortam değişkenidir"
```


`export` komutu, değişkeni alt işlemlere erişilebilir hale getirir. Bu, kabuk değişkenleri ile ortam değişkenleri arasındaki temel farktır.

Bu farkı göstermek için, hem normal bir kabuk değişkenine hem de ortam değişkenine erişmeye çalışan bir kabuk komut dosyası oluşturalım:

```bash
echo '#!/bin/bash
echo "Kabuk değişkeni: $my_var"
echo "Ortam değişkeni: $MY_ENV_VAR"' > test_vars.sh
```


Bu komut, basit bir kabuk komut dosyası oluşturur. Komut dosyası içinde hem bir kabuk değişkeni (`my_var`) hem de bir ortam değişkeni (`MY_ENV_VAR`) kullanılır.

Komut dosyasını çalıştırılabilir hale getirin:

```bash
chmod +x test_vars.sh
```


Bu komut, `test_vars.sh` komut dosyasını çalıştırılabilir hale getirir.

Şimdi komut dosyasını çalıştırın:

```bash
./test_vars.sh
```


Komut dosyasını çalıştırdığınızda, ortam değişkenine (`MY_ENV_VAR`) erişebildiğinizi, ancak kabuk değişkenine (`my_var`) erişemediğinizi göreceksiniz.

`MY_ENV_VAR`'ın artık bir ortam değişkeni olduğunu doğrulamak için, tekrar `env` komutunu kullanabiliriz, ancak bu sefer çıktıyı `grep` ile filtreleyeceğiz:

```bash
env | grep MY_ENV_VAR
```


Bu komut, yeni ortam değişkeninizi çıktıda gösterecektir.

Yeni ortam değişkeninizin değerini doğrudan kontrol edebilirsiniz:

```bash
echo $MY_ENV_VAR
```


# PATH Ortam Değişkenini Değiştirme

Linux'ta `PATH` değişkeni en önemli ortam değişkenlerinden biridir. Sistem, çalıştırılabilir dosyaları nerede arayacağını bu değişkenden öğrenir. Şimdi bu değişkene yeni bir dizin ekleyerek nasıl değiştirebileceğimizi görelim.

Öncelikle, özel scriptlerinizi saklayabileceğiniz yeni bir dizin oluşturalım:

```bash
mkdir ~/my_scripts
```


Bu komut, home dizininde `my_scripts` adında bir dizin oluşturur. Bu dizin, kullanıcıya özel scriptlerin saklanacağı bir yer olacaktır.

Şimdi, bu yeni dizini `PATH`'inize ekleyelim. Yine `export` komutunu kullanacağız, ancak bu sefer var olan bir ortam değişkenini değiştireceğiz:

```bash
export PATH="$PATH:$HOME/my_scripts"
```


Bu komutu şu şekilde parçalara ayıralım:
- `$PATH` şu anda `PATH`'in mevcut değerini gösterir.
- `:` dizinleri `PATH`'de ayırmak için kullanılır.
- `$HOME`, home dizininizi gösteren bir ortam değişkenidir.

Bu komutla, `:$HOME/my_scripts` yolunu mevcut `PATH`'e eklemiş oluyoruz. Böylece, `my_scripts` dizinini de sistem çalıştırılabilir dosyaları ararken kontrol edecektir.

Yeni dizinin `PATH`'e eklendiğini doğrulamak için şu komutu kullanın:

```bash
echo $PATH
```


Bu komut, güncel `PATH` değerini ekranda gösterecektir. `:/home/kullanici_adiniz/my_scripts` yolunu `PATH`'in sonunda görebilmelisiniz.

Bu işlemi test etmek için, yeni dizinimizde basit bir script oluşturalım:

```bash
echo '#!/bin/bash
echo "Özel scriptimden merhaba!"' > ~/my_scripts/hello.sh
```


Bu komut, `my_scripts` dizininde `hello.sh` adında bir dosya oluşturur ve içerisine bir script ekler. Bu script çalıştırıldığında `"Özel scriptimden merhaba!"` mesajını ekrana yazdıracaktır.

Oluşturduğumuz scripti çalıştırılabilir hale getirelim:

```bash
chmod +x ~/my_scripts/hello.sh
```


Bu komut, `hello.sh` scriptini çalıştırılabilir (executable) yapar, böylece terminalde bu scripti doğrudan çalıştırabilirsiniz.

Şimdi, bu scripti herhangi bir dizinden sadece adını yazarak çalıştırabilmelisiniz:

```bash
hello.sh
```


Eğer her şey doğru çalıştıysa, `"Özel scriptimden merhaba!"` mesajını görmelisiniz.

Bu, `my_scripts` dizinini `PATH`'e eklememiz sayesinde çalışıyor. Bir komut yazdığınızda, kabuk o komut için çalıştırılabilir bir dosyayı `PATH`'de listelenen dizinler içinde arar. Biz de `my_scripts` dizinini `PATH`'e ekleyerek kabuğa bu dizinde de arama yapması gerektiğini söyledik.

Bunu göstermek için farklı bir dizine geçin ve scripti tekrar çalıştırın:

```bash
cd /tmp
hello.sh
```
