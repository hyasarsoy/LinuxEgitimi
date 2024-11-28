```markdown
# **Modprobe**

---

## **1. modprobe Komutuna Giriş**
`modprobe`, Linux çekirdeğine dinamik olarak çekirdek modülleri (kernel modules) eklemek veya kaldırmak için kullanılan bir komuttur. Çekirdek modülleri, çekirdeğe eklenen veya kaldırılan işlevselliklerdir (örneğin, aygıt sürücüleri veya dosya sistemleri).

### **Temel Komutlar**
- **Modül yüklemek:**
  ```bash
  sudo modprobe <module_name>
  ```
- **Modül kaldırmak:**
  ```bash
  sudo modprobe -r <module_name>
  ```
- **Yüklü modülleri kontrol etmek:**
  ```bash
  lsmod
  ```

---

## **2. modprobe Kullanımı ve Özellikleri**

### **2.1 modprobe ile Modül Yükleme**
`modprobe`, belirtilen modülü `/lib/modules/$(uname -r)/` dizininde arar ve yüklü değilse çekirdeğe ekler.

**Örnek:**
Bir ağ kartı sürücüsü modülünü yüklemek:
```bash
sudo modprobe e1000
```

---

### **2.2 modprobe ile Modül Kaldırma**
`modprobe -r`, çekirdekten bir modülü güvenli bir şekilde kaldırır. Modül, başka modüller tarafından kullanılmıyorsa kaldırılabilir.

**Örnek:**
`e1000` modülünü kaldırmak:
```bash
sudo modprobe -r e1000
```

---

### **2.3 Modül Parametreleri**
Modüller, belirli özellikleri veya işlevleri kontrol etmek için parametreler alabilir.

**Örnek:**
Bir modülü belirli bir parametreyle yüklemek:
```bash
sudo modprobe module_name param_name=value
```

**Örnek:**
`loop` modülünü, 8 döngüsel aygıt oluşturmak için yüklemek:
```bash
sudo modprobe loop max_loop=8
```

---

### **2.4 Kalıcı Ayarlar**
Modüller ve parametrelerini kalıcı olarak yapılandırmak için `/etc/modprobe.d/` dizinindeki dosyalar kullanılır.

**Örnek:**
`/etc/modprobe.d/custom.conf` dosyasını oluşturun ve içine şu satırı ekleyin:
```plaintext
options loop max_loop=8
```

---

### **2.5 modprobe ile Hata Giderme**
**Modül hatalarını kontrol etmek:**
```bash
dmesg | grep <module_name>
```

**Örnek:**
`e1000` modülünü yüklerken hata varsa:
```bash
dmesg | grep e1000
```

---

## **3. Proje: USB Aygıt Sürücüsünü Yükleme ve Test Etme**

### **Amaç:**
Bir USB sürücüsü (`usb_storage`) modülünü yüklemek, kaldırmak ve test etmek.

### **Adımlar:**

#### **3.1 Yüklü Modülleri Kontrol Etme**
`usb_storage` modülünün yüklü olup olmadığını kontrol edin:
```bash
lsmod | grep usb_storage
```

#### **3.2 Modülü Yükleme**
USB depolama modülünü yükleyin:
```bash
sudo modprobe usb_storage
```

#### **3.3 USB Aygıtını Test Etme**
Bir USB cihazı takın ve cihazın bağlanıp bağlanmadığını kontrol edin:
```bash
dmesg | tail
```

#### **3.4 Modülü Kaldırma**
USB depolama modülünü kaldırın:
```bash
sudo modprobe -r usb_storage
```

---

## **4. Örnek Proje: Özel Bir Modül Yaratma ve Kullanma**

### **Proje: "Hello World" Modülünü Yazma**

#### **4.1 Çekirdek Modülü Oluşturma**
1. `hello_module.c` adında bir dosya oluşturun:
   ```c
   #include <linux/module.h>
   #include <linux/kernel.h>
   #include <linux/init.h>

   MODULE_LICENSE("GPL");
   MODULE_AUTHOR("Öğrenci Adı");
   MODULE_DESCRIPTION("Basit bir Hello World modülü");

   static int __init hello_init(void) {
       printk(KERN_INFO "Hello, Kernel!\n");
       return 0;
   }

   static void __exit hello_exit(void) {
       printk(KERN_INFO "Goodbye, Kernel!\n");
   }

   module_init(hello_init);
   module_exit(hello_exit);
   ```

2. Bir `Makefile` oluşturun:
   ```plaintext
   obj-m += hello_module.o

   all:
       make -C /lib/modules/$(shell uname -r)/build M=$(PWD) modules

   clean:
       make -C /lib/modules/$(shell uname -r)/build M=$(PWD) clean
   ```

3. Modülü derleyin:
   ```bash
   make
   ```

#### **4.2 Modülü Yükleme ve Kontrol Etme**
1. Modülü yükleyin:
   ```bash
   sudo insmod hello_module.ko
   ```

2. Modül mesajlarını kontrol edin:
   ```bash
   dmesg | tail
   ```

3. Modülü kaldırın:
   ```bash
   sudo rmmod hello_module
   ```


---


# **SSH**

---

## **1. SSH Nedir ve Temelleri**
Secure Shell (SSH), ağ üzerinden güvenli bir şekilde bir sunucuya erişmek ve yönetmek için kullanılan bir protokoldür. SSH, veri trafiğini şifreleyerek güvenliği sağlar.

### **Temel SSH Komutları**
- **Uzak sunucuya bağlanma:**
  ```bash
  ssh username@remote_host
  ```
- **Özel bir port üzerinden bağlanma:**
  ```bash
  ssh -p port_number username@remote_host
  ```
- **Komut çalıştırma:**
  ```bash
  ssh username@remote_host "ls -l /var/www/"
  ```

---

## **2. SSH Tünelleme**

SSH tünelleme, güvenli bir şekilde veriyi bir ağ üzerinden iletmek için kullanılan bir yöntemdir.

### **2.1 Local Port Forwarding**
Local port forwarding, yerel bir portu, uzaktaki bir sunucu üzerinden başka bir hedefe yönlendirmek için kullanılır.

**Örnek:**
- Yerel port `8080` üzerinden bir uzak web sunucusuna bağlanma:
  ```bash
  ssh -L 8080:target_server:80 username@remote_host
  ```
  - `8080`: Yerel port.
  - `target_server:80`: Hedef sunucu ve port.

**Kullanım Senaryosu:**
- Bir veri tabanına veya HTTP sunucusuna yerel erişim sağlama.

---

### **2.2 Remote Port Forwarding**
Remote port forwarding, uzak bir sunucunun portunu yerel bir port üzerinden yönlendirmek için kullanılır.

**Örnek:**
- Uzak sunucunun `8080` portunu yerel makinedeki `3000` portuna yönlendirme:
  ```bash
  ssh -R 8080:localhost:3000 username@remote_host
  ```
  - `8080`: Uzak sunucudaki port.
  - `localhost:3000`: Yerel makinedeki hedef port.

**Kullanım Senaryosu:**
- Yerel bir hizmeti (örneğin bir web sunucusu) internetteki birine erişilebilir hale getirme.

---

### **2.3 Dynamic Port Forwarding**
Dynamic port forwarding, SOCKS proxy kullanarak herhangi bir port veya hedefe dinamik bağlantılar kurar.

**Örnek:**
- Dinamik bir SOCKS proxy oluşturma:
  ```bash
  ssh -D 8080 username@remote_host
  ```
  - Tarayıcınızı bu SOCKS proxy'yi kullanacak şekilde yapılandırarak internet trafiğinizi SSH tüneli üzerinden yönlendirebilirsiniz.

**Kullanım Senaryosu:**
- İnternet trafiğini güvenli hale getirme ve coğrafi engelleri aşma.

---

## **3. Karmaşık Port Forwarding**
Karmaşık senaryolar için birden çok port yönlendirme kombinasyonu yapılabilir.

**Örnek:**
- Bir web sunucusuna erişim sağlarken aynı zamanda bir veritabanına bağlantı yönlendirme:
  ```bash
  ssh -L 8080:web_server:80 -L 3306:db_server:3306 username@remote_host
  ```

**Örnek Senaryo:**
1. Uzak bir veri tabanına bağlanırken bir web arayüzü üzerinden erişim sağlamak.
2. Özel bir ağdaki birden fazla servise aynı anda bağlanmak.

---

## **4. SSH ile Güvenlik ve Ayarlar**

### **4.1 SSH Anahtar Tabanlı Kimlik Doğrulama**
SSH anahtar çiftleri, parolalara kıyasla daha güvenli bir kimlik doğrulama yöntemidir.

#### **Adımlar:**
1. SSH anahtar çifti oluşturma:
   ```bash
   ssh-keygen -t rsa -b 4096
   ```
2. Genel anahtarı sunucuya kopyalama:
   ```bash
   ssh-copy-id username@remote_host
   ```

3. SSH bağlantısı yapma:
   ```bash
   ssh username@remote_host
   ```

---

### **4.2 SSH Konfigürasyon Dosyası**
SSH ayarlarını kolaylaştırmak için `~/.ssh/config` dosyasını kullanabilirsiniz.

**Örnek Konfigürasyon:**
```plaintext
Host myserver
    HostName 192.168.1.100
    User myuser
    Port 2222
    IdentityFile ~/.ssh/id_rsa
