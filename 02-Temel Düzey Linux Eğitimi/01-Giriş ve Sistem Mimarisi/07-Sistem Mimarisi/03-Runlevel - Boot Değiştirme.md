
# Runlevel / Boot Hedeflerini Değiştirme ve Sistemi Kapatma veya Yeniden Başlatma

## 1. Runlevel Nedir?

Runlevel, bir Unix veya Linux tabanlı işletim sisteminde belirli bir çalışma seviyesini temsil eder. Her runlevel, sistemin hangi servislerin ve işlemlerin çalışacağını belirler. Modern Linux dağıtımlarında **systemd** kullanılmasına rağmen, runlevel mantığı hala geçerlidir.

### Temel Runlevel Değerleri:

1. **0** - Sistem kapalı (shutdown).
2. **1** - Tek kullanıcı modu (genellikle sistem kurtarma için).
3. **2** - Çok kullanıcılı mod, ağ desteği olmadan.
4. **3** - Çok kullanıcılı mod, ağ desteği ile (grafik arayüz olmadan).
5. **4** - Boş (kullanılmayan özel runlevel).
6. **5** - Grafik arayüz (GUI) modu.
7. **6** - Sistemi yeniden başlatma (reboot).

## 2. Runlevel / Boot Hedeflerini Değiştirme

Modern Linux dağıtımlarında **systemd** kullanıldığı için runlevel yerine **target** kavramı kullanılır. Systemd'de runlevel karşılıkları şu şekildedir:

- **runlevel 0**: `poweroff.target`
- **runlevel 1**: `rescue.target`
- **runlevel 3**: `multi-user.target`
- **runlevel 5**: `graphical.target`
- **runlevel 6**: `reboot.target`

### Runlevel Değiştirme

#### 1. `systemctl` Komutu ile Runlevel Değiştirme
Systemd ile hedef değiştirmek için `systemctl` komutu kullanılır.

- Tek kullanıcı moduna geçmek için (kurtarma modu):
  ```bash
  sudo systemctl isolate rescue.target
  ```

- Çok kullanıcılı ağ moduna geçmek için:
  ```bash
  sudo systemctl isolate multi-user.target
  ```

- Grafik arayüze geçmek için:
  ```bash
  sudo systemctl isolate graphical.target
  ```

### Geçerli Runlevel Görüntüleme

Sistemin mevcut çalışma seviyesini öğrenmek için:
```bash
runlevel
```

## 3. Sistemi Kapatma ve Yeniden Başlatma

### Sistemi Kapatma

Sistemi kapatmak için aşağıdaki komutlar kullanılabilir:

- **shutdown** komutu ile:
  ```bash
  sudo shutdown now
  ```

- **poweroff** komutu ile:
  ```bash
  sudo poweroff
  ```

- **halt** komutu ile:
  ```bash
  sudo halt
  ```

### Sistemi Yeniden Başlatma

Sistemi yeniden başlatmak için:

- **reboot** komutu ile:
  ```bash
  sudo reboot
  ```

- **shutdown** komutu ile yeniden başlatmak:
  ```bash
  sudo shutdown -r now
  ```

## 4. Runlevel ve Hedefler Arasındaki Farklar

- **Runlevel**: Klasik Unix/Linux sistemlerinde kullanılır. Örneğin, `runlevel 3` ağ ile çok kullanıcılı modu ifade eder.
- **Target**: Systemd ile birlikte gelen daha modern bir kavramdır ve daha esnektir. `multi-user.target`, runlevel 3'e eşdeğerdir.


