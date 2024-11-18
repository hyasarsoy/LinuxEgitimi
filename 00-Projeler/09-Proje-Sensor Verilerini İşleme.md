```markdown
# **Sensor Verilerini İşleme**

Bu projede, sensör verilerinden düşman gemi hareketlerini içeren bilgileri filtreleyecek, sıralayacak ve yinelenen kayıtları temizleyecek bir veri işleme hattı oluşturacaksınız.

---

## **Görevler**
1. **Sensör Verilerini Filtreleme:**
   - `00-Projeler/Assets/sensor_data.txt` dosyasından gereksiz log girdilerini filtreleyin.
   - Sadece `"Detected enemy vessel"` içeren satırları tutun.

2. **Zaman Damgasına Göre Sıralama:**
   - Filtrelenen girdileri zaman damgasına (ilk alan) göre artan sırada sıralayın.

3. **Yinelenen Kayıtları Kaldırma:**
   - Aynı olan satırları kaldırarak yalnızca benzersiz kayıtları bırakın.

4. **Sonuçları Kaydetme:**
   - İşlenmiş verileri `processed_sensor_data.txt` dosyasına kaydedin.

---

## **Gereksinimler**
- Veriler `00-Projeler/Assets/sensor_data.txt` dosyasından okunmalıdır.
- Nihai işlenmiş veriler `processed_sensor_data.txt` dosyasına kaydedilmelidir.

---

## **Örnek**
Son işlenmiş dosya olan **processed_sensor_data.txt** şu şekilde görünmelidir:

```plaintext
0300h - Detected enemy vessel at sector E5
0420h - Detected enemy vessel at sector A2
0510h - Detected enemy vessel at sector D4
...
...
2338h - Detected enemy vessel at sector R1
2349h - Detected enemy vessel at sector Z8
2358h - Detected enemy vessel at sector D3
```
```

