#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <time.h>
#include <ctype.h>
#include <unistd.h>  // sleep fonksiyonu için (Linux/macOS)

#define MAX_INPUT 256
#define MAX_NOT 1024

// Metindeki sondaki '\n' karakterini kaldırır
void satirSonuTemizle(char *str) {
    size_t len = strlen(str);
    if (len > 0 && str[len - 1] == '\n') {
        str[len - 1] = '\0';
    }
}

// Metni küçük harfe çevirir
void metniKucukHarfeCevir(char *str) {
    for (int i = 0; str[i]; i++) {
        str[i] = tolower(str[i]);
    }
}

// Selam verir
void selamVer() {
    printf("Selamlar! Size nasıl yardımcı olabilirim?\n");
}

// Nasılsın sorusuna cevap verir
void nasilOldugumuSoyle() {
    printf("İyiyim, teşekkürler. Siz nasılsınız?\n");
}

// 1-100 arası rastgele sayı üretir
void rastgeleSayiUret() {
    int sayi = rand() % 100 + 1;
    printf("Rastgele sayı: %d\n", sayi);
}

// Basit dört işlem hesap makinesi
void basitHesapMakinesi() {
    char islem;
    double sayi1, sayi2;

    printf("İşlem türü (+, -, *, /): ");
    scanf(" %c", &islem);
    printf("İki sayı giriniz: ");
    scanf("%lf %lf", &sayi1, &sayi2);

    switch (islem) {
        case '+': printf("Sonuç: %.2lf\n", sayi1 + sayi2); break;
        case '-': printf("Sonuç: %.2lf\n", sayi1 - sayi2); break;
        case '*': printf("Sonuç: %.2lf\n", sayi1 * sayi2); break;
        case '/': 
            if (sayi2 == 0) printf("Hata: Sıfıra bölünemez.\n");
            else printf("Sonuç: %.2lf\n", sayi1 / sayi2);
            break;
        default:
            printf("Geçersiz işlem.\n");
    }
    while(getchar() != '\n'); // tamponu temizle
}

// Bugünün tarihini gösterir
void bugununTarihiniGoster() {
    time_t suan = time(NULL);
    struct tm *t = localtime(&suan);
    printf("Bugünün tarihi: %04d-%02d-%02d\n", t->tm_year + 1900, t->tm_mon + 1, t->tm_mday);
}

// Şu anki saati gösterir
void suankiSaatiGoster() {
    time_t suan = time(NULL);
    struct tm *t = localtime(&suan);
    printf("Şu an saat: %02d:%02d:%02d\n", t->tm_hour, t->tm_min, t->tm_sec);
}

// Komut listesini yazdırır
void komutlariGoster() {
    printf("Kullanılabilir komutlar:\n");
    printf("- merhaba\n");
    printf("- nasılsın\n");
    printf("- rastgele sayı\n");
    printf("- hesap makinesi\n");
    printf("- bugün tarih\n");
    printf("- saat kaç\n");
    printf("- şaka yap\n");
    printf("- dosya aç [dosyaadı]\n");
    printf("- dosya oluştur [dosyaadı]\n");
    printf("- dosya yaz [dosyaadı]\n");
    printf("- dosya sil [dosyaadı]\n");
    printf("- dosya satır oku [dosyaadı] [satırno]\n");
    printf("- sayı tahmin et\n");
    printf("- şifre oluştur\n");
    printf("- not tut\n");
    printf("- hafıza temizle\n");
    printf("- geri sayım başlat [saniye]\n");
    printf("- çıkış\n");
}

// Rastgele şaka yapar
void sakaYap() {
    const char *sakalar[] = {
        "Bilgisayarım ısınınca terliyor!",
        "Kütüphanede kitaplar sessizce konuşuyor.",
        "Fare neden bilgisayarın yanında koşuyor? Çünkü fare tıklıyor!",
        "Programcılar neden denize gitmez? Çünkü sürekli hata yaparlar!",
        "Klavyeyle aram iyidir, hep bana tuş basar."
    };
    int idx = rand() % (sizeof(sakalar)/sizeof(sakalar[0]));
    printf("%s\n", sakalar[idx]);
}

