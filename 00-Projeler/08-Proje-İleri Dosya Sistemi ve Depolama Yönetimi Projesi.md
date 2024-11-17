## **İleri Dosya Sistemi ve Depolama Yönetimi Projesi**

### **Proje: Yeni Disk Ekleyerek ve Dosya Sistemleri ile Çalışma**

### **Proje Hedefi**
Bu proje, öğrencilere yeni bir disk ekleme, dosya sistemini oluşturma, bağlama (mount), ve günlük kullanım için optimize etme becerilerini kazandırmayı amaçlamaktadır.

---

### **Görevler**
1. **Yeni Bir Disk Ekleyin:**
   - Sanallaştırma ortamında yeni bir disk ekleyin (örneğin 1 GB boyutunda bir disk).
   - Eklenen diski kontrol edin ve sistem tarafından tanınıp tanınmadığını doğrulayın.

2. **Dosya Sistemi Oluşturun:**
   - Yeni diskte `ext4` dosya sistemi oluşturun.
   - Dosya sistemi oluşturduktan sonra doğrulama yapın.

3. **Mount İşlemini Gerçekleştirin:**
   - Diski `/mnt/yeni_disk` dizinine bağlayın (mount).
   - Bağlama işlemini test etmek için dizin içerisine bir dosya oluşturun.

4. **Otomatik Bağlama Ayarlayın (fstab):**
   - Sistem yeniden başlatıldığında diskin otomatik olarak bağlanmasını sağlamak için `/etc/fstab` dosyasını düzenleyin.

5. **Disk Kullanımını İzleyin:**
   - Bağlanan diskin kullanımı hakkında bilgi edinin (`df -h` komutunu kullanarak).
   - `tune2fs` komutunu kullanarak dosya sistemi parametrelerini inceleyin.

6. **Performans Optimizasyonu Yapın:**
   - Dosya sistemini `noatime` seçeneği ile bağlayarak performansı artırın.
   - Optimizasyon sonrası bağlama seçeneklerini doğrulayın.

7. **Disk Bölümlendirme ve LVM Kullanımı:**
   - Eklenen diski birden fazla bölüme ayırın.
   - Bu bölümleri birleştirerek LVM (Logical Volume Manager) yapılandırması oluşturun.
   - LVM üzerine bir dosya sistemi kurup mount edin.

---

### **Gereksinimler**
- **Linux Dağıtımı:** Ubuntu, CentOS veya başka bir popüler dağıtım.
- **Sanallaştırma Ortamı:** VirtualBox, VMware, veya KVM gibi sanal makine araçları.
- **Disk Yönetimi Araçları:** `fdisk`, `mkfs`, `mount`, `blkid`, `df`, `lsblk`, `tune2fs`.

---

### **Adım Adım Çözüm**
1. **Yeni Diskin Eklenmesi ve Tanınması:**
   ```bash
   lsblk  # Sistemde mevcut diskleri kontrol edin.
   sudo fdisk /dev/sdb  # Yeni diski yapılandırın.
   ```

2. **Dosya Sistemi Oluşturma:**
   ```bash
   sudo mkfs.ext4 /dev/sdb1  # ext4 dosya sistemi oluşturun.
   ```

3. **Bağlama İşlemi:**
   ```bash
   sudo mkdir -p /mnt/yeni_disk
   sudo mount /dev/sdb1 /mnt/yeni_disk
   echo "Merhaba Linux!" > /mnt/yeni_disk/test_dosya.txt
   cat /mnt/yeni_disk/test_dosya.txt  # Bağlama işlemini doğrulayın.
   ```

4. **Fstab Düzenlemesi:**
   ```bash
   sudo blkid  # Disk UUID'sini bulun.
   sudo nano /etc/fstab
   # Aşağıdaki satırı ekleyin:
   UUID=XXXX-XXXX /mnt/yeni_disk ext4 defaults,noatime 0 2
   ```

5. **Disk Kullanımı ve Optimizasyon:**
   ```bash
   df -h  # Disk kullanımını kontrol edin.
   sudo tune2fs -l /dev/sdb1  # Dosya sistemi parametrelerini inceleyin.
   ```

6. **LVM Yapılandırması:**
   ```bash
   sudo pvcreate /dev/sdb1 /dev/sdb2  # Fiziksel birimler oluşturun.
   sudo vgcreate my_vg /dev/sdb1 /dev/sdb2  # Volume group oluşturun.
   sudo lvcreate -L 500M -n my_lv my_vg  # Logical volume oluşturun.
   sudo mkfs.ext4 /dev/my_vg/my_lv  # Dosya sistemi oluşturun.
   sudo mount /dev/my_vg/my_lv /mnt/lvm_disk
   ```

---

### **Test Senaryosu**
- Disk bağlandıktan sonra bir dosya oluşturup sistem yeniden başlatıldığında dosyanın hala erişilebilir olduğunu doğrulayın.
- LVM yapılandırmasının büyütülmesi veya küçültülmesi için testler yapın.

---

### **Çıktı Örneği**
- `/mnt/yeni_disk/test_dosya.txt` dosyasını başarıyla görüntüleyin.
- `df -h` çıktısında yeni bağlanan disk veya LVM alanını görmelisiniz.

