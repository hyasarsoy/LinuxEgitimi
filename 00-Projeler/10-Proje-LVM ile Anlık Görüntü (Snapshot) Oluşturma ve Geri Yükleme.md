T### **Proje: LVM ile Anlık Görüntü (Snapshot) Oluşturma ve Geri Yükleme**

#### **Proje Hedefi:**
Bu proje, Linux sisteminde **LVM (Logical Volume Manager)** kullanarak bir **anlık görüntü (snapshot)** oluşturmayı, veriyi yedeklemeyi ve gerektiğinde bu snapshot'tan geri yükleme yapmayı öğretecektir. Snapshot'lar, bir dosya sisteminin belirli bir andaki durumunun kopyalanmasına olanak tanır.

---

### **1. LVM Snapshot Oluşturma**

#### **Aşamalar:**

1. **Mevcut Mantıksal Birimi (LV) Belirleyin:**
   İlk olarak, snapshot almak istediğiniz mantıksal birimi belirlemeniz gerekmektedir. Sistemdeki mevcut mantıksal birimleri listelemek için şu komutu kullanabilirsiniz:

   ```bash
   sudo lvs
   ```

   Bu komut, mevcut mantıksal birimler ve grupları listeleyecektir.

2. **Snapshot Oluşturma:**
   Snapshot almak için `lvcreate` komutunu kullanacağız. Temel komut şu şekildedir:

   ```bash
   sudo lvcreate --size [boyut] --snapshot --name [snapshot_adı] [volume_group]/[logical_volume]
   ```

   - `--size [boyut]`: Snapshot için ayıracağınız alan (snapshot yalnızca değişiklikleri takip eder, bu yüzden genellikle küçük bir boyut yeterlidir).
   - `--name [snapshot_adı]`: Snapshot’ın adı.
   - `[volume_group]/[logical_volume]`: Snapshot almak istediğiniz mantıksal birim ve volume group (VG).

   **Örnek:**

   Eğer `vg01` volume group içinde `lv_data` adında bir mantıksal birim varsa ve 1 GB'lık bir snapshot oluşturmak istiyorsanız şu komutu kullanabilirsiniz:

   ```bash
   sudo lvcreate --size 1G --snapshot --name lv_data_snapshot vg01/lv_data
   ```

   Bu komut, `lv_data` adlı mantıksal birim için `lv_data_snapshot` adında 1 GB boyutunda bir snapshot oluşturacaktır.

3. **Snapshot’ı Kontrol Etme:**
   Snapshot’ın başarıyla oluşturulduğunu kontrol etmek için şu komutu kullanabilirsiniz:

   ```bash
   sudo lvs
   ```

   Bu komut, tüm mantıksal birimlerinizi ve snapshot'ları listeleyecektir.

---

### **2. Snapshot Kullanımı (Veri Yedekleme veya Test Amaçlı)**

Snapshot oluşturduktan sonra, bu snapshot'ı mount ederek veriye erişebilir ve yedek alabilirsiniz. Bu işlem, orijinal veriyi değiştirmeden test yapmanıza veya yedeklemenize olanak tanır.

#### **Snapshot’ı Mount Etme:**

Snapshot’ı mount etmek için şu komutu kullanabilirsiniz:

```bash
sudo mount /dev/[volume_group]/[snapshot_adı] /mnt
```

**Örnek:**
Eğer `lv_data_snapshot` adında bir snapshot’ınız varsa:

```bash
sudo mount /dev/vg01/lv_data_snapshot /mnt
```

Bu komut, `lv_data_snapshot` adlı snapshot’ı `/mnt` dizinine bağlar. Bu dizine giderek snapshot’ın içeriğini inceleyebilirsiniz.

---

### **3. Snapshot’tan Geri Yükleme (Restore Etme)**

Eğer snapshot’ı geri yüklemek isterseniz, bunun için snapshot'taki veriyi orijinal mantıksal birime kopyalamanız gerekir.

#### **Adımlar:**

1. **Snapshot’ı Unmount Etme:**
   Eğer snapshot’ı mount ettiyseniz, önce unmount etmeniz gerekir:

   ```bash
   sudo umount /mnt
   ```

2. **Snapshot’tan Veri Geri Yükleme:**
   Snapshot’tan veri geri yüklemek için `dd` komutunu kullanabilirsiniz. Bu komut, düşük seviyeli veri kopyalama yapacaktır:

   ```bash
   sudo dd if=/dev/[volume_group]/[snapshot_adı] of=/dev/[volume_group]/[logical_volume] bs=4M
   ```

   **Örnek:**
   Eğer `lv_data_snapshot` adlı snapshot’tan `lv_data` adlı mantıksal birime veri geri yüklemek istiyorsanız:

   ```bash
   sudo dd if=/dev/vg01/lv_data_snapshot of=/dev/vg01/lv_data bs=4M
   ```

   Bu komut, snapshot’taki veriyi orijinal mantıksal birime kopyalar.

3. **Veri Kontrolü:**
   Geri yükledikten sonra, verilerin doğru şekilde geri yüklendiğini kontrol edebilirsiniz.

---

### **4. Snapshot Silme (Temizleme)**

Snapshot’tan sonra artık ihtiyacınız kalmadıysa, snapshot'ı silerek sistemdeki gereksiz alanı boşaltabilirsiniz.

#### **Snapshot’ı Silme:**

```bash
sudo lvremove /dev/[volume_group]/[snapshot_adı]
```

**Örnek:**

```bash
sudo lvremove /dev/vg01/lv_data_snapshot
```

Bu komut, `lv_data_snapshot` adlı snapshot’ı siler ve bu snapshot için kullanılan alanı geri kazandırır.

---

### **5. Projede Dikkat Edilmesi Gerekenler**

- **Snapshot Boyutu:** Snapshot, orijinal mantıksal birimle tamamen aynı büyüklükte değildir. Snapshot yalnızca yapılan değişiklikleri takip eder, ancak çok fazla değişiklik yapılıyorsa snapshot boyutunu arttırmak gerekebilir.
  
- **Snapshot Performans Etkisi:** Snapshot almak, sistemi kopyalamak anlamına gelmez. Bu nedenle, çok fazla veri değişikliği yapıldığında snapshot'lar, sistem performansını etkileyebilir. Yedekleme işlemi bittikten sonra snapshot'ların silinmesi önerilir.

- **Daha Fazla Alan İçin Snapshotlar:** Eğer çok büyük bir veri değişikliği bekliyorsanız, snapshot’ınızın boyutunu yeterince büyük tutmanız önemlidir. Küçük bir snapshot boyutu, veri değişiklikleri arttıkça yetersiz kalabilir.

---

### **Proje Özeti**

1. **Snapshot Oluşturma:** `sudo lvcreate --size [boyut] --snapshot --name [snapshot_adı] [volume_group]/[logical_volume]`
2. **Snapshot’ı Mount Etme:** `sudo mount /dev/[volume_group]/[snapshot_adı] /mnt`
3. **Snapshot’tan Veri Geri Yükleme:** `sudo dd if=/dev/[volume_group]/[snapshot_adı] of=/dev/[volume_group]/[logical_volume]`
4. **Snapshot Silme:** `sudo lvremove /dev/[volume_group]/[snapshot_adı]`
