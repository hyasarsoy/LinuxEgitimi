# Vim Kullanım Kılavuzu

**Vim** (Vi IMproved), Vi tabanlı güçlü ve modlu bir metin editörüdür. Bu kılavuz, Vim'in temel kullanımına, modlarına ve komutlarına dair detaylı bir rehber sunar.

---

## 1. Vim'in Modları

Vim, farklı modlarda çalışır ve her modun kendine özgü işlevi vardır. İşte temel modlar:

- **Normal Mod**: Komutları çalıştırmak için kullanılan mod. Vim açıldığında bu modda başlar.
- **Insert Mod**: Metin yazmak için kullanılan mod. Normal moddayken `i` tuşuna basarak bu moda geçebilirsiniz.
- **Visual Mod**: Metni seçmek için kullanılan mod. Seçim yaptıktan sonra üzerinde işlemler yapabilirsiniz. Normal modda `v` tuşuna basarak bu moda geçebilirsiniz.
- **Command Mod**: Dosya kaydetmek, çıkmak gibi komutları girmek için kullanılır. Normal modda `:` tuşuna basarak komut moduna geçebilirsiniz.

---

## 2. Temel Komutlar

### 2.1. Normal Mod Komutları
- **Hareket Komutları**:
  - `h`: Bir karakter sola gider.
  - `j`: Bir satır aşağı gider.
  - `k`: Bir satır yukarı gider.
  - `l`: Bir karakter sağa gider.
  - `w`: Bir sonraki kelimenin başına gider.
  - `b`: Bir önceki kelimenin başına gider.
  - `0`: Satırın başına gider.
  - `$`: Satırın sonuna gider.

- **Dosya Kaydetme ve Çıkış**:
  - `:w`: Dosyayı kaydeder.
  - `:q`: Dosyadan çıkar.
  - `:wq`: Dosyayı kaydederek çıkar.
  - `:q!`: Değişiklikleri kaydetmeden çıkar.

### 2.2. Insert Mod Komutları
- **Metin Ekleme**:
  - `i`: İmlecin bulunduğu yerden metin ekler.
  - `I`: Satırın başından metin ekler.
  - `a`: İmlecin bulunduğu yerin sağından metin ekler.
  - `A`: Satırın sonundan metin ekler.
  - `o`: Alt satıra yeni bir satır ekler.
  - `O`: Üst satıra yeni bir satır ekler.

### 2.3. Visual Mod Komutları
- **Metin Seçimi**:
  - `v`: Karakter bazlı seçim yapar.
  - `V`: Satır bazlı seçim yapar.
  - `Ctrl+v`: Blok bazlı seçim yapar.

- **Seçilen Metin Üzerinde İşlemler**:
  - `d`: Seçilen metni siler.
  - `y`: Seçilen metni kopyalar.
  - `p`: Kopyalanan veya kesilen metni yapıştırır.

---

## 3. Metin Düzenleme

### 3.1. Silme Komutları
- `x`: İmlecin üzerindeki karakteri siler.
- `dw`: İmleçten itibaren bir kelimeyi siler.
- `dd`: Satırı siler.
- `d$`: İmleçten satırın sonuna kadar siler.
- `d0`: İmleçten satırın başına kadar siler.

### 3.2. Kopyalama ve Yapıştırma Komutları
- `yy`: Satırı kopyalar.
- `y$`: İmleçten satırın sonuna kadar kopyalar.
- `p`: Kopyalanan veya kesilen metni yapıştırır.

### 3.3. Geri Alma ve Yineleme
- `u`: Son işlemi geri alır.
- `Ctrl+r`: Geri alınan işlemi tekrar eder.

---

## 4. Arama ve Değiştirme

### 4.1. Arama Yapmak
- `/kelime`: Aşağı doğru kelimeyi arar.
- `?kelime`: Yukarı doğru kelimeyi arar.
- `n`: Arama sonucunun bir sonrakine gider.
- `N`: Arama sonucunun bir öncekine gider.

### 4.2. Değiştirme
- `:%s/eski/yeni/g`: Dosya genelinde tüm "eski" ifadelerini "yeni" ile değiştirir.
- `:%s/eski/yeni/gc`: Tüm değişiklikleri onaylayarak yapar.

---

## 5. Gelişmiş Özellikler

### 5.1. Çoklu Dosya Düzenleme
- `:e filename`: Yeni bir dosya açar.
- `:bnext` veya `:bn`: Bir sonraki dosyaya geçer.
- `:bprev` veya `:bp`: Bir önceki dosyaya geçer.
- `:split filename`: Ekranı ikiye bölerek dosyayı açar.

### 5.2. Makro Kaydetme ve Kullanma
- `q<register>`: Bir makro kaydetmeye başlar (`register` a-z arası bir harf olabilir).
- Komutları girin.
- `q`: Makro kaydını durdurur.
- `@<register>`: Kaydedilen makroyu çalıştırır.

---

## 6. Dosya Gezginleri

Vim’de dosyalar arasında hızlıca geçiş yapabilir ve hatta ekranı bölebilirsiniz:
- `:vsplit filename`: Dosyayı dikey olarak ikiye böler ve iki dosya arasında çalışmanızı sağlar.
- `Ctrl+ww`: Ekranlar arasında geçiş yapar.

---

## 7. Vim'den Çıkmak

Vim'den çıkmak, özellikle yeni başlayanlar için kafa karıştırıcı olabilir. İşte birkaç çıkış yolu:
- `:q`: Dosyayı kapatır (değişiklik yoksa).
- `:q!`: Dosyadan çıkarken yapılan değişiklikleri kaydetmez.
- `:wq`: Dosyayı kaydederek kapatır.

---

## 8. .vimrc Dosyası ile Özelleştirme

Vim'in davranışlarını özelleştirmek için `~/.vimrc` dosyasını kullanabilirsiniz. Bu dosya, başlangıçta yüklenen ayarları içerir. İşte birkaç örnek:

```vim
" Satır numaralarını göster
set number

" Otomatik girinti
set autoindent

" Sürekli arama
set incsearch
```

---

## 9. Kısayollar

- **Insert moduna geçme**: `i`, `a`, `o`
- **Normal moda geçme**: `ESC`
- **Kopyalama**: `yy` (satır), `yw` (kelime)
- **Silme**: `dd` (satır), `dw` (kelime)
- **Arama**: `/kelime`, `n` (sonraki)
- **Geri alma**: `u`
- **Yineleme**: `Ctrl+r`

---

## Sonuç

Vim başlangıçta zor gelebilir, ancak öğrenildiğinde son derece hızlı ve verimli bir editördür. Bu rehber ile temel komutları öğrenerek Vim'i etkili bir şekilde kullanmaya başlayabilirsiniz. Daha ileri seviye özellikler için pratik yapmaya devam edin ve `.vimrc` dosyanızı ihtiyaçlarınıza göre düzenleyin.

```