// Dosyanın içeriğini ekrana yazdırır
void dosyaAc(const char *dosyaAdi) {
    FILE *dosya = fopen(dosyaAdi, "r");
    if (!dosya) {
        printf("Dosya açılamadı: %s\n", dosyaAdi);
        return;
    }
    char satir[256];
    printf("%s dosyasının içeriği:\n", dosyaAdi);
    while(fgets(satir, sizeof(satir), dosya)) {
        printf("%s", satir);
    }
    fclose(dosya);
}

// Boş dosya oluşturur
void dosyaOlustur(const char *dosyaAdi) {
    FILE *dosya = fopen(dosyaAdi, "w");
    if (!dosya) {
        printf("Dosya oluşturulamadı: %s\n", dosyaAdi);
        return;
    }
    fclose(dosya);
    printf("Dosya oluşturuldu: %s\n", dosyaAdi);
}

// Dosyaya satır ekler
void dosyayaYaz(const char *dosyaAdi) {
    char metin[256];
    printf("Dosyaya eklenecek metni yazın: ");
    fgets(metin, sizeof(metin), stdin);
    satirSonuTemizle(metin);

    FILE *dosya = fopen(dosyaAdi, "a");
    if (!dosya) {
        printf("Dosya açılamadı: %s\n", dosyaAdi);
        return;
    }
    fprintf(dosya, "%s\n", metin);
    fclose(dosya);
    printf("Metin dosyaya eklendi.\n");
}

// Dosyayı siler
void dosyaSil(const char *dosyaAdi) {
    if(remove(dosyaAdi) == 0) {
        printf("Dosya silindi: %s\n", dosyaAdi);
    } else {
        printf("Dosya silinemedi veya bulunamadı: %s\n", dosyaAdi);
    }
}

// Dosyadan istenilen satırı okur
void dosyadanSatirOku(const char *dosyaAdi, int satirNo) {
    if (satirNo <= 0) {
        printf("Geçersiz satır numarası.\n");
        return;
    }
    FILE *dosya = fopen(dosyaAdi, "r");
    if (!dosya) {
        printf("Dosya açılamadı: %s\n", dosyaAdi);
        return;
    }
    char satir[256];
    int sayac = 0;
    while (fgets(satir, sizeof(satir), dosya)) {
        sayac++;
        if (sayac == satirNo) {
            printf("%d. satır: %s", satirNo, satir);
            fclose(dosya);
            return;
        }
    }
    printf("Dosyada %d. satır bulunamadı.\n", satirNo);
    fclose(dosya);
}

// Sayı tahmin oyunu
void sayiTahminOyunu() {
    int hedef = rand() % 100 + 1;
    int tahmin, sayac = 0;
    printf("1 ile 100 arasında bir sayı tuttum, tahmin et!\n");

    while(1) {
        printf("Tahmininiz: ");
        if(scanf("%d", &tahmin) != 1) {
            printf("Geçersiz giriş!\n");
            while(getchar() != '\n');
            continue;
        }
        sayac++;
        if(tahmin < hedef) {
            printf("Daha yüksek bir sayı söyleyin.\n");
        }
        else if(tahmin > hedef) {
            printf("Daha düşük bir sayı söyleyin.\n");
        }
        else {
            printf("Tebrikler! %d denemede bildiniz.\n", sayac);
            break;
        }
    }
    while(getchar() != '\n');
}

// Rastgele 12 karakterli şifre üretir
void sifreOlustur() {
    const char charset[] = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789!@#$%^&*";
    char sifre[13];
    for (int i=0; i<12; i++) {
        sifre[i] = charset[rand() % (sizeof(charset)-1)];
    }
    sifre[12] = '\0';
    printf("Oluşturulan şifre: %s\n", sifre);
}

// Hafıza temizleme simülasyonu
void hafizaTemizle() {
    printf("Hafıza temizlendi (simülasyon).\n");
}

// Geri sayım başlatır (saniye cinsinden)
void geriSayimBaslat(int saniye) {
    if (saniye <= 0) {
        printf("Geçersiz süre.\n");
        return;
    }
    printf("Geri sayım başladı: %d saniye\n", saniye);
    for (int i = saniye; i > 0; i--) {
        printf("%d...\n", i);
        sleep(1);
    }
    printf("Süre doldu!\n");
}

