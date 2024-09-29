# Kullanıcı ve Grup Yönetimi

Linux sistemlerinde kullanıcı ve grup yönetimi, çok kullanıcılı bir ortamda yetkilendirme, güvenlik ve erişim kontrolü açısından büyük öneme sahiptir. Kullanıcı ve grupların nasıl yönetileceğini öğrenmek, sistem yöneticilerinin temel görevlerinden biridir.

## 1. Kullanıcı Yönetimi

### 1.1. Yeni Kullanıcı Oluşturma

Yeni bir kullanıcı oluşturmak için `useradd` komutu kullanılır:

```bash
sudo useradd <kullanıcı_adı>
```

Bu komut sadece kullanıcıyı oluşturur. Şifre belirlemek için şu komutu kullanabilirsiniz:

```bash
sudo passwd <kullanıcı_adı>
```

### 1.2. Kullanıcıyı Silme

Bir kullanıcıyı sistemden kaldırmak için `userdel` komutunu kullanabilirsiniz:

```bash
sudo userdel <kullanıcı_adı>
```

Eğer kullanıcının ev dizinini de silmek istiyorsanız, şu komut kullanılmalıdır:

```bash
sudo userdel -r <kullanıcı_adı>
```

### 1.3. Kullanıcı Bilgilerini Düzenleme

Var olan bir kullanıcıya ait bilgileri düzenlemek için `usermod` komutu kullanılır. Örneğin, kullanıcının varsayılan kabuğunu değiştirmek için:

```bash
sudo usermod -s /bin/bash <kullanıcı_adı>
```

### 1.4. Kullanıcı Listesini Görüntüleme

Sistemde kayıtlı tüm kullanıcıları görmek için `/etc/passwd` dosyasını inceleyebilirsiniz:

```bash
cat /etc/passwd
```

Bu dosya, her bir kullanıcının sistemde nasıl tanımlandığına dair bilgileri içerir.

## 2. Grup Yönetimi

Linux sistemlerinde gruplar, kullanıcıların dosya ve dizinler üzerinde ortak yetkilere sahip olmasını sağlar. Gruplar, kullanıcıların belirli kaynaklara erişimini yönetmek için kullanılır.

### 2.1. Yeni Grup Oluşturma

Yeni bir grup oluşturmak için `groupadd` komutunu kullanabilirsiniz:

```bash
sudo groupadd <grup_adı>
```

### 2.2. Gruba Kullanıcı Ekleme

Bir kullanıcıyı mevcut bir gruba eklemek için `usermod` komutunu kullanabilirsiniz:

```bash
sudo usermod -aG <grup_adı> <kullanıcı_adı>
```

Burada `-aG` parametresi, kullanıcıyı belirtilen gruba ekler ve var olan grup üyeliklerini korur.

### 2.3. Grup Bilgilerini Görüntüleme

Sistemde mevcut olan tüm grupları ve grup üyelerini görmek için `/etc/group` dosyasını inceleyebilirsiniz:

```bash
cat /etc/group
```

Bu dosya, sistemdeki grupların ve bu gruplara ait kullanıcıların listesini içerir.

### 2.4. Grubu Silme

Bir grubu sistemden kaldırmak için `groupdel` komutunu kullanabilirsiniz:

```bash
sudo groupdel <grup_adı>
```

## 3. Kullanıcı ve Grup İzinleri

Linux'ta her dosya ve dizin, bir kullanıcıya ve bir gruba ait olur. Dosyalar üzerinde üç tür izin vardır: okuma (r), yazma (w) ve çalıştırma (x). İzinler üç farklı kategoriye ayrılır:

- **Sahip**: Dosyanın sahibinin izinleri.
- **Grup**: Dosyanın grup üyelerinin izinleri.
- **Diğer**: Dosyaya erişimi olan diğer tüm kullanıcıların izinleri.

### 3.1. İzinleri Görüntüleme

Bir dosya veya dizinin izinlerini görmek için `ls -l` komutu kullanılır:

```bash
ls -l <dosya_adı>
```

Çıktı şu şekilde olur:

```bash
-rw-r--r-- 1 kullanıcı grup 4096 Sep 12 12:00 dosya.txt
```

Bu örnekte:

- `-rw-r--r--`: Dosyanın izinlerini gösterir.
- `kullanıcı`: Dosyanın sahibi.
- `grup`: Dosyanın grup sahibi.

### 3.2. İzinleri Değiştirme

Bir dosya veya dizinin izinlerini değiştirmek için `chmod` komutu kullanılır. Örneğin, bir dosyaya sahibine okuma ve yazma izni vermek için:

```bash
chmod u+rw <dosya_adı>
```

Gruba çalıştırma izni vermek için:

```bash
chmod g+x <dosya_adı>
```

Diğer kullanıcıların tüm izinlerini kaldırmak için:

```bash
chmod o-rwx <dosya_adı>
```

### 3.3. Sahipliği Değiştirme

Bir dosyanın sahipliğini değiştirmek için `chown` komutu kullanılır. Örneğin, bir dosyanın sahibi ve grubunu değiştirmek için:

```bash
sudo chown <yeni_sahip>:<yeni_grup> <dosya_adı>
```

## 4. Sudo Yetkilendirme

Sudo, bir kullanıcıya geçici olarak yönetici yetkileri verme işlevi görür. Bir kullanıcının `sudo` komutunu kullanabilmesi için `sudoers` dosyasına eklenmesi gerekir.

### 4.1. Kullanıcıyı Sudoers Dosyasına Ekleme

Kullanıcıyı sudo grubuna eklemek için:

```bash
sudo usermod -aG sudo <kullanıcı_adı>
```

Bu işlemden sonra, kullanıcı `sudo` komutunu kullanarak yönetici işlemleri gerçekleştirebilir.

### 4.2. Sudoers Dosyasını Düzenleme

`/etc/sudoers` dosyası, sudo yetkilerinin nasıl yönetildiğini belirler. Bu dosyayı düzenlemek için `visudo` komutu kullanılır:

```bash
sudo visudo
```

Dosyada yanlış düzenleme yapmak sistemde ciddi sorunlara yol açabilir, bu yüzden dikkatli olunmalıdır.