```

**Bağlanma:**
```bash
ssh myserver
```

---

### **4.3 Güvenliği Artırma**
- **SSH Dinleme Portunu Değiştirme:**
  `/etc/ssh/sshd_config` dosyasında şu ayarı yapın:
  ```plaintext
  Port 2222
  ```
- **Root Girişi Devre Dışı Bırakma:**
  ```plaintext
  PermitRootLogin no
  ```

- **Parola ile Girişi Devre Dışı Bırakma:**
  ```plaintext
  PasswordAuthentication no
  ```

---

## **5. Proje: SSH ile Güvenli Dosya Transferi ve Yönetimi**

### **Proje Amaçları:**
1. Uzak bir sunucuyu yönetmek.
2. Dosyaları güvenli bir şekilde transfer etmek.
3. SSH tüneli üzerinden uzak bir veritabanı bağlantısı sağlamak.

---

### **5.1 Adım 1: SSH Üzerinden Dosya Transferi**
**scp Kullanımı:**
Uzak bir sunucuya dosya gönderme:
```bash
scp local_file.txt username@remote_host:/remote/directory
```

Uzak bir sunucudan dosya alma:
```bash
scp username@remote_host:/remote/directory/remote_file.txt /local/directory
```

---

### **5.2 Adım 2: SSH Tünelleme ile Veri Tabanına Erişim**
1. Yerel makinenizi, uzak bir PostgreSQL sunucusuna bağlanmak için yapılandırın:
   ```bash
   ssh -L 5432:remote_postgres_server:5432 username@remote_host
   ```
2. Bağlantıyı test etmek için bir PostgreSQL istemcisi kullanın:
   ```bash
   psql -h localhost -U dbuser -d mydatabase
   ```

---

### **5.3 Adım 3: Sistem Yönetimi için SSH Tüneli**
1. Uzak bir web arayüzüne güvenli erişim sağlamak için local port forwarding kullanın:
   ```bash
   ssh -L 8080:web_interface_server:80 username@remote_host
   ```

2. Web tarayıcınızda `http://localhost:8080` adresini ziyaret edin.

---

