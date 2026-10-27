# Tasarım kararları

Figma Make çalışmasından çıkan kararlar ve açık sorular. Tasarımın her yeni adımı bunlara uyar. Ürün
kararlarının asıl kaydı ana repodaki PROJECT-STATE'tir; burası tasarım için özeti.

## Verildi (27 Ekim 2026, 1. sürüm: tasarım sistemi + Bugün)

| Konu | Karar |
|---|---|
| Ek token'lar | `control` (çerçeveli düğme ve giriş kenarı; ikincil metin rengi, çünkü çizgi rengi bilgi taşıyamaz), `emphasis` (önemli vurgu: koyuda turuncu, açıkta gece moru), `stage` (Alaaddin ve duman kutusunun zemini; her temada gece moru). TOKENS.md'ye eklendi. |
| Turuncu | Ekranda yalnız tek ana eylemde. Kart içi "Yaptım" / "İzledim" krem dolgulu ara düğme. |
| Pasif durum | Saydamlık yerine kesik çerçeve ve soluk metin. |
| Tehlikeli eylem ve hata | Kırmızı yok. Tehlikeli eylem: kalın çerçeve, çöp kutusu ikonu, "Geri alınamaz" yazısı, sistem onayı. Hata: çarpı ikonu ve "Tekrar bak: …" metni. **Onaylandı.** |
| Görev kartı durumları | Şekille: planlı boş halka, tamamlandı dolu tik, yarım yarısı dolu halka, yapılmadı kesik halka (çarpı ve ünlem yok, altında planın ne yaptığı). Gölge modunda da okunur. |
| YouTube etiketi | **Resmi YouTube logosu, kendi renkleriyle.** Marka paletinin bilinçli istisnası: YouTube API politikasına uymak ürünün değişmez kuralı; logo bizim paletimiz değil, YouTube'un markası. |
| Güvenli mod dumanı | **Sakin.** "Soluk" kılavuzdaki anlamıyla (bir süre ara verip dönüş) kalır; zor bir günde "sönüyorsun" gibi okunmasın. |
| Bugün özeti sayımı | **"2 kitap · 1 video"** (videolar kitap sayılmaz). Sabah bildirimi de aynı biçimde. |
| "Gün tamam" koşulu | Ürünün seri kuralı: günün görevlerinin **en az üçte ikisi ya da planlanan dakikanın en az %60'ı** yapıldıysa gün tamam ve seri artar (öğrenci ekranı ve veli raporu aynı kuralı kullanır). "Gün tamam" sahnesi bu koşula bağlanır, "bütün kartlar tamamlandı"ya değil. Check-in bitmiş ama gün tamam değilse kutlamasız, sakin bir kapanış ("Bugünlük bu kadar, yarın kaldığın yerden"). |
| Gün tamam metni | Öneri kabul: "Bugünlük bu kadar." ve "Planın tamam, serin 7 gün oldu. Yarın kaldığın yerden." |
| Duman, Bugün ekranında | Başlığın sağında, altında adı yazılı. Yeni kullanıcı, normal gün, akşam: sakin. Güvenli mod: sakin. Gün tamam: yanık. Öneri (onay bekliyor): dinlenme günü kapalı, sınava ≤ 30 gün titrek. |
| Alaaddin, Bugün ekranında | Yalnız dönüm noktalarında, tek ve kısa cümleyle: yeni kullanıcıda boş plan sahnesi, güvenli modda bandın içinde "sakin", gün tamamda gün tamam sahnesi. Normal gün ve akşamda yok. |
| SCREENS.md'den kabul edilen sapmalar | "Yaptım" birincil değil ara düğme; giriş kenarı `control`; prototip için eklenen sade "Nereye kadar geldin?" ve "Ne oldu?" adımları. |
| Ölçüler | Boşluk 4 pt tabanlı; köşeler 6, 10, 14, 20, 28; dokunma alanları 44, 52, 56. |
| Sekme ikonları (SF Symbols) | sun.max, books.vertical, bubble.left.and.bubble.right, gearshape; seçili sekmede dolu ikon ve kalın etiket. |

## Verildi (27 Ekim 2026, 3. sürüm: kurulum)

| Konu | Karar |
|---|---|
| İlerleme göstergesi | Üstte geri okunun yanında 6 bölüt; başlığın üstünde "Adım n/6". |
| Seçim kutusu ve çip | Seçili hali `foreground` dolgu ve tik (koyuda krem, açıkta gece moru). Turuncu yalnız tek ana eylemde: Başla, Devam, Planımı kur. TOKENS.md düzeltildi. |
| Karşılama'da logo | **Yok.** Yalnız Alaaddin karşılama sahnesi; marka bir önceki açılış ekranında (gece moru zemin, lamba simgesi). Kılavuzun "yazı logosu ve simge aynı ekranda değil" kuralıyla da uyumlu. |
| Alaaddin, kurulumda | Karşılama'da karşılama sahnesi, Hazırsın'da **"mutlu"** (kurulumun bitişi tek seferlik dönüm noktası; onaylandı). Aradaki adımlarda yok. |
| Hazırsın özeti | Sınava kalan gün ve haftalık saat iki satırda, ikonlu. 18 altı kutusu ürün metnini aynen kullanır. |
| Figma'nın eklediği metinler | Tarih kutularında "GG / AA / YYYY" ipucu ve Hazırsın hata sahnesi kabul. |
| Ortak adım düzeni | Kurulum ve check-in adımları aynı düzeni (ilerleme, başlık, içerik, altta tek ana eylem) kullanır. |

**Bugün ekranına henüz işlenmeyenler** (1. sürüm kararları, prototipte uygulanmalı): güvenli mod dumanı
"sakin", "2 kitap · 1 video" sayımı, "gün tamam" koşulu, resmi YouTube logosu, tehlikeli eylem çerçevesinin
rengi (`control`, kırmızı yok). Uygulamada sayım, YouTube logosu ve çerçeve var; duman ve sahneler henüz yok.

## Açık

- **Açık temada duman ve sahneler:** duman SVG'lerinin ve çizimlerin açık zemin sürümü yok; şimdilik gece moru
  `stage` kutusunda. Açık zemin sürümleri marka tasarımcısından istenecek.
- **Dinlenme günü ve sınava ≤ 30 gün duman önerileri** onay bekliyor.
- **Gölge modu** ürün kararı bekliyor (henüz uygulamada yok).
- **Klavye açık hali:** Devam'ın klavyenin üstüne yapışması prototipte yok; uygulamada yerel davranışla yapılır.
