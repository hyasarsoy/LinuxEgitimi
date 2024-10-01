# 03 - SSH ile Uzak Bağlantılar

SSH (Secure Shell), Linux ve diğer işletim sistemlerinde uzak sistemlere güvenli bir şekilde bağlanmak ve yönetmek için kullanılan bir protokoldür. SSH, özellikle güvenli olmayan ağlar üzerinden iletişim kurarken, verileri şifreleyerek güvenli bir kanal sağlar. 

---

## 1. SSH Nedir?

SSH, ağ üzerinden güvenli veri iletimi sağlamak için şifreleme teknikleri kullanan bir protokoldür. SSH, yaygın olarak sistem yöneticileri ve geliştiriciler tarafından sunuculara erişmek, komutlar çalıştırmak, dosya aktarmak ve yönetimsel işlemler yapmak için kullanılır.

---

## 2. SSH Bağlantısı Nasıl Yapılır?

### 2.1 SSH Sunucusu Kurulumu

Linux sistemlerinde SSH sunucusu genellikle varsayılan olarak kuruludur, ancak kurulu değilse aşağıdaki adımlarla SSH sunucusunu yükleyebilirsiniz:

#### Debian/Ubuntu:
```bash
sudo apt update
sudo apt install openssh-server
```

#### CentOS/Fedora/RHEL:
```bash
sudo yum install openssh-server
sudo systemctl enable sshd
sudo systemctl start sshd
```

SSH sunucusunun çalıştığını kontrol etmek için:
```bash
sudo systemctl status sshd
```

### 2.2 SSH ile Bağlanma

SSH kullanarak uzak bir makineye bağlanmak için aşağıdaki komut kullanılır:
```bash
ssh kullanıcıadı@sunucu_ip_adresi
```

Örnek:
```bash
ssh root@192.168.1.100
```

İlk kez bağlanırken, sunucunun kimliğini doğrulamak için bir güvenlik uyarısı alırsınız. "yes" yazarak bağlantıyı kabul edebilirsiniz. Ardından, uzak makinedeki kullanıcı parolasını girerek oturum açabilirsiniz.

---

## 3. SSH Yapılandırma

SSH yapılandırma dosyası `/etc/ssh/sshd_config` dosyasındadır. Bu dosyada, SSH bağlantılarının nasıl yapılandırılacağını kontrol eden birçok seçenek bulunur.

### 3.1 SSH Portunu Değiştirme

Varsayılan olarak SSH 22 numaralı portu kullanır. Güvenlik için SSH portunu değiştirebilirsiniz.

1. SSH yapılandırma dosyasını açın:
   ```bash
   sudo nano /etc/ssh/sshd_config
   ```

2. `Port 22` satırını bulun ve istediğiniz port numarası ile değiştirin:
   ```bash
   Port 2222
   ```

3. Değişiklikleri kaydedin ve SSH servisini yeniden başlatın:
   ```bash
   sudo systemctl restart sshd
   ```

### 3.2 SSH Root Girişi Kısıtlama

Güvenliği artırmak için doğrudan root kullanıcıyla SSH bağlantısını kısıtlamak iyi bir uygulamadır.

1. `/etc/ssh/sshd_config` dosyasını düzenleyin:
   ```bash
   sudo nano /etc/ssh/sshd_config
   ```

2. `PermitRootLogin` ayarını bulun ve şu şekilde değiştirin:
   ```bash
   PermitRootLogin no
   ```

3. Değişiklikleri kaydedin ve SSH servisini yeniden başlatın:
   ```bash
   sudo systemctl restart sshd
   ```

### 3.3 Parola Doğrulamasını Devre Dışı Bırakma

SSH anahtar çiftleri kullanarak daha güvenli bir doğrulama yöntemi kullanmak için parola doğrulamasını devre dışı bırakabilirsiniz.

1. SSH yapılandırma dosyasını düzenleyin:
   ```bash
   sudo nano /etc/ssh/sshd_config
   ```

2. Aşağıdaki satırı bulup şu şekilde değiştirin:
   ```bash
   PasswordAuthentication no
   ```

3. Değişiklikleri kaydedip SSH servisini yeniden başlatın:
   ```bash
   sudo systemctl restart sshd
   ```

---

## 4. SSH Anahtar Doğrulama

Parola doğrulaması yerine SSH anahtar çiftleri kullanarak daha güvenli bir doğrulama yöntemi kullanabilirsiniz.

### 4.1 SSH Anahtarı Oluşturma

1. SSH anahtarı oluşturmak için şu komutu kullanın:
   ```bash
   ssh-keygen -t rsa -b 4096
   ```

2. Varsayılan konuma kaydedin ve bir parola belirleyin (boş bırakabilirsiniz).

### 4.2 Anahtarı Uzak Sunucuya Kopyalama

Anahtarı uzak sunucuya kopyalamak için `ssh-copy-id` komutunu kullanabilirsiniz:
```bash
ssh-copy-id kullanıcıadı@sunucu_ip_adresi
```

Anahtar kopyalandıktan sonra, parola yerine SSH anahtarınız ile giriş yapabilirsiniz.

---

## 5. Dosya Aktarımı: SCP ve SFTP

### 5.1 SCP (Secure Copy)

SCP, SSH protokolü üzerinden dosya kopyalamak için kullanılır.

- Uzak sunucuya dosya kopyalamak:
  ```bash
  scp dosyaadı kullanıcıadı@sunucu_ip_adresi:/hedef/dizin
  ```

- Uzak sunucudan dosya almak:
  ```bash
  scp kullanıcıadı@sunucu_ip_adresi:/kaynak/dosya ./hedef/dizin
  ```

### 5.2 SFTP (Secure File Transfer Protocol)

SFTP, SSH protokolü üzerinde çalışan güvenli bir dosya aktarım yöntemidir.

- SFTP oturumu başlatmak için:
  ```bash
  sftp kullanıcıadı@sunucu_ip_adresi
  ```

SFTP oturumunda `put` komutu ile dosya gönderebilir, `get` komutu ile dosya alabilirsiniz.

---

## 6. SSH ile İleri Seviye Kullanımlar

### 6.1 SSH Tünelleme

SSH tünelleme, bir ağ bağlantısını güvenli hale getirmek için kullanılır. Örneğin, bir yerel portu uzak bir makineye yönlendirebilirsiniz:
```bash
ssh -L 8080:localhost:80 kullanıcıadı@sunucu_ip_adresi
```

Bu komut, yerel makinedeki `8080` portunu uzak makinedeki `80` portuna tüneller.

### 6.2 SSH Agent Kullanımı

SSH anahtarlarını daha güvenli bir şekilde kullanmak için SSH Agent kullanılabilir. Anahtarı yükleyip oturum boyunca tekrar parola girmek zorunda kalmazsınız:
```bash
ssh-agent bash
ssh-add ~/.ssh/id_rsa
```

