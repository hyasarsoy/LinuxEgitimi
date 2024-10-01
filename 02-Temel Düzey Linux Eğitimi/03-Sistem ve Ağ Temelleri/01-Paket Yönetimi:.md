# 01 - Paket Yönetimi

Linux'ta paket yönetimi, yazılımların yüklenmesi, kaldırılması ve güncellenmesi işlemlerini kolaylaştıran önemli bir sistem bileşenidir. Farklı Linux dağıtımları, farklı paket yönetim araçları ve sistemleri kullanır, ancak temel işlevsellik tüm sistemlerde benzerdir.

Bu bölümde, temel Linux paket yönetim sistemlerini öğreneceğiz:

- `apt`: Debian ve Ubuntu tabanlı dağıtımlarda kullanılır.
- `yum` ve `dnf`: RHEL, CentOS, Fedora tabanlı dağıtımlarda kullanılır.

---

## 1. `apt` (Advanced Packaging Tool)

### Temel `apt` Komutları

1. **Paket listelerini güncelleme:**
   ```bash
   sudo apt update
   ```
   - Bu komut, yazılım paketlerinin en güncel sürümlerinin alınması için paket listelerini günceller.

2. **Paketleri yükseltme:**
   ```bash
   sudo apt upgrade
   ```
   - Sistemdeki tüm yüklü paketlerin yeni sürümlerini indirir ve günceller.

3. **Yeni bir paket yükleme:**
   ```bash
   sudo apt install <paket_ismi>
   ```
   - Belirtilen paketi indirir ve kurar.

4. **Paket kaldırma:**
   ```bash
   sudo apt remove <paket_ismi>
   ```
   - Sistemdeki bir paketi kaldırır.

5. **Gereksiz paketleri temizleme:**
   ```bash
   sudo apt autoremove
   ```
   - Artık kullanılmayan bağımlılıkları kaldırır.

6. **Paket hakkında bilgi görüntüleme:**
   ```bash
   apt show <paket_ismi>
   ```
   - Belirtilen paket hakkında detaylı bilgi verir.

---

## 2. `yum` ve `dnf`

Red Hat tabanlı sistemlerde `yum` ve daha yeni versiyonu olan `dnf`, paket yönetimi için kullanılır.

### Temel `yum` Komutları

1. **Paket listelerini güncelleme:**
   ```bash
   sudo yum check-update
   ```
   - Yüklü paketlerin güncellemeleri olup olmadığını kontrol eder.

2. **Paketleri yükseltme:**
   ```bash
   sudo yum update
   ```
   - Sistem genelindeki tüm paketleri günceller.

3. **Yeni bir paket yükleme:**
   ```bash
   sudo yum install <paket_ismi>
   ```
   - Belirtilen paketi indirir ve kurar.

4. **Paket kaldırma:**
   ```bash
   sudo yum remove <paket_ismi>
   ```
   - Sistemdeki bir paketi kaldırır.

5. **Yüklü paketleri listeleme:**
   ```bash
   yum list installed
   ```
   - Sistemde yüklü olan tüm paketleri listeler.

6. **Paket hakkında bilgi görüntüleme:**
   ```bash
   yum info <paket_ismi>
   ```
   - Bir paket hakkında bilgi verir.

### Temel `dnf` Komutları

`dnf`, `yum`'un yerini almış modern bir paket yöneticisidir.

1. **Depo güncelleme:**
   ```bash
   sudo dnf update
   ```

2. **Yeni bir paket yükleme:**
   ```bash
   sudo dnf install <paket_ismi>
   ```

3. **Paket kaldırma:**
   ```bash
   sudo dnf remove <paket_ismi>
   ```

4. **Sistem temizleme:**
   ```bash
   sudo dnf autoremove
   ```

---

## 3. Paket Depoları ve Yazılım Kaynakları

Paket yöneticileri, yazılım paketlerini belirli depolardan indirir. Bu depolar, güvenli ve doğrulanmış yazılım kaynakları içerir. Sistem yöneticileri bu depoları yapılandırabilir ve gerektiğinde üçüncü taraf depolarını ekleyebilir.

### Depo Eklemek (Ubuntu/Debian)

1. Yeni bir depo eklemek için `add-apt-repository` komutu kullanılır:
   ```bash
   sudo add-apt-repository ppa:<depo_adı>
   ```

2. Depolar eklendikten sonra paket listeleri güncellenmelidir:
   ```bash
   sudo apt update
   ```

### Depo Eklemek (RHEL/CentOS)

1. Yeni bir depo eklemek için `yum-config-manager` komutu kullanılabilir:
   ```bash
   sudo yum-config-manager --add-repo <repo_url>
   ```

2. Daha sonra paket listeleri güncellenir:
   ```bash
   sudo yum makecache
   ```

---

## 4. Örnek Senaryolar

### Örnek 1: Apache Web Sunucusu Kurulumu

1. Ubuntu/Debian tabanlı sistemlerde:
   ```bash
   sudo apt install apache2
   ```

2. RHEL/CentOS tabanlı sistemlerde:
   ```bash
   sudo yum install httpd
   ```

### Örnek 2: Nginx Web Sunucusu Kurulumu

1. Ubuntu/Debian tabanlı sistemlerde:
   ```bash
   sudo apt install nginx
   ```

2. RHEL/CentOS tabanlı sistemlerde:
   ```bash
   sudo yum install nginx
   ```

