# lamba: tasarım çalışma alanı

**lamba**, YKS'ye hazırlanan öğrenciler için günlük plan ve koçluk uygulaması (iOS ve Android). Bu repo
yalnız **tasarım** içindir: ürünün özeti, ekranların listesi, kurallar ve marka paketi. Uygulama kodu burada
yok, olması da gerekmiyor.

## Okuma sırası

1. [DESIGN-BRIEF.md](DESIGN-BRIEF.md): ürün ne, kimin için, günlük döngü, tasarımdan beklenenler.
2. [SCREENS.md](SCREENS.md): uygulamadaki tüm ekranlar; içerik, durumlar ve gerçek metinlerle.
3. [UI-RULES.md](UI-RULES.md): değişmez ürün kuralları, marka kuralları, erişilebilirlik, teknik çerçeve.
4. [TOKENS.md](TOKENS.md): renklerin uygulamadaki anlamsal adlara eşlenmesi (öneri).
6. [FIGMA-PROMPTS.md](FIGMA-PROMPTS.md): Figma Make için sıralı istemler.
5. `brand/kilavuz/lamba-marka-kilavuzu.html`: marka kılavuzu (tarayıcıda aç). Logo, renk, yazı, duman
   durumları, Alaaddin, sahneler ve yapılmaması gerekenler.

## Marka paketi (`brand/`)

| Klasör | İçindeki |
|---|---|
| `logo/` | Yatay, dikey, simge, yazı logosu; dumanlı ve dumansız; koyu, açık, tek renk. Uygulama ikonu. SVG ve PNG. |
| `logo/parilti/` | Parıltılı lamba (yalnız özel anlar: hedef, seri, kutlama). |
| `logo/duman-durumlari/` | Lambanın beş ruh hali: yanık, sakin, soluk, titrek, kapalı (koyu ve Gölge). |
| `cizimler/renkli/` | Alaaddin'in 6 ifadesi (sakin, mutlu, düşünüyor, mola, kutlama, uyuyor) ve 8 sahne (karşılama, çalışıyor, boş plan, gün tamam, ara verdi, sınav yaklaşıyor, hata, ilerleme). Şeffaf PNG. |
| `cizimler/renkli-zeminli/` | Aynıları gece moru zeminli. |
| `cizimler/golge-modu*/` | Siyah-beyaz (Gölge modu) karşılıkları. |
| `kilavuz/` | Marka kılavuzu (HTML). |

Logoyu hazır dosyadan kullan; yeniden çizme, renklendirme, esnetme.

## Bu repoda yapılmayacaklar

- Uygulama kodu, API, veritabanı tasarımı yok. Figma Make'in ürettiği prototip kodu yalnız fikir ve görsel
  içindir; uygulamaya geliştirici tarafından işlenir.
- Kitap sayfası, soru görseli ya da gerçek öğrenci verisi kullanılmaz; örnek içerik uydurma olmalı
  (ör. "3 Adım TYT Tarih · sayfa 41-58").
- Ödeme / Premium, deneme sonucu girişi, uygulama içi video oynatıcı, sosyal paylaşım henüz yok; bunları
  tasarlamaya gerek yok (bkz. DESIGN-BRIEF).

## Senkron

Ürün kararlarının asıl yeri ana repo (`yks-ai-koc`). Ekranlar ya da kurallar değişince bu dosyalar oradan
güncellenir. Tasarım netleşince renkler, yazı ve bileşenler ana repoda uygulamanın temasına işlenir;
TOKENS.md o işin sözleşmesidir.

`screenshots/`: uygulamanın şu anki (geçici görünümlü) ekran görüntüleri buraya eklenebilir.