// Not tutma: kullanıcının notunu "notlar.txt" dosyasına ekler
void notTut() {
    char notMetni[MAX_NOT];
    printf("Notunuzu girin: ");
    fgets(notMetni, sizeof(notMetni), stdin);
    satirSonuTemizle(notMetni);

    FILE *dosya = fopen("notlar.txt", "a");
    if (!dosya) {
        printf("Not dosyası açılamadı.\n");
        return;
    }
    fprintf(dosya, "%s\n", notMetni);
    fclose(dosya);
    printf("Not kaydedildi.\n");
}

// Programdan çıkış yapar
void cikisYap() {
    printf("Programdan çıkılıyor, iyi günler!\n");
    exit(0);
}

int main() {
    srand(time(NULL));

    char girilen[MAX_INPUT];

    printf("Sanal Asistan'a hoş geldiniz! Yardım için 'yardım' yazabilirsiniz.\n");

    while(1) {
        printf("\nKomut: ");
        if (!fgets(girilen, sizeof(girilen), stdin)) {
            printf("Girdi alınamadı, çıkılıyor.\n");
            break;
        }
        satirSonuTemizle(girilen);
        metniKucukHarfeCevir(girilen);

        if (strcmp(girilen, "merhaba") == 0) {
            selamVer();
        } 
        else if (strcmp(girilen, "nasılsın") == 0) {
            nasilOldugumuSoyle();
        }
        else if (strcmp(girilen, "rastgele sayı") == 0) {
            rastgeleSayiUret();
        }
        else if (strcmp(girilen, "hesap makinesi") == 0) {
            basitHesapMakinesi();
        }
        else if (strcmp(girilen, "bugün tarih") == 0) {
            bugununTarihiniGoster();
        }
        else if (strcmp(girilen, "saat kaç") == 0) {
            suankiSaatiGoster();
        }
        else if (strcmp(girilen, "şaka yap") == 0) {
            sakaYap();
        }
        else if (strncmp(girilen, "dosya aç ", 9) == 0) {
            dosyaAc(girilen + 9);
        }
        else if (strncmp(girilen, "dosya oluştur ", 14) == 0) {
            dosyaOlustur(girilen + 14);
        }
        else if (strncmp(girilen, "dosya yaz ", 10) == 0) {
            dosyayaYaz(girilen + 10);
        }
        else if (strncmp(girilen, "dosya sil ", 10) == 0) {
            dosyaSil(girilen + 10);
        }
        else if (strncmp(girilen, "dosya satır oku ", 16) == 0) {
            char dosyaAdi[128];
            int satirNo;
            if(sscanf(girilen + 16, "%127s %d", dosyaAdi, &satirNo) == 2) {
                dosyadanSatirOku(dosyaAdi, satirNo);
            } else {
                printf("Doğru kullanım: dosya satır oku [dosyaadı] [satırno]\n");
            }
        }
        else if (strcmp(girilen, "sayı tahmin et") == 0) {
            sayiTahminOyunu();
        }
        else if (strcmp(girilen, "şifre oluştur") == 0) {
            sifreOlustur();
        }
        else if (strcmp(girilen, "not tut") == 0) {
            notTut();
        }
        else if (strcmp(girilen, "hafıza temizle") == 0) {
            hafizaTemizle();
        }
        else if (strncmp(girilen, "geri sayım başlat ", 18) == 0) {
            int saniye;
            if(sscanf(girilen + 18, "%d", &saniye) == 1) {
                geriSayimBaslat(saniye);
            } else {
                printf("Doğru kullanım: geri sayım başlat [saniye]\n");
            }
        }
        else if (strcmp(girilen, "yardım") == 0) {
            komutlariGoster();
        }
        else if (strcmp(girilen, "çıkış") == 0) {
            cikisYap();
        }
        else {
            printf("Anlamadım, lütfen başka bir komut deneyin veya 'yardım' yazın.\n");
        }
    }

    return 0;
}
