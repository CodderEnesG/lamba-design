# Figma Make istemleri

Kredi ziyan olmasın diye sıra: önce tasarım sistemi ve tek ana ekran, beğenilince diğer ekranlar aynı
sistemle. Temel değişirse tüm ekranları baştan yaptırmak gerekir.

## 1. istem: tasarım sistemi + Bugün ekranı

```text
Sen "lamba" adlı bir mobil uygulamanın arayüzünü tasarlıyorsun. Bağlı GitHub reposu yalnız tasarım
içindir; uygulama kodu yok. Kod yazmaya, backend, API ya da veritabanı kurmaya çalışma. Odak: görsel
tasarım ve tıklanabilir prototip.

Önce şu dosyaları sırayla oku ve onlara sadık kal:
1. README.md
2. DESIGN-BRIEF.md (ürün, kullanıcılar, günlük döngü, ton)
3. SCREENS.md (ekranlar, gerçek Türkçe metinler, durumlar)
4. UI-RULES.md (değişmez kurallar; bunları asla çiğneme)
5. TOKENS.md (renk adları)
6. brand/kilavuz/lamba-marka-kilavuzu.html (marka kılavuzu)

Marka kuralları (kılavuzdan, kısaca):
- Palet yalnız: gece moru #1C1330, krem #F6EEE0, turuncu #FF9F43 (oran ≈ 60/30/10) ve kılavuzdaki
  destek tonları. Yeşil, kırmızı, sarı yok; doğru/yanlış/uyarı ikon, şekil ve metinle gösterilir.
  Gradyan yok. Turuncu krem zeminde yazı ya da çizgi olmaz.
- Başlıklar Bricolage Grotesque, metin ve butonlar Source Sans 3. Marka adı hep küçük harf: lamba.
- Logo, duman durumları, Alaaddin ifadeleri ve sahneler brand/ klasöründe hazır; yeniden çizme,
  renklendirme, esnetme. Ekranda en fazla bir Alaaddin.

Bu ilk adımda yalnız şunları yap:

A) Tasarım sistemi (koyu tema ana kimlik, açık tema karşılığıyla):
   - Renk ve yazı ölçeği, boşluk ve köşe yarıçapı
   - Butonlar: birincil (tek ana eylem, turuncu), ikincil, sessiz ve tehlikeli eylem (kırmızı
     kullanmadan; ikon, çerçeve ve metinle)
   - Seçim çipi, metin ve sayı girişi, bant (bilgi, güvenli mod, onay bekleniyor), boş durum, hata
     durumu, yükleme ("düşünüyor" Alaaddin)
   - Görev kartı varyantları: kitap (sayfa, test) ve YouTube videosu; planlı / tamamlandı / yarım /
     yapılmadı durumları ve kart içi check-in düğmeleri ("Yaptım", "Yarım kaldı", "Yapamadım";
     video için "İzledim", "İzleyemedim")
   - Alt sekme çubuğu: Bugün, Kütüphane, Koç, Ayarlar

B) "Bugün" ekranı (SCREENS.md bölüm 2.1), iPhone boyutunda (390 × 844), koyu ve açık temada şu
   durumlarla:
   1. Yeni kullanıcı, kitap yok (boş plan sahnesi)
   2. Normal gün: 2 kitap kartı + 1 YouTube video kartı, hiçbiri işaretlenmemiş
   3. Akşam: kartlar işaretlenmiş (biri tamamlandı, biri yarım, biri yapılmadı) + doğru/yanlış formu
   4. Güvenli mod açık (hafif mod bandı, yumuşak görünüm)
   5. Gün tamam (gün tamam sahnesi, "yanık" duman)
   Metinleri SCREENS.md'den aynen kullan; örnek içerik uydurma ama gerçekçi olsun
   ("3 Adım TYT Tarih · s. 41-58 · ≈ 50 dk", "Sınava 235 gün", "Seri: 6 gün").

Kurallar:
- YouTube kartında "YouTube" kaynak etiketi ve kanal adı görünür kalır; video uygulama içinde oynatılmaz,
  yalnız "YouTube'da aç" düğmesi var.
- Ton yargısız: "yapılmadı" durumu suçlayıcı görünmez, kırmızı ya da ünlem yok.
- Dokunma alanları en az 44 pt; uzun Türkçe kelimeler taşmaz.

Bitirince kısaca yaz: hangi tasarım kararlarını verdin, duman durumlarını ve Alaaddin'i Bugün
ekranında nasıl kullandın, belgelerde belirsiz kalan ya da karar gerektiren neler var.
```

## Sonraki istemler (sırayla, her biri ayrı)

2. Aynı tasarım sistemiyle SCREENS.md bölüm 1'deki kurulum ekranlarını (8 ekran) tasarla. Karşılama
   ekranında karşılama sahnesini kullan.
3. Bölüm 2.2 Kütüphane ve bölüm 3'teki kaynak ekleme ekranlarını tasarla (barkod, arama, hızlı ekle,
   içindekiler, YouTube listesi).
4. Bölüm 2.3 Koç (sohbet) ve bölüm 6 Destek ekranlarını tasarla. Akut risk yanıtı ve Destek ekranı sakin,
   net ve büyük arama düğmeleriyle olsun; UI-RULES'taki kriz kurallarına uy.
5. Bölüm 4 check-in ve bölüm 2.4 Ayarlar, bölüm 5 hesap ve veli onayı ekranlarını tasarla; 18 yaş altı
   kilitli durumlarını da göster.
6. Bölüm 7'deki veli web sayfalarını (onay ve haftalık rapor) mobil tarayıcı için tasarla.

## Not

Figma soru sorarsa ya da belirsizlik bildirirse yanıtları ana repoya (PROJECT-STATE) taşınır; bazıları
ürün kararıdır (tehlikeli eylemlerin dili, Gölge modu, duman durumlarının anlamı).
