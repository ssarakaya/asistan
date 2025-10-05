# 🧠 Asistan.c

**Sanal Asistan --- Komut Satırı Üzerinden Çalışan Basit Yapay Asistan**

## 📋 Proje Hakkında

`asistan.c`, C dilinde yazılmış etkileşimli bir **konsol tabanlı sanal
asistan** programıdır.\
Kullanıcıdan metin tabanlı komutlar alır ve çeşitli işlemler
gerçekleştirir --- örneğin tarih/saat gösterme, dosya işlemleri, basit
hesap makinesi, rastgele sayı veya şifre üretimi gibi.

Program tamamen **terminal (CLI)** üzerinden çalışır.

------------------------------------------------------------------------

## ⚙️ Özellikler

  ----------------------------------------------------------------------------------
  Kategori                   Komut                          Açıklama
  -------------------------- ------------------------------ ------------------------
  👋 Genel                   `merhaba`                      Asistan selam verir.

  😊 Durum                   `nasılsın`                     Asistan nasıl olduğunu
                                                            söyler.

  🎲 Oyun                    `sayı tahmin et`               1--100 arasında sayı
                                                            tahmin oyunu oynanır.

  🧮 Hesaplama               `hesap makinesi`               Dört işlem ( +, −, ×, ÷
                                                            ) hesaplama yapar.

  📅 Tarih                   `bugün tarih`                  Günün tarihini gösterir.

  ⏰ Saat                    `saat kaç`                     Şu anki saati gösterir.

  😂 Eğlence                 `şaka yap`                     Rastgele şaka üretir.

  🔑 Güvenlik                `şifre oluştur`                Rastgele 12 karakterli
                                                            şifre oluşturur.

  🗒️ Notlar                  `not tut`                      Girilen notu
                                                            `notlar.txt` dosyasına
                                                            kaydeder.

  🧹 Hafıza                  `hafıza temizle`               Hafıza temizleme
                                                            simülasyonu yapar.

  ⏳ Sayaç                   `geri sayım başlat [saniye]`   Geri sayım başlatır.

  💾 Dosya                   `dosya oluştur [ad]`           Yeni bir dosya
                                                            oluşturur.

  💾 Dosya                   `dosya aç [ad]`                Dosyanın içeriğini
                                                            ekrana yazar.

  💾 Dosya                   `dosya yaz [ad]`               Dosyaya satır ekler.

  💾 Dosya                   `dosya sil [ad]`               Dosyayı siler.

  💾 Dosya                   `dosya satır oku [ad] [no]`    Dosyadan belirtilen
                                                            satırı okur.

  🆘 Yardım                  `yardım`                       Tüm komutları listeler.

  🚪 Çıkış                   `çıkış`                        Programı sonlandırır.
  ----------------------------------------------------------------------------------

------------------------------------------------------------------------

## 🧰 Gereksinimler

-   macOS veya Linux işletim sistemi\
-   C derleyicisi (örneğin `gcc`)\
-   Terminal erişimi

------------------------------------------------------------------------

## 💻 Kurulum ve Çalıştırma

1.  Terminali aç.\

2.  Dosyanın bulunduğu dizine gir:

    ``` bash
    cd dosya_yolu
    ```

3.  Programı derle:

    ``` bash
    gcc asistan.c -o asistan
    ```

4.  Programı çalıştır:

    ``` bash
    ./asistan
    ```

------------------------------------------------------------------------

## 🧩 Örnek Kullanım

``` bash
Komut: merhaba
Selamlar! Size nasıl yardımcı olabilirim?

Komut: rastgele sayı
Rastgele sayı: 47

Komut: bugün tarih
Bugünün tarihi: 2025-10-05

Komut: dosya oluştur deneme.txt
Dosya oluşturuldu: deneme.txt

Komut: not tut
Notunuzu girin: Yarın toplantı var.
Not kaydedildi.

Komut: çıkış
Programdan çıkılıyor, iyi günler!
```

------------------------------------------------------------------------

##  Geliştirici Notları

-   Kod yapısı tamamen **modüler fonksiyonlar** halinde düzenlenmiştir.\
-   `unistd.h` kullanıldığı için Windows ortamında `sleep()` fonksiyonu
    uyumsuz olabilir.\
    \> Windows için `Sleep()` (ms cinsinden) fonksiyonu
    kullanılmalıdır.\
-   Türkçe karakterler terminalin kodlamasına göre bozulabilir; UTF-8
    tercih edilir.

