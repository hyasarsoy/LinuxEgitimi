### **Sistem Günlüklerini Yedekleme**  
**Görev:** Sistem log (günlük) dizinini yedekleyin. Yedekleme dosyası tarihe göre kolayca tanımlanabilir olmalı, böylece gerektiğinde hızlı bir şekilde erişilebilir.

---

#### **Görevler**  
1. `/var/log/` dizinini yedekleyin ve sonucu `/home/halil/project/` dizinine kaydedin.  
2. Yedekleme dosyasını aşağıdaki formatta adlandırın:  
   **`yıl-ay-gün.tar.gz`**  
   Örneğin, eğer bugün **20 Şubat 2024** ise, dosya adı şu şekilde olmalı: `2024-02-20.tar.gz`.  

---

#### **Gereksinimler**  
- **`tar` Komutunu Kullanma:** Yedekleme için `tar` komutunu kullanmalısınız.  
- **Gerekli İzinler:** `/var/log/` dizinini okumak için gerekli izinlere sahip olmalısınız. Gerekirse `sudo` kullanın.  
- **Sıkıştırma:** Depolama alanından tasarruf etmek için yedekleme dosyasını sıkıştırın.  

---

#### **İpucu**  
Doğru dosya adı formatını oluşturmak için `date` komutunu kullanabilirsiniz. `date` komutu ile `+%Y-%m-%d` format dizesi, bugünün tarihini "yıl-ay-gün" formatında çıktı olarak verir.  
Örneğin:  
```bash
date +%Y-%m-%d
```
Bu komut şu şekilde bir çıktı verir:  
```
2024-02-20
```
Bu çıktıyı komut alt ifadeleri (command substitution) ile kullanarak yedekleme dosyasının adını oluşturabilirsiniz.

---

#### **Örnek**  
Yedekleme işlemini tamamladıktan sonra, proje dizininde `.tar.gz` uzantılı dosya görünecek:  

```bash
halil:project/ $ ls
2024-02-20.tar.gz
```

---

#### **Kod Örneği**
Aşağıdaki komutlar, yedekleme işlemini gerçekleştirir:  
```bash
#!/bin/bash

# Tarih formatı
backup_date=$(date +%Y-%m-%d)

# Hedef dosya adı ve dizini
backup_file="/home/halil/project/${backup_date}.tar.gz"

# Yedekleme işlemi
sudo tar -czvf "$backup_file" /var/log/
```

---

#### **Adımlar**  
1. Komut dosyasını bir dosyaya kaydedin, örneğin: `backup_logs.sh`.  
2. Çalıştırma izinlerini verin:  
   ```bash
   chmod +x backup_logs.sh
   ```
3. Scripti çalıştırarak yedeklemeyi gerçekleştirin:  
   ```bash
   ./backup_logs.sh
   ```
