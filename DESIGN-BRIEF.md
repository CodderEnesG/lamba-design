# lamba: tasarım özeti

Bu belge uygulamayı tasarımcıya ve Figma Make'e anlatır. Kod okumana gerek yok: ekranlar
[SCREENS.md](SCREENS.md)'de, uyulması gereken kurallar [UI-RULES.md](UI-RULES.md)'de, marka
[brand/](brand/)'de ve kılavuzu `brand/kilavuz/lamba-marka-kilavuzu.html`'de.

Kaynak: ürünün ana reposu (`yks-ai-koc`). Ürün kararları orada değişir; bu klasör o kararların tasarım
için hazırlanmış özetidir (27 Ekim 2026).

## Ürün tek cümlede

**lamba**, YKS'ye hazırlanan öğrencinin elindeki kitaplara ve izlediği YouTube ders listelerine göre her
gün sayfa, test ve video düzeyinde plan çıkaran, akşam "bugün ne oldu?" diye soran, aksayan bir şey olursa
planı yeniden kuran ve haftalık özeti veliye gönderen bir mobil koç.

Değer yapay zekânın zekâsından değil **takipten** geliyor: plan yapmak kolay, onu her gün uygulatmak zor.
Planı bir kural motoru hesaplar; yapay zekâ konuşur, yorumlar ve kitabın içindekiler sayfasını okur.

## Kimin için

| Kişi | Durum | Uygulamadan ne ister |
|---|---|---|
| **Öğrenci** (ana kullanıcı) | 11. ve 12. sınıf ya da mezun, 15-19 yaş. Telefonda, akşam yorgun, sınav stresi yüksek. | Bugün ne yapacağını bir bakışta görmek, yapınca işaretlemek, aksayınca suçlanmadan planın düzelmesi. |
| **Veli** (ödeyen) | Uygulamayı kullanmaz. 18 yaş altı öğrencinin verisi için onay verir, haftalık rapor alır. | Çocuğunun düzenli çalıştığını görmek; sohbet ya da kişisel detay değil. |

Platform: önce iOS, sonra Android (Expo / React Native). Dil yalnız Türkçe. Açık ve koyu tema var.

## Günlük döngü (ürünün kalbi)

1. **Sabah:** Bildirim "Bugünün planı hazır: ≈ 2 sa · 2 kitap". Öğrenci **Bugün** ekranını açar.
2. **Gün içinde:** Bugün ekranında görev kartları: "3 Adım TYT Tarih · sayfa 41-58 · ≈ 50 dk", "Matematik
   test 12-14", "YouTube: Türev 3. ders · 24 dk video". Çalışırken uygulama arka planda kalır.
3. **Akşam check-in:** Her kart için "Yaptım", "Yarım kaldı" (nereye kadar), "Yapamadım". Yapamadıysa tek
   dokunuşla neden: zaman yetmedi, konu zor, isteksizim, kendimi kötü hissediyorum.
4. **Yeniden plan:** Kural motoru yarın ve sonrasını otomatik ayarlar. "Kötü hissediyorum" derse 3 gün
   **güvenli mod**: yük yarıya iner, ton yumuşar, Destek ekranı önerilir.
5. **Seri ve ilerleme:** Tamamlanan günler seriyi büyütür; kitap başına yüzde.
6. **Pazar:** Veli onay verdiyse öğrenci haftalık raporu veliye WhatsApp'tan gönderir.

## Özellikler (bugün çalışan ya da kodu yazılmış)

- **Kurulum (6 adım):** doğum ayı/yılı, sınıf, alan (SAY/EA/SÖZ/DİL), hedef (sıralama ya da puan,
  atlanabilir), sınav tarihi, hafta içi / hafta sonu günlük süre. 18 yaş altıysa veli onayı uyarısı.
- **Kütüphane:** kitap ekleme dört yoldan: barkod okut, katalogda ara, **içindekiler sayfasının fotoğrafı**
  (yapay zekâ bölümleri okur, öğrenci kontrol eder), hızlı ekle (ad + sayfa/test sayısı). Ayrıca **YouTube
  oynatma listesi** (link yapıştır, videolar sırayla plana girer). Kitap başına ilerleme çubuğu.
- **Bugün:** sınava kalan gün, seri, görev kartları, check-in, isteğe bağlı doğru/yanlış sayısı, uyarılar
  (plan sığmıyor, dinlenme günü), güvenli mod bandı, Pazar günü "raporu velime gönder".
