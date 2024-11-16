# **Sistem Kaynaklarını İzleme Scripti**

Bu proje, **CPU**, **bellek** ve **disk kullanımını** izleyen bir Bash betiğinden oluşmaktadır. Belirlenen eşik değerlerini aşan kaynaklar için bir uyarı mesajı görüntülenir. Betik, sürekli çalışır ve kaynak kullanımı gerçek zamanlı olarak kontrol edilir.

---

## **Proje Yapısı**

- **`monitor_system.sh`**: İzleme işlemini gerçekleştiren ana Bash betiği.
- **Eşik Değerler**:
  - **CPU Kullanımı**: %80
  - **Bellek Kullanımı**: %15
  - **Disk Kullanımı**: %80
- **Çıktı**: 
  - Terminalde kaynak kullanımını yüzdelik olarak gösterir.
  - Belirlenen eşikleri aşan kaynaklar için kırmızı renkte uyarı mesajı verir.

---

## **Kurulum ve Kullanım**

### 1. **Betik Dosyasını Oluşturma**
Bir dosya oluşturun ve aşağıdaki Bash kodunu içine yapıştırın:

```bash
#!/bin/bash

# CPU, bellek ve disk kullanımı için eşik değerleri (yüzde olarak)
CPU_ESIK=80
BELLEK_ESIK=15
DISK_ESIK=80

# Uyarı göndermek için kullanılan fonksiyon
uyari_gonder() {
  echo "$(tput setaf 1)UYARI: $1 eşik değeri aşıldı! Mevcut değer: $2%$(tput sgr0)"
}

# Sistem kaynaklarını izleyen ana fonksiyon
sistem_izle() {
  while true; do
    cpu_kullanimi=$(top -bn1 | grep "Cpu(s)" | awk '{print $2 + $4}')
    cpu_kullanimi=${cpu_kullanimi%.*} 

    bellek_kullanimi=$(free | awk '/Mem/ {printf("%3.1f", ($3/$2) * 100)}')

    disk_kullanimi=$(df -h / | awk '/\// {print $(NF-1)}')
    disk_kullanimi=${disk_kullanimi%?} 

    if ((cpu_kullanimi >= CPU_ESIK)); then
      uyari_gonder "CPU Kullanımı" "$cpu_kullanimi"
    fi

    if ((bellek_kullanimi >= BELLEK_ESIK)); then
      uyari_gonder "Bellek Kullanımı" "$bellek_kullanimi"
    fi

    if ((disk_kullanimi >= DISK_ESIK)); then
      uyari_gonder "Disk Kullanımı" "$disk_kullanimi"
    fi

    clear
    printf "%-15s %s\n" "Kaynak" "Kullanım (%)"
    echo "----------------------"
    printf "%-15s %s\n" "CPU Kullanımı" "$cpu_kullanimi"
    printf "%-15s %s\n" "Bellek Kullanımı" "$bellek_kullanimi"
    printf "%-15s %s\n" "Disk Kullanımı" "$disk_kullanimi"

    sleep 1
  done
}

sistem_izle
```

### 2. **Çalıştırma İzni Verme**
Betik dosyasına çalıştırma izni vermek için şu komutu çalıştırın:
```bash
chmod +x monitor_system.sh
```

### 3. **Betiği Çalıştırma**
Betiği çalıştırmak için şu komutu kullanabilirsiniz:
```bash
./monitor_system.sh
```

---

## **Çıktı Örneği**

Betik çalıştığında terminalde aşağıdaki gibi bir çıktı alırsınız:

```
Kaynak         Kullanım (%)
----------------------
CPU Kullanımı  45
Bellek Kullanımı 12.3
Disk Kullanımı  70
```

Eşik aşıldığında:
```
UYARI: CPU Kullanımı eşik değeri aşıldı! Mevcut değer: 85%
```

---

## **Özellikler**

- **Dinamik Güncelleme**: Her saniye sistem kaynakları yeniden kontrol edilir.
- **Renkli Uyarılar**: Eşik değerler aşıldığında kırmızı renkte uyarı gösterilir.
- **Uyarlanabilirlik**: Eşik değerleri kolayca değiştirilebilir.
