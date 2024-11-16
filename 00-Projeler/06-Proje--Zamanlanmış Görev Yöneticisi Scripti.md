# **Zamanlanmış Görev Yöneticisi Scripti**

Bu proje, kullanıcıların **cron** görevlerini kolayca görüntüleyebileceği, ekleyebileceği veya kaldırabileceği bir Bash betiğinden oluşur. Betik, kullanıcı dostu bir menü aracılığıyla **zamanlanmış görevlerin yönetilmesini** sağlar.

---

## **Proje Yapısı**

- **`task_scheduler.sh`**: Zamanlanmış görevlerin yönetimi için ana Bash betiği.
- **Özellikler**:
  - **Listeleme**: Mevcut zamanlanmış görevleri görüntüler.
  - **Ekleme**: Yeni bir görev eklemenize olanak tanır.
  - **Silme**: Belirtilen bir görevi kaldırır.
  - **Çıkış**: Programı sonlandırır.

---

## **Kurulum ve Kullanım**

### 1. **Betik Dosyasını Oluşturma**
Bir dosya oluşturun ve aşağıdaki Bash kodunu içine yapıştırın:

```bash
#!/bin/bash

# Zamanlanmış görevleri listeleme fonksiyonu
listele_gorevler() {
  echo "Zamanlanmış Görevler:"
  crontab -l
  echo
}

# Yeni görev ekleme fonksiyonu
ekle_gorev() {
  read -p "Çalıştırılacak komut veya betiği girin: " komut
  read -p "Zamanlama türünü seçin (saatlik, günlük, haftalık): " zamanlama
  read -p "Ek parametreler varsa girin: " parametreler

  case $zamanlama in
    saatlik)
      cron_zaman="0 * * * *"
      ;;
    günlük)
      cron_zaman="0 0 * * *"
      ;;
    haftalık)
      cron_zaman="0 0 * * 0"
      ;;
    *)
      echo "Geçersiz zamanlama türü. Lütfen saatlik, günlük veya haftalık seçin."
      return
      ;;
  esac

  # Görevi crontab'a ekleme
  (
    crontab -l 2> /dev/null
    echo "$cron_zaman $komut $parametreler"
  ) | crontab -

  echo "Görev başarıyla zamanlandı."
  echo
}

# Görev kaldırma fonksiyonu
sil_gorev() {
  read -p "Kaldırılacak komut veya betiği girin: " komut

  # Görevi crontab'dan kaldırma
  crontab -l | grep -v "$komut" | crontab -

  echo "Görev başarıyla kaldırıldı."
  echo
}

# Ana menü döngüsü
while true; do
  echo "Görev Yöneticisi"
  echo "1. Zamanlanmış görevleri listele"
  echo "2. Görev ekle"
  echo "3. Görev kaldır"
  echo "4. Çıkış"
  read -p "Seçiminizi girin: " secim
  echo

  case $secim in
    1)
      listele_gorevler
      ;;
    2)
      ekle_gorev
      ;;
    3)
      sil_gorev
      ;;
    4)
      break
      ;;
    *)
      echo "Geçersiz seçim. Lütfen tekrar deneyin."
      echo
      ;;
  esac
done
```

---

## **Kurulum Adımları**

### 1. **Çalıştırma İzni Verme**
Betik dosyasına çalıştırma izni vermek için şu komutu çalıştırın:
```bash
chmod +x task_scheduler.sh
```

### 2. **Betiği Çalıştırma**
Betiği çalıştırmak için:
```bash
./task_scheduler.sh
```

---

## **Kullanıcı Arayüzü**

Betik çalıştırıldığında aşağıdaki menü görüntülenir:

```
Görev Yöneticisi
1. Zamanlanmış görevleri listele
2. Görev ekle
3. Görev kaldır
4. Çıkış
```

### Kullanıcı Seçenekleri:

#### **1. Zamanlanmış Görevleri Listele**
Mevcut görevleri listeler. Örneğin:
```
Zamanlanmış Görevler:
0 0 * * * /usr/bin/ornek_script
```

#### **2. Görev Ekle**
Kullanıcıdan zamanlama türü ve komut bilgisi alır ve crontab’a ekler.

#### **3. Görev Kaldır**
Belirtilen komutu arar ve zamanlanmış görevlerden kaldırır.

#### **4. Çıkış**
Menüden çıkışı sağlar.

---

## **Proje Özellikleri**

| **Özellik**        | **Açıklama**                                                    |
|---------------------|----------------------------------------------------------------|
| Zamanlanmış Görevler | Mevcut görevleri listeleme                                     |
| Görev Ekleme        | Saatlik, günlük veya haftalık olarak yeni bir görev ekleme     |
| Görev Kaldırma      | Belirtilen komutun zamanlanmış görevlerden kaldırılması        |
| Çıkış               | Programı güvenli bir şekilde kapatma                           |

Herhangi bir sorun yaşarsanız, sormaktan çekinmeyin! 😊