- **Koç (sohbet):** yapay zekâ koçla yalnız yazılı sohbet. Plan, motivasyon, aksayan günler. Soru çözmez.
  Riskli mesajda önce güvenlik katmanı çalışır; akut riskte koç yerine sabit destek metni ve Destek ekranı.
- **Destek:** 112 ve ALO 183'ü arama, "velime ya da rehberime haber ver" (öğrenci kendisi gönderir),
  "planımı hafiflet". Onay beklerken bile çalışır.
- **Ayarlar:** sabah bildirim saati, hesap bağlama (e-posta + 6 haneli kod), yedekleme, veli onayı iste,
  haftalık rapor, verileri sil.
- **Veli onayı:** 18 yaş altı öğrenci velinin e-postasını yazar, linki WhatsApp'la gönderir. Veli web
  sayfasında açıklamayı okur, rızaları ayrı ayrı verir, e-postasına gelen kodla doğrular; aynı linkten geri
  çekebilir. Onaya kadar sohbet, fotoğraf, YouTube ve yedekleme kapalı; plan telefonda çalışır.
- **Haftalık veli raporu (web):** haftanın günleri (tamam/planlı), tamamlanan gün, çalışma süresi, seri,
  kitap yüzdeleri, kısa not. Sohbet asla yer almaz.
- **Bildirimler:** sabah planı, akşam 20:00 ve 21:30 check-in hatırlatması.

## Henüz olmayanlar (tasarlanmayacak ya da sonra)

Ödeme ve Premium ekranları (Şubat 2027), deneme sonucu girişi, uygulama içi video oynatıcı (Ocak),
liste ↔ kitap bağlama, odak zamanlayıcısı, sosyal paylaşım ve sıralama, kitle kaynaklı katalog. Marka
kılavuzundaki "Çalışıyor" sahnesi ve "Gölge modu" henüz uygulamada yok (bkz. UI-RULES).

## Ton

Samimi, kısa, yargısız. "Sen" diye hitap. Koç **tatlı-sert** olabilir ama sertlik yalnız davranışa yönelir,
kişiye asla ("testi atlamışsın, yarın ilk iş onu yapalım"; "tembelsin" değil). Güvenli modda sertlik
tamamen kalkar. Başarısızlık ve ara vermek suçlanmaz; marka kılavuzundaki "Ara verdi" sahnesi bu ruhla.
Marka adı her zaman küçük harf: **lamba**.

## Tasarımdan beklenen

1. [SCREENS.md](SCREENS.md)'deki **tüm ekranların** marka kimliğiyle yeniden tasarımı. Şu anki görünüm geçici
   (siyah-beyaz, varsayılan bileşenler). Ekran akışı ve içerik aynı kalır; görsel dil, hiyerarşi ve
   mikro metin önerileri serbest.
2. **Ortak bileşenler:** adım ekranı (ilerleme + alt sabit buton), seçim çipi, görev kartı (sayfa, test,
   video; planlı / yapıldı / yarım / yapılmadı), check-in düğmeleri, neden seçimi, sohbet balonları
   (öğrenci, koç, sabit destek yanıtı, "bildir"), bantlar (güvenli mod, onay bekleniyor, uyarı), boş durum,
   hata durumu, yükleme, birincil / ikincil / tehlikeli eylem butonu, alt sekme çubuğu (4 sekme).
3. **Açık ve koyu tema** (marka paleti ikisini de tanımlıyor). Koyu tema ana kimlik (gece moru).
4. **Alaaddin ve sahnelerin yerleşimi:** hangi ekranda hangi sahne ya da ifade (kılavuzdaki eşleşmeler:
   karşılama, boş plan, gün tamam, ara verdi, sınav yaklaşıyor, hata, ilerleme; düşünüyor = yükleme).
5. **Duman durumlarının** uygulamadaki anlamı için öneri (kılavuz "şimdilik öneri" diyor): örneğin Bugün
   ekranında günün durumu.
6. Veli web sayfaları (onay ve rapor): mobil tarayıcıda okunur, sade.

Çıktı tasarımlar uygulamaya geliştirici tarafından işlenir; Figma Make'in ürettiği kod doğrudan uygulamaya
girmez. Bu yüzden görsel karar ve bileşen tutarlılığı, çalışan koddan daha önemli.
