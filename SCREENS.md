# Ekran envanteri

Uygulamadaki tüm ekranlar; ne gösterdikleri, hangi durumlarda nasıl değiştikleri ve düğmelerin ne yaptığı.
Metinler uygulamadaki gerçek metinlerdir (tırnak içinde). Süslü parantezli yerler değişkendir:
`{gün}`, `{e-posta}` gibi.

Bu belge 27 Ekim 2026'daki koda göre yazıldı. Şu anki görünüm geçicidir; renk, yazı, boşluk ve ikonlar
yeniden tasarlanacak. Buradaki "birincil düğme", "çerçeveli düğme" gibi adlar bugünkü düğme türlerini
anlatır, tasarım önerisi değildir. Uygulamanın kodundaki çalışma adı "YKS AI Koç"; marka adı **lamba**.

Her bölümün sonundaki **Kaynak** satırı geliştiriciler içindir; tasarım için okumanız gerekmez.

---

## 0. Gezinme haritası

### Açılış

- Uygulama açılınca açılış ekranı (splash) görünür.
- Öğrencinin profili yoksa **Kurulum** akışı açılır. Profil varsa **sekmeler** açılır, ilk sekme **Bugün**.
- Kurulumdan kenar kaydırmayla geri çıkılamaz (sekmelere sızılmaz). Kurulum içindeki adımlar arasında geri
  gidilebilir.
- Nadir bir hata durumu: telefondaki veritabanı hazırlanamazsa tüm ekran yerine tek satır kırmızı yazı çıkar:
  "Veritabanı hazırlanamadı: {hata}". Tasarlanmamış; basit bir hata ekranı yeterli.

### Alt sekme çubuğu (4 sekme)

Sistemin yerel sekme çubuğu kullanılıyor (iOS'ta iOS sekme çubuğu, Android'de Material).

| Sıra | Etiket | Bugünkü ikon |
|---|---|---|
| 1 | Bugün | Ev ikonu (görsel dosya) |
| 2 | Kütüphane | "Keşfet" ikonu (görsel dosya; şablondan kalma, değişmeli) |
| 3 | Koç | İki konuşma balonu (sistem ikonu) |
| 4 | Ayarlar | Dişli (sistem ikonu) |

Sekme ekranlarının üst çubuğu yok; başlık içeriğin en üstünde büyük yazıyla durur.

### Ekran akışları (sekmeler dışındaki ekranlar)

Kurulum sekmelerin yerine açılır; diğerleri sekmelerin üstüne itilir. Hepsinde aynı üst çubuk var: **başlıksız**, yalnız sol üstte
geri oku (yazısız; ekran okuyucu için adı "Geri"), alt gölgesi yok.

| Akış | Ekranlar | Nereden açılır |
|---|---|---|
| Kurulum | Karşılama, 6 adım, Hazırsın | İlk açılış; veriler silinince |
| Kitap/kaynak ekleme | Ekleme yolu seçimi, Barkod, Katalog arama, Baskı ayrıntısı, Hızlı ekle, İçindekilerden ekle, İçindekiler kontrolü, YouTube listesi | Bugün, Kütüphane |
| Check-in | Yarım kaldı, Ne oldu? | Bugün'deki görev kartı |
| Hesap | Hesap bağla / Hesabına giriş yap, Veli onayı | Ayarlar, Koç, Bugün, kilitli ekranlar, Karşılama |
| Destek | Destek | Ayarlar, Bugün, Koç |

Karşılama ekranında üst çubuk da yok.

### Uygulama dışı yüzeyler

- **Veli web sayfaları** (tarayıcıda): Veli onayı sayfası ve Haftalık rapor sayfası. Bölüm 7.
- **Bildirimler** (ekran değil, metin olarak bilgi için):
  - Sabah: "Bugünün planı hazır" / "≈ {süre} · {n} kitap · {m} video. Başlamak için dokun." (video yoksa yalnız kitap)
  - Akşam: "Bugün nasıl geçti?" / "Check-in yap; yarının planı ona göre ayarlanır."
  - Geç kalan check-in: "Check-in bekliyor" / "Bir dakikanı alır. Yapamadıysan da söyle, planı kaydıralım."
- **Sistem pencereleri:** kamera ve galeri izinleri, paylaşım menüsü, onay uyarıları (Kaldır, Sil). Uyarılar
  sistemin kendi penceresidir; içerikleri ilgili ekranda yazıyor.

### Genel gözlemler

- Uygulama telefonun açık/koyu temasını izliyor; iki tema da gerekli.
- Birçok ekran veri yüklenirken **hiçbir şey göstermiyor** (boş beyaz ekran, genelde bir an). Yükleniyor
  göstergesi yalnız İçindekilerden ekle, YouTube listesi ve Koç (gönderiliyor) ekranlarında var. İskelet
  (skeleton) ya da ortak bir yükleniyor durumu tasarlamak açık bir fırsat.
- Hata metinleri bugün kırmızı küçük yazı. Marka kuralı doğru/yanlış/uyarı için renk kullanmıyor
  (UI-RULES.md); hata satırı yeniden tasarlanmalı.

---

## 1. Kurulum (onboarding)

Akış: Karşılama → Adım 1 Doğum → Adım 2 Sınıf → Adım 3 Alan → Adım 4 Hedef → Adım 5 Sınav tarihi →
Adım 6 Günlük süre → Hazırsın → Bugün.

Adım ekranlarının ortak düzeni (**Adım ekranı**, bölüm 8): üstte küçük gri "Adım {n}/6", altında başlık,
varsa gri alt başlık, içerik, en altta tam genişlik "Devam" düğmesi. Klavye açılınca Devam klavyenin üstüne
yapışır. Seçim yapılmadan Devam soluk ve basılamaz. Bugün yalnız yazıyla adım gösteriliyor; ilerleme çubuğu
yok.

### 1.1 Karşılama

- **Nereden:** ilk açılış; verileri silince; Hazırsın ekranındaki hata durumundan.
- **Ne için:** kurulumu başlatmak ya da eski hesabı geri yüklemek.
- **İçerik** (üst çubuk yok, metin dikeyde ortada):
  - Büyük başlık: "Planını birlikte kuralım"
  - Gövde (büyük gri): "Birkaç soruyla günlük çalışma planının iskeletini çıkaracağız. Kitaplarını bir sonraki
    adımda ekleyeceksin."
  - Altta: birincil büyük düğme "Başla"
  - Altında yazı düğmesi: "Hesabım var, geri yükle"
- **Eylemler:**
  - "Başla": önceki yarım kurulumu sıfırlar, Adım 1'e gider.
  - "Hesabım var, geri yükle": Hesabına giriş yap ekranı (5.1, geri yükleme modu).
- **Durumlar:** tek durum.
- **Kaynak:** apps/mobile/src/app/onboarding/index.tsx

### 1.2 Adım 1/6: Doğum ayı ve yılı

- **Ne için:** yaş; 18 altı ise veli onayı gerekir.
- **İçerik:**
  - "Adım 1/6"
  - Başlık: "Doğum ayın ve yılın"
  - Alt başlık: "18 yaşından küçüksen velinden onay isteyeceğiz. Gün sormuyoruz."
  - "Ay" etiketi + 12 ay seçim kutusu, 3 sütunlu ızgara ("Ocak" … "Aralık")
  - "Yıl" etiketi + 17 yıl seçim kutusu, 4 sütunlu ızgara (bu yıldan 14 yıl öncesinden 30 yıl öncesine;
    2026'da 2012 … 1996)
  - "Devam"
- **Durumlar:** ay ve yıl seçilmeden Devam pasif. Seçili kutu vurgulu.
- **Eylemler:** Devam → Adım 2.
- **Kısıtlar:** gün sorulmaz. Doğum ayı içindeki öğrenci 18 altı sayılır (koruyucu taraf).
- **Kaynak:** apps/mobile/src/app/onboarding/birth.tsx

### 1.3 Adım 2/6: Sınıf

- **İçerik:** "Adım 2/6"; başlık "Kaçıncı sınıftasın?"; alt alta 3 seçim kartı: "11. sınıf", "12. sınıf",
  "Mezun"; "Devam".
- **Durumlar:** seçim yoksa Devam pasif.
- **Eylemler:** Devam → Adım 3. Sınıf değişirse önceden seçilen sınav tarihi sıfırlanır.
- **Kaynak:** apps/mobile/src/app/onboarding/grade.tsx

### 1.4 Adım 3/6: Alan

- **İçerik:** "Adım 3/6"; başlık "Alanın hangisi?"; alt alta 4 seçim kartı, her birinde başlık ve gri açıklama:
  - "Sayısal" / "Matematik, fizik, kimya, biyoloji"
  - "Eşit Ağırlık" / "Matematik, edebiyat, tarih, coğrafya"
  - "Sözel" / "Edebiyat, tarih, coğrafya, felsefe grubu"
  - "Dil" / "Yabancı dil"
  - "Devam"
- **Durumlar:** seçim yoksa Devam pasif.
- **Kaynak:** apps/mobile/src/app/onboarding/field.tsx

### 1.5 Adım 4/6: Hedef

- **İçerik:**
  - "Adım 4/6"; başlık "Hedefin ne?"
  - Alt başlık: "Koçun seni buna göre motive eder. Emin değilsen geçebilirsin."
  - Yan yana 2 seçim kartı: "Sıralama" (varsayılan seçili), "Puan"
  - Sayı alanı; ipucu yazısı türe göre "Örn. 20000" ya da "Örn. 450"
  - Hata satırı (geçersiz değerde): "1 ile 3.000.000 arasında bir sıralama gir" ya da
    "100 ile 560 arasında bir puan gir"
  - Altta, Devam'ın üstünde yazı düğmesi "Şimdilik geç"; en altta "Devam"
- **Durumlar:** alan boş ya da geçersizse Devam pasif; yazılmış ama geçersizse hata satırı görünür.
- **Eylemler:** Devam → Adım 5 (hedef kaydedilir). "Şimdilik geç" → Adım 5 (hedefsiz).
- **Kaynak:** apps/mobile/src/app/onboarding/target.tsx

### 1.6 Adım 5/6: Sınav tarihi

- **İçerik:**
  - "Adım 5/6"; başlık "Sınav tarihin"; alt başlık "ÖSYM takvimi açıklanınca tarihi güncelleyeceğiz."
- **Durum A, tahmini tarih var** (varsayılan): vurgulu kart içinde büyük tarih ("19 Haziran 2027") ve altında
  gri "tahmini"; altında çerçeveli düğme "Farklı bir tarih gir"; "Devam".
  - Tahmini tarih sınıfa göre: 12. sınıf ve mezun ilk sınav (19 Haziran 2027), 11. sınıf bir sonraki
    (17 Haziran 2028). İkisi de tahmindir.
- **Durum B, elle giriş:** yan yana 3 sayı kutusu "Gün", "Ay", "Yıl"; yıl 4 haneye ulaşınca tarih geçersiz ya
  da geçmişteyse hata "Geçerli ve ileride bir tarih gir"; yazı düğmesi "Tahmini tarihi kullan" (A'ya döner).
- **Durum C, tahmini tarih yok** (liste bittiyse): B'nin üstünde gri "Tahmini tarih yok; tarihi kendin gir.",
  "Tahmini tarihi kullan" düğmesi yok.
- **Eylemler:** Devam → Adım 6. Tarih geçerli ve ileride değilse pasif.
- **Kaynak:** apps/mobile/src/app/onboarding/exam.tsx

### 1.7 Adım 6/6: Günlük çalışma süresi

- **İçerik:**
  - "Adım 6/6"; başlık "Günde ne kadar çalışabilirsin?"
  - Alt başlık: "Gerçekçi ol; plan buna göre kurulur, sonra değiştirebilirsin."
  - İki sayaç satırı (− değer +): "Hafta içi" (varsayılan "2 saat"), "Hafta sonu" (varsayılan "4 saat")
  - Yazı düğmesi: "Günleri ayrı ayarla"
  - "Devam"
- **Durumlar:**
  - **Ayrı günler:** "Günleri ayrı ayarla"ya basınca 7 sayaç satırı ("Pazartesi" … "Pazar"); düğme kaybolur.
    Daha önce günler farklı girildiyse doğrudan bu durumda açılır.
  - Sayaç 30 dakikalık adımla 0 ile 12 saat arası. Değer metni: "Çalışmıyorum" (0), "2 saat", "2,5 saat".
    Sınırda − ya da + soluk.
  - Hepsi 0 ise hata satırı "En az bir gün çalışma süresi gir" ve Devam pasif.
- **Eylemler:** Devam → Hazırsın.
- **Kaynak:** apps/mobile/src/app/onboarding/time.tsx

### 1.8 Hazırsın

- **Ne için:** kurulumun özeti; 18 altına veli onayı uyarısı.
- **İçerik** (adım etiketi yok):
  - Başlık: "Hazırsın"
  - "Sınava {gün} gün var."
  - "Haftada {saat} saat çalışacaksın."
  - **Yalnız 18 altında**, gri kutu: kalın "Veli onayı gerekecek" ve altında "18 yaşından küçük olduğun için
    velinin onayı gelene kadar verilerin yalnız bu telefonda kalır. Planın çalışır; koçla sohbet ve fotoğraf
    yükleme onaydan sonra açılır."
  - Altta birincil büyük düğme "Planımı kur"
- **Durumlar:**
  - 18 üstü: kutu yok.
  - Hata (normal akışta görülmez; eksik adım ya da tarih geçmiş): tek satır yazı ("Geçerli ve ileride bir tarih
    gir" ya da "Planını birlikte kuralım") ve "Başla" düğmesi → Karşılama.
- **Eylemler:** "Planımı kur" → profil kaydedilir, Bugün sekmesi açılır.
- **Kısıtlar:** 18 altında onaya kadar veri sunucuya gitmez, analitik de toplanmaz.
- **Kaynak:** apps/mobile/src/app/onboarding/done.tsx

---

## 2. Ana sekmeler

### 2.1 Bugün

- **Nereden:** sekme 1; uygulama açılışı; check-in bitince geri dönülen yer.
- **Ne için:** günün planı, görev kartları ve akşam check-in'i.
- **İçerik** (yukarıdan aşağı, kaydırılabilir; aşağıdakilerin çoğu koşullu):
  1. **Başlık bloğu**
     - "Bugün"
     - Gri: "{tarih} · {gün adı}", örn. "27 Ekim 2026 · Salı"
     - Büyük: "Sınava {gün} gün"
     - Seri varsa (1+ gün): "Seri: {gün} gün"
     - Görev varsa, gri özet: "Bugün ≈ {süre} · {n} kitap · {m} video" (süre "45 dk", "2 sa", "2 sa 30 dk"
       biçiminde; video ya da kitap yoksa o kısım yazılmaz). Karar 27 Ekim (DECISIONS.md).
  2. **Kitap yok kutusu** (hiç kaynak yoksa): çerçeveli kutu, "Planın kitaplarına göre kurulur. İlk kitabını
     ekle." ve birincil düğme "Kitap ekle".
  3. **Bugün iş yok satırı** (kaynak var ama bugün görev yok), gri:
     - Çalışma süresi 0 olan gün: "Bugün çalışma günün değil. Dinlen."
     - Diğer: "Planlanacak iş kalmadı."
  4. **Veli onayı bandı** (18 altı, onay bekliyor ya da geri çekildi): renkli zeminli band, gri metin ve küçük
     çerçeveli düğme "Veli onayı iste".
     - Bekliyor: "Velin onay verene kadar verilerin yalnız bu telefonda kalır. Hesap bağlama onaydan sonra
       açılır."
     - Geri çekildi: "Velin onayını geri çekti; verilerin yalnız bu telefonda."
  5. **Haftalık rapor düğmesi** (yalnız **pazar** günü, yalnız hesabı bağlı ve velisi rapora izin vermiş
     öğrencide): bkz. "Rapor paylaşma bloğu", bölüm 8.
  6. **Hafif mod bandı** (güvenli mod açıksa): renkli zeminli band, "Hafif mod açık: birkaç gün yükün yarı
     yarıya." ve küçük çerçeveli düğme "Destek".
  7. **Görev kartları**: her kitap için bir kart, her video için ayrı kart. Varyantlar aşağıda.
  8. **Doğru/yanlış formu**: bugünün bütün kartlarında check-in yapılınca çıkar (aşağıda).
  9. **Uyarılar** (bugün kırmızı küçük yazı):
     - Fazla yük: "Sınava kadar her şey sığmıyor: {n} bölüm "zaman kalırsa" listesinde. Günlük süreni
       artırabilir ya da kitap çıkarabilirsin."
     - Sığmayan bölüm: "Bazı bölümler bir günlük süreden uzun; plana giremedi. Günlük süreni ya da test başı
       dakikayı gözden geçir."
  10. Yalnız geliştirici sürümünde: "Kurulu bildirim: {n}" ve "Kurulumu sıfırla (geliştirme)". **Tasarlanmaz.**

#### Görev kartı: kitap (sayfa ya da test)

- Kalın kitap adı
- Satır: solda aralık, sağda gri süre
  - Sayfa: "s. 41-58"; test: "Test 3-5"; tek sayfa/test: "s. 41"; arada boşluk varsa virgülle: "s. 41-45, 50-58"
  - Süre: "≈ 45 dk"
- Birden çok bölüm varsa gri: "{n} bölüm"
- Altta check-in alanı (aşağıda)

#### Görev kartı: video (YouTube)

- Kalın video başlığı. Video bilgisi önbellekte yoksa: "Video bilgisi yenileniyor"
- Gri: "{liste adı} · {kanal adı}"
- Satır: solda **"▶ YouTube"** etiketi (kırmızı, küçük, kalın), sağda gri süre:
  "{video süresi} video · ≈ {plan süresi} not dahil" (örn. "12 dk video · ≈ 15 dk not dahil"); video bilgisi
  yoksa yalnız "≈ {süre}"
- Küçük çerçeveli düğme "YouTube'da aç" (video kimliği yoksa gizli) → YouTube uygulaması ya da tarayıcı
- Altta check-in alanı

#### Kartın check-in alanı

- **Bekliyor** (yan yana küçük düğmeler):
  - Birincil: "Yaptım" (video: "İzledim") → hemen tamamlandı olur, onay sorulmaz, geri alma yok.
  - Çerçeveli: "Yarım kaldı" → Check-in: Yarım kaldı (4.1). **Yalnız** kitap kartında ve aralık birden çok
    sayfa/test içeriyorsa görünür; videoda hiç yok.
  - Çerçeveli: "Yapamadım" (video: "İzleyemedim") → Check-in: Ne oldu? (4.2)
- **Tamamlandı:** kalın "✓ Tamamlandı" (video: "✓ İzlendi")
- **Yapılmadı:** kalın "Yapılmadı · {neden}" ve altında gri planın ne yaptığı (neden metinleri 4.2'de)
- **Yarım:** kalın "Yarım: {yapılan aralık} yapıldı · {neden}" (örn. "Yarım: s. 41-50 yapıldı · Zaman yetmedi")
  ve altında gri etki metni
- Neden "Kötü hissediyorum" ise ek olarak küçük çerçeveli "Destek" düğmesi → Destek ekranı

#### Doğru/yanlış formu (isteğe bağlı)

- Çerçeveli kutu: kalın "Bugün çözdüğün sorular (isteğe bağlı)"
- Yan yana: "Doğru" ve "Yanlış" ipuçlu iki sayı kutusu (en çok 4 hane), küçük birincil "Kaydet"
- İkisi de boşsa Kaydet pasif
- Kaydedilince kutunun yerine gri satır: "Kaydedildi: {d} doğru, {y} yanlış"

#### Durumlar (özet)

- Yeni kullanıcı, kitap yok → kitap yok kutusu.
- Dinlenme günü / iş kalmadı → gri satır.
- Görevler bekliyor → kartlar check-in düğmeleriyle.
- Kısmen check-in → bazı kartlar sonuçlu, bazıları düğmeli.
- Hepsi check-in → kartlar sonuçlu + doğru/yanlış formu (ya da kayıt satırı).
- 18 altı onaysız → veli onayı bandı (plan yine çalışır).
- Pazar + hesap + rapor izni → rapor düğmesi.
- Güvenli mod → hafif mod bandı. Güvenli mod iki yolla açılır: "Kötü hissediyorum" nedeni seçilince
  **ertesi gün** başlar ve 3 gün sürer; Destek ekranındaki "Planımı birkaç gün hafiflet" ya da sohbetteki
  risk sinyali **aynı gün** başlatır (o gün + 3 gün).
- Fazla yük / sığmayan bölüm → uyarı satırları.

#### Kısıtlar

- Plandaki sayılar (aralık, süre, gün) kural motorundan gelir, yapay zekâdan değil.
- "▶ YouTube" etiketi ve kanal adı video kartında görünür kalmalı (YouTube politikası). Video uygulama içinde
  oynatılmaz; yalnız "YouTube'da aç". İzleme verisi toplanmaz.
- Hafif mod bandı yumuşak dille; alarm dili yok.
- **Kaynak:** apps/mobile/src/app/(tabs)/index.tsx, features/plan/task-card.tsx, features/plan/counts-form.tsx,
  features/report/report-share.tsx

### 2.2 Kütüphane

- **Nereden:** sekme 2; kitap ekleme akışı bitince buraya dönülür.
- **Ne için:** eklenen kitap ve listelerin ilerlemesi; yeni kaynak ekleme; kaldırma.
- **İçerik:**
  - Başlık "Kütüphane"
  - Boşsa gri: "Henüz kitap eklemedin. Planın eklediğin kitaplara göre kurulur."
  - Her kaynak için çerçeveli kart:
    - Kalın ad
    - Gri özet:
      - Kitap: "{toplam} sayfa · {n} bölüm · sayfa başı {dk} dk" (test kitabında "test" ve "test başı")
      - YouTube listesi: "{n} video · {hız}× · {kanal}" (örn. "24 video · 1,25× · Kanal Adı")
      - Liste bilgisi 30 günü geçtiyse: "Liste bilgisi 30 günü geçti; yenilenince plana döner."
    - İnce ilerleme çubuğu
    - Gri "%{n} tamamlandı"
    - Kırmızı yazılı yazı düğmesi "Kaldır"
  - Listenin altında birincil "Kitap ekle" (her durumda görünür)
- **Eylemler:**
  - "Kitap ekle" → Ekleme yolu seçimi (3.1).
  - "Kaldır" → sistem uyarısı: başlık "\"{ad}\" kütüphanenden kaldırılsın mı?", düğmeler "Vazgeç" ve
    "Kaldır" (yıkıcı). Onaylanınca kart kaybolur.
- **Durumlar:** boş; dolu; liste bilgisi süresi geçmiş kart. Kartlara dokunmak bir şey açmaz (ayrıntı ekranı
  yok).
- **Kısıtlar:** kapak görseli, sayfa görüntüsü yok. Not: YouTube listesi kartında bugün "▶ YouTube" etiketi
  yok, yalnız kanal adı var; etiketin burada da gerekip gerekmediği **açık soru**.
- **Kaynak:** apps/mobile/src/app/(tabs)/library.tsx

### 2.3 Koç

- **Nereden:** sekme 3.
- **Ne için:** yapay zekâ koçla yalnız metin sohbeti (plan, aksayan günler, motivasyon; soru çözmez).
- **Durum A, kilitli: veli onayı yok** (18 altı, onay bekliyor ya da geri çekildi):
  - Başlık "Koç"
  - "Sohbet, velin onay verdikten sonra açılır. O zamana kadar planın bu telefonda çalışmaya devam ediyor."
  - Birincil "Veli onayı iste" → Veli onayı (5.2)
- **Durum B, kilitli: hesap yok** (onay sorunu yok ama hesap bağlı değil):
  - Başlık "Koç"
  - "Koçla konuşmak için önce hesabını bağla; sohbet sunucuda işlenir."
  - Birincil "Hesap bağla" → Hesap bağla (5.1)
  - Onay eksikse önce A gösterilir.
- **Durum C, sohbet:**
  - Kaydırılan listenin en üstünde başlık "Koç" ve gri tanıtım: "Ben bir yapay zekâ koçuyum. Planını, aksayan
    günleri ve motivasyonunu konuşabiliriz; soru çözmem. Yazdıkların velinle paylaşılmaz."
  - Mesaj balonları (bölüm 8):
    - **Öğrenci:** sağda, dolu renkli balon. Gönderilemezse altında kırmızı küçük yazı düğmesi
      "Gönderilemedi · Tekrar dene".
    - **Koç:** solda, gri balon. Altında küçük yazı düğmesi "Bildir"; basınca yerine gri "Bildirildi,
      teşekkürler".
    - **Koç, akut risk yanıtı:** balonda sabit destek metni ve altında küçük birincil "Destek ekranını aç".
  - Hata satırı (giriş alanının üstünde, kırmızı):
    - "Bugünkü mesaj hakkın doldu; yarın devam edelim."
    - "Sohbet velinin onayından sonra açılır."
    - "Oturumun kapanmış; Ayarlar’dan hesabını yeniden bağla."
    - "Mesaj gönderilemedi; internet bağlantını kontrol et."
  - Uzunluk uyarısı (kırmızı): "Mesaj en fazla 1000 karakter olabilir."
  - Alt çubuk (üstünde ince çizgi): çok satırlı metin alanı, ipucu "Koçuna yaz…"; sağda "Gönder" düğmesi
    (gönderirken "Gönderiliyor…").
- **Eylemler:**
  - Gönder: alan boş, 1000 karakteri aşıyor ya da gönderim sürüyorsa pasif. Basınca alan temizlenir, mesaj
    listeye eklenir.
  - Koç akut risk yanıtı verirse uygulama **kendiliğinden Destek ekranına geçer**; geri dönünce balon ve
    "Destek ekranını aç" düğmesi durur.
  - "Bildir": mesajı inceleme için işaretler.
- **Durumlar:** kilitli (2 tür), boş sohbet (yalnız tanıtım; ayrı boş durum yok), mesajlar, gönderiliyor,
  gönderilemedi, kota doldu, oturum kapandı, akut yanıt. Gönderilmekte olan mesaj balonu bugün normal
  balondan farksız; "yazıyor" göstergesi yok. Koç yanıtının başka türleri (kontrol sorusu, destek önerisi,
  hizmet yok) aynı gri balonla görünür.
- **Kısıtlar:**
  - **Yalnız metin.** Fotoğraf, dosya, sesli mesaj, ek düğmesi yok ve eklenmeyecek.
  - Sohbet veliye hiçbir zaman gösterilmez; tanıtım metni bunu söyler.
  - Akut riskte koç yanıt üretmez; sabit metin + Destek ekranı.
  - Sohbet geçmişi yeni telefona taşınmaz.
- **Kaynak:** apps/mobile/src/app/(tabs)/coach.tsx

### 2.4 Ayarlar

- **Nereden:** sekme 4.
- **İçerik** (bölümler alt alta):
  1. Başlık "Ayarlar"
  2. **Sabah bildirimi**
     - Kalın "Sabah bildirimi", gri "Günün planı bu saatte gelir."
     - 7 saat seçim kutusu, 4 sütunlu ızgara: "06:30", "07:00", "07:30", "08:00" (varsayılan), "08:30",
       "09:00", "10:00". Basınca hemen kaydedilir.
  3. **Hesap ve yedek** (kalın "Hesap ve yedek"), 3 varyant:
     - **18 altı, onay yok:** gri metin (bekliyor ya da geri çekildi; metinler Bugün'deki bandla aynı) ve
       birincil "Veli onayı iste" → Veli onayı.
     - **Hesap bağlı:** "Bağlı: {e-posta}"; gri "Son yedek: {gg.aa.yyyy ss:dd}" ya da "Henüz yedeklenmedi";
       rapor paylaşma bloğu (velisi rapora izin verdiyse, her gün); çerçeveli "Şimdi yedekle"; sonuç satırı
       "Yedek güncel" / "{n} kayıt yedeklendi" / "Yedeklenemedi; internet bağlantını kontrol et."; yazı düğmesi
       "Çıkış yap".
     - **Hesap bağlı değil** (yetişkin ya da onaylı 18 altı): gri "Hesap bağlarsan planın ve ilerlemen
       yedeklenir; telefon değiştirince geri gelir." ve birincil "Hesap bağla" → Hesap bağla.
  4. **Destek**: kalın "Zor bir an mı yaşıyorsun?", gri "Konuşabileceğin yerler ve planını birkaç gün
     hafifletme.", çerçeveli "Destek" → Destek ekranı.
  5. **Verileri sil**: kalın "Verileri sil", gri açıklama, yıkıcı (kırmızı) düğme.
     - Hesaplı: açıklama "Hesabın, sunucudaki yedeğin ve bu telefondaki planın, kitapların ve check-in
       kayıtların kalıcı olarak silinir." Düğme "Hesabımı ve verilerimi sil".
     - Hesapsız: açıklama "Bu telefondaki planın, kitapların ve check-in kayıtların kalıcı olarak silinir."
       Düğme "Verilerimi sil".
- **Eylemler:**
  - Sil düğmesi → sistem uyarısı: başlık "Her şey silinsin mi?", gövde "Bu işlem geri alınamaz. Uygulama
    kurulumun başına döner.", düğmeler "Vazgeç" ve "Sil" (yıkıcı). Silinirken düğme pasif. Başarılı → Karşılama.
    Başarısız → kırmızı "Silinemedi; internet bağlantını kontrol edip tekrar dene."
  - "Çıkış yap": oturumu kapatır, bölüm "hesap bağlı değil" varyantına döner.
- **Kısıtlar:** hesap ve veri silme burada bulunur ve geri alınamaz olduğu yazar (Apple şartı). 18 altı onaysız
  hesap bağlayamaz.
- **Kaynak:** apps/mobile/src/app/(tabs)/settings.tsx

---

## 3. Kitap ve kaynak ekleme

Akış: Ekleme yolu seçimi → (Barkod → Katalog arama → Baskı ayrıntısı) | (Katalog arama → Baskı ayrıntısı) |
(İçindekilerden ekle → İçindekiler kontrolü) | Hızlı ekle | YouTube listesi → **Kütüphane sekmesi**.
Ekleme bitince öğrenci nereden başlamış olursa olsun Kütüphane sekmesine döner.

### 3.1 Ekleme yolu seçimi

- **Nereden:** Bugün "Kitap ekle", Kütüphane "Kitap ekle".
- **İçerik:** başlık "Kitabını nasıl ekleyelim?" ve alt alta 5 kart (seçim kartı görünümünde, ama seçim değil
  gezinme yapar):
  - "Barkodu okut" / "Arka kapaktaki ISBN barkodu" → 3.2
  - "Ara" / "ISBN ya da kitap adıyla katalogda" → 3.3
  - "İçindekilerden ekle" / "Fotoğrafını çek, bölümleri biz okuyalım" → 3.6
  - "Hızlı ekle" / "Katalogda yoksa: ad ve sayfa ya da test sayısı" → 3.5
  - "YouTube listesi" / "Ders oynatma listesinin linkini yapıştır" → 3.8
- **Durumlar:** tek durum. Kilitli seçenekler (içindekiler, YouTube) burada işaretlenmiyor; kilit kendi
  ekranlarında gösteriliyor.
- **Kaynak:** apps/mobile/src/app/book/add.tsx

### 3.2 Barkod okuma

- **İçerik:**
  - **Kamera izni yok:** düz ekran, "Barkodu okutmak için kamera izni gerekiyor.", birincil "İzin ver",
    yazı düğmesi "ISBN'i elle yaz".
  - **Kamera açık:** tam ekran kamera görüntüsü (siyah zemin). Altta beyaz yazı "Barkodu çerçeveye getir" ve
    ikincil düğme "ISBN'i elle yaz". Not: bugün ekranda çizili bir çerçeve **yok**; yazı çerçeveden söz
    ediyor.
- **Eylemler:** geçerli ISBN okununca kendiliğinden Katalog arama açılır (ISBN yazılmış olarak). "ISBN'i elle
  yaz" → Katalog arama (boş).
- **Kısıtlar:** görüntü kaydedilmez; yalnız barkod numarası okunur.
- **Kaynak:** apps/mobile/src/app/book/scan.tsx

### 3.3 Katalogda ara

- **İçerik:**
  - Başlık "Katalogda ara"
  - Arama alanı, ipucu "ISBN ya da ad (ör. 3 Adım TYT Tarih)" (barkoddan gelindiyse ISBN dolu; değilse klavye
    kendiliğinden açılır)
  - Sonuç kartları: başlık "{seri} · {sınav} {ders}" (örn. "3 Adım · TYT Tarih"), gri açıklama
    "{yayınevi} · {n} sayfa"
- **Durumlar:**
  - Boş arama: sonuç yok, mesaj yok.
  - Katalog yükleniyor: gösterge yok (sonuçlar geç gelir).
  - Sonuçlar listesi (sıra: TYT, AYT, YDT; sonra ders).
  - Bir ISBN birden çok kitapta ortaksa listenin üstünde gri: "Bu barkod birden çok kitapta ortak; dersini seç."
  - Sonuç yok: gri "Katalogda bulunamadı. Hızlı ekleyebilirsin." ve çerçeveli "Hızlı ekle".
  - Katalog yüklenemedi: kırmızı "Katalog yüklenemedi. İnternet bağlantını kontrol et ya da hızlı ekle." ve
    çerçeveli "Hızlı ekle".
- **Eylemler:** sonuç kartı → Baskı ayrıntısı (3.4). "Hızlı ekle" → Hızlı ekle (3.5, bu ekranın yerine).
- **Kaynak:** apps/mobile/src/app/book/search.tsx

### 3.4 Baskı ayrıntısı

- **Ne için:** katalogdaki kitabı onaylayıp sayfa başı süreyi seçmek.
- **İçerik** (Adım ekranı düzeni, adım etiketi yok):
  - Başlık "{seri} · {sınav} {ders}", gri alt başlık yayınevi
  - "{n} bölüm · {n} sayfa"; bölümler gelene kadar "Bölümler yükleniyor…"
  - Kalın "Bir sayfa ortalama kaç dakikanı alıyor?" ve yan yana 4 kutu: "2 dk", "3 dk" (varsayılan),
    "5 dk", "8 dk"
  - Alt düğme "Kütüphaneme ekle"
- **Durumlar:** kitap bilgisi gelene kadar ekran boş. Bölümler gelmeden ya da bölüm yoksa düğme pasif.
- **Eylemler:** "Kütüphaneme ekle" → Kütüphane sekmesi.
- **Kısıtlar:** katalogda yalnız olgu bilgisi (bölüm, sayfa aralığı) var; içindekiler metni ya da sayfa
  görüntüsü gösterilmez.
- **Kaynak:** apps/mobile/src/app/book/edition.tsx

### 3.5 Hızlı ekle

- **İçerik** (Adım ekranı düzeni):
  - Başlık "Hızlı ekle"
  - Kalın "Kitabın adı", metin alanı ipucu "Ör. X Yayınları TYT Fizik"
  - Kalın "Neyle ilerleyeceksin?", yan yana 2 kutu "Sayfa" (varsayılan), "Test"
  - Kalın "Toplam sayfa" ya da "Toplam test", sayı alanı
  - Kalın "Bir sayfa ortalama kaç dakikanı alıyor?" ya da "Bir test ortalama kaç dakikanı alıyor?", yan yana
    4 kutu: sayfa için "2 dk" "3 dk" "5 dk" "8 dk" (varsayılan 3); test için "10 dk" "15 dk" "20 dk" "30 dk"
    (varsayılan 15). Tür değişince süre varsayılana döner.
  - Alt düğme "Ekle"
- **Durumlar:** ad 2-80 karakter ve sayı 1-2000 değilse düğme pasif. Hata mesajı gösterilmiyor.
- **Eylemler:** "Ekle" → Kütüphane sekmesi.
- **Kaynak:** apps/mobile/src/app/book/quick.tsx

### 3.6 İçindekilerden ekle

- **İçerik:**
  - Başlık "İçindekilerden ekle"
  - Gri: "Kitabının içindekiler sayfasının fotoğrafını çek; bölümleri ve sayfaları biz okuyalım, sen kontrol et.
    Fotoğraf okunduktan sonra silinir."
- **Durumlar:**
  - **Kilitli, veli onayı yok:** "Velin onay verene kadar fotoğraf yükleme kapalı. Hızlı ekleyebilirsin."
    Düğme yok (geri ile çıkılır).
  - **Kilitli, hesap yok:** "Fotoğrafla eklemek için önce hesabını bağla (Ayarlar)." ve çerçeveli
    "Hesap bağla" → Hesap bağla.
  - **Hazır:** birincil "Fotoğraf çek", çerçeveli "Galeriden seç".
  - **Okunuyor:** dönen gösterge ve "Okunuyor… (10 saniye kadar)".
  - **Hata** (kırmızı, düğmelerin altında):
    - "Kamera izni olmadan fotoğraf çekemeyiz."
    - "Bugünlük fotoğraf hakkın doldu; yarın tekrar dene ya da hızlı ekle."
    - "Sayfa okunamadı. Işığı ve açıyı düzeltip tekrar dene."
    - "Bağlantı kurulamadı. İnternetini kontrol et."
- **Eylemler:** fotoğraf seçilince okunur; başarılıysa İçindekiler kontrolü bu ekranın yerine açılır.
  Fotoğraf seçimi iptal edilirse hiçbir şey olmaz.
- **Kısıtlar:** fotoğraf saklanmaz, gösterilmez, önizlemesi yok. 18 altında onaya kadar kapalı.
- **Kaynak:** apps/mobile/src/app/book/toc.tsx

### 3.7 İçindekiler kontrolü

- **Ne için:** okunan bölüm başlıklarını ve başlangıç sayfalarını öğrencinin düzeltmesi.
- **İçerik** (Adım ekranı düzeni):
  - Başlık "Kontrol et", alt başlık "Başlangıç sayfalarını kitapla karşılaştır; yanlışsa düzelt."
  - Kalın "Kitabın adı" ve boş metin alanı
  - Her bölüm için bir satır: geniş metin alanı (bölüm adı) + dar sayı alanı (başlangıç sayfası). Sorunlu
    satırın sayı alanı kırmızı çerçeveli.
  - Sorun satırı (kırmızı): "Sayfa sırası bozuk" ya da "Sayfa eksik"
  - Kalın "Son bölüm hangi sayfada bitiyor?" ve dar sayı alanı
  - Kalın "Bir sayfa ortalama kaç dakikanı alıyor?" ve 4 kutu ("2 dk" "3 dk" "5 dk" "8 dk", varsayılan 3)
  - Alt düğme "Kütüphaneme ekle"
- **Durumlar:** ad, sayfalar ve son sayfa tutarlı olmadan düğme pasif. Satır ekleme/silme düğmesi yok.
- **Eylemler:** "Kütüphaneme ekle" → Kütüphane sekmesi.
- **Kısıtlar:** bölüm adları yalnız bu öğrencide kalır, paylaşılmaz.
- **Kaynak:** apps/mobile/src/app/book/toc-review.tsx

### 3.8 YouTube listesi ekle

- **Durum A, kilitli** (Adım ekranı düzeni):
  - Başlık "YouTube listesi ekle"
  - Onay yok: "YouTube listesi eklemek velinin onayından sonra açılır." Alt düğme "Veli onayı iste" → Veli onayı.
  - Hesap yok: "YouTube listesi eklemek için hesabını bağla; liste sunucudan getirilir." Alt düğme
    "Hesap bağla" → Hesap bağla.
- **Durum B, link girme:**
  - Başlık "YouTube listesi ekle", alt başlık "Ders oynatma listesinin linkini yapıştır. Videolar planına sırayla
    girer."
  - Kalın "Liste linki", alan ipucu "https://www.youtube.com/playlist?list=…"
  - Alt düğme "Listeyi getir" (link bir oynatma listesi linki değilse pasif)
- **Durum C, getiriliyor:** dönen gösterge ve gri "Liste getiriliyor…"; düğme pasif.
- **Durum D, hata** (kırmızı):
  - "Bu bir YouTube oynatma listesi linki değil."
  - "Liste bulunamadı ya da gizli."
  - "Listede izlenebilir video yok."
  - "Bugünkü liste ekleme hakkın doldu; yarın tekrar dene."
  - "Liste ekleme velinin onayından sonra açılır."
  - "YouTube'a şu an ulaşılamıyor; biraz sonra tekrar dene."
  - "Liste getirilemedi; internet bağlantını kontrol et."
- **Durum E, önizleme:**
  - Çerçeveli kart: kalın liste adı, gri kanal adı, "{n} video · toplam {süre}", **"▶ YouTube"** etiketi;
    listede çocuklara özel video varsa gri "Bu listede "çocuklara özel" işaretli videolar var."
  - Kalın "İzleme hızı", yan yana 4 kutu "1×" (varsayılan), "1,25×", "1,5×", "2×"
  - Kalın "Not alma payı", gri "Durdurup not almak için videoya eklenen süre.", 3 kutu "%0", "%25"
    (varsayılan), "%50"
  - Alt düğme "Kütüphaneme ekle"
- **Eylemler:** "Listeyi getir" → C, sonra D ya da E. Link değiştirilirse önizleme kaybolur, B'ye döner.
  "Kütüphaneme ekle" → Kütüphane sekmesi.
- **Kısıtlar:** YouTube kaynağı açıkça görünür; küçük resim (thumbnail) yok; liste bilgisi en fazla 30 gün
  tutulur. Video izleme ücretli duvarın arkasına konmaz.
- **Kaynak:** apps/mobile/src/app/book/youtube.tsx

---

## 4. Check-in

Bugün'deki görev kartından açılır; bitince Bugün'e dönülür ve kart sonuç durumuna geçer.

### 4.1 Yarım kaldı

- **Nereden:** kitap kartında "Yarım kaldı".
- **İçerik** (Adım ekranı düzeni):
  - Başlık "Nereye kadar geldin?"
  - Tek sayaç satırı: solda aralık ("s. 41-58" ya da "Test 3-5"), ortada değer "{n}. sayfaya kadar" ya da
    "{n}. teste kadar", − ve +. Başlangıç değeri aralığın ortası; en az ilk sayfa, en çok sondan bir önceki.
  - "Devam"
- **Eylemler:** Devam → Ne oldu? (yarım bilgisiyle).
- **Kaynak:** apps/mobile/src/app/checkin/partial.tsx

### 4.2 Ne oldu?

- **Nereden:** kartta "Yapamadım"/"İzleyemedim" ya da Yarım kaldı ekranından.
- **İçerik** (Adım ekranı düzeni):
  - Başlık "Ne oldu?", alt başlık "Planı buna göre ayarlayacağız. Yargı yok."
  - Alt alta 4 seçim kartı: "Zaman yetmedi", "Konu zor geldi", "İsteksizim", "Kötü hissediyorum"
  - Alt düğme "Kaydet" (seçim yoksa pasif)
- **Eylemler:** Kaydet → Bugün. Kartta sonuç ve planın yaptığı gösterilir:
  - Zaman yetmedi: "Kalan kısmı sonraki günlere dağıttık. Üç gün üst üste olursa günlük yükünü azaltacağız."
  - Konu zor geldi: "Bu bölüme daha çok zaman ayırdık."
  - İsteksizim: "Yarın en kısa görevle başlayacaksın."
  - Kötü hissediyorum: "Önümüzdeki üç gün yükün yarıya indi." + kartta "Destek" düğmesi; ertesi günden itibaren
    Bugün'de hafif mod bandı.
- **Kısıtlar:** yargısız dil. "Kötü hissediyorum" seçimi plan yükünü azaltır ve desteğe yol açar; kriz
  değerlendirmesi değildir.
- **Kaynak:** apps/mobile/src/app/checkin/reason.tsx

---

## 5. Hesap ve veli onayı

### 5.1 Hesap bağla / Hesabına giriş yap

- **Nereden:** Ayarlar "Hesap bağla"; Koç (kilitli); İçindekilerden ekle (kilitli); YouTube (kilitli);
  Veli onayı (onay geldi); Karşılama "Hesabım var, geri yükle" (geri yükleme modu).
- **Ne için:** e-posta ve tek kullanımlık kodla giriş; yedekleme ve sunucu özelliklerini açmak.
- **İçerik** (Adım ekranı düzeni, iki aşama):
  - Başlık: "Hesap bağla" ya da geri yüklemede "Hesabına giriş yap"
  - **Aşama 1, e-posta:**
    - Kalın "E-posta adresin", alan ipucu "ornek@eposta.com"
    - Onay kartı (bugün seçim kartı görünümünde, aç/kapa çalışır; onay kutusu gibi tasarlanabilir):
      "Planımın ve ilerlememin yedeklenmek için Supabase'in Frankfurt (AB) sunucularında saklanmasını kabul
      ediyorum." altında gri "Aydınlatma metni hazırlanıyor (taslak)."
    - Alt düğme "Kod gönder" (e-posta geçerli ve onay işaretli değilse pasif)
  - **Aşama 2, kod:**
    - Kalın "{e-posta} adresine gelen 6 haneli kodu yaz"
    - Ortalanmış, harf aralıklı 6 haneli kod alanı (telefonun kod otomatik doldurması açık)
    - Alt düğme "Doğrula" (6 hane olmadan pasif)
  - Hata satırı (kırmızı): "Olmadı; kodu kontrol edip tekrar dene." (kod gönderilemediğinde de bu metin çıkıyor)
- **Durumlar ve eylemler:**
  - Hesap bağlama başarılı → önceki ekrana döner.
  - Geri yükleme başarılı → Bugün.
  - Geri yüklemede hesapta plan yok → kurulum Adım 1'e geçer. "Bu hesapta kayıtlı plan yok; kuruluma
    başlayalım." metni koda yazılmış ama ekran hemen değiştiği için büyük olasılıkla görünmüyor (**belirsiz**).
  - Onaylı 18 altı, yanlış hesapla girerse (ör. velinin adresi): oturum kapanır, Aşama 1'e döner, hata
    "Velinin onayı bu hesaba bağlanamadı. Kendi e-posta adresinle giriş yap (velinin adresiyle değil)."
  - İşlem sürerken düğme pasif; ayrı gösterge yok.
  - Bugün **yok**: "Kodu yeniden gönder" ve e-postayı değiştirme düğmesi (metni var, ekranda kullanılmıyor).
    Kodu yeniden istemek için geri çıkıp girmek gerekiyor.
- **Kısıtlar:** 18 altı onay gelmeden hesap bağlayamaz (bu ekrana giden düğmeler gizli). Yer tutucu rıza
  metni yayından önce avukat metniyle değişecek.
- **Kaynak:** apps/mobile/src/app/account/sign-in.tsx

### 5.2 Veli onayı

- **Nereden:** Bugün bandı, Ayarlar, Koç (kilitli), YouTube (kilitli) "Veli onayı iste".
- **Ne için:** 18 altı öğrencinin velisine onay linki göndermesi ve durumu izlemesi.
- **Durum A, form** (henüz istek yok; "Yeni link oluştur"a basıldı; link süresi doldu; onay geri çekildi).
  Adım ekranı düzeni:
  - Başlık "Veli onayı"
  - Alt başlık: "18 yaşından küçük olduğun için sohbet, fotoğrafla kitap ekleme ve yedekleme velinin onayından
    sonra açılır. O zamana kadar planın yalnız bu telefonda çalışır."
  - Koşullu bilgi satırı:
    - Geri çekildiyse: "Velin onayını geri çekti. Sunucudaki yedeğin silindi; planın bu telefonda çalışmaya
      devam ediyor. İstersen yeniden onay isteyebilirsin."
    - Süre dolduysa: "Linkin süresi doldu; yeni bir link oluştur."
  - Kalın "Velinin e-posta adresi", alan ipucu "ornek@eposta.com", gri "Velin onay sayfasında bu adrese gelen
    kodla doğrulama yapacak. Sunucuya yalnız bu adres gider."
  - Hata (kırmızı): "Link oluşturulamadı; internet bağlantını kontrol et."
  - Alt düğme "Onay linki oluştur" (e-posta geçersizse ya da işlem sürüyorsa pasif)
- **Durum B, link hazır / bekleniyor:**
  - Başlık "Link hazır"
  - "Linki veline gönder. Velin sayfayı açıp {veli e-postası} adresiyle onay verince burada görünür. Link 7 gün
    geçerli."
  - Link metni (küçük, gri, seçilip kopyalanabilir)
  - Birincil "WhatsApp'tan gönder" → WhatsApp, hazır mesajla
  - Çerçeveli "Başka yolla paylaş" → sistem paylaşım menüsü
  - Çerçeveli "Durumu kontrol et"; hâlâ bekliyorsa altında gri "Henüz onay gelmedi."
  - Hata (kırmızı): "Link oluşturulamadı; internet bağlantını kontrol et." (durum sorgusu başarısız olunca da bu
    metin çıkıyor)
  - Yazı düğmesi "Yeni link oluştur" → A
  - Hazır mesaj: "YKS AI Koç'u kullanmak için onayına ihtiyacım var. Bu linkten açıklamayı okuyup onay
    verebilirsin: {link}" (eski çalışma adı geçiyor)
- **Durum C, onay geldi:**
  - Başlık "Velin onay verdi", "Artık hesabını bağlayıp planını yedekleyebilirsin.", birincil "Hesap bağla" →
    Hesap bağla (bu ekranın yerine).
- **Arka plan:** onay durumu uygulama açılınca ve öne gelince kendiliğinden sorulur; onay gelince Bugün bandı
  ve kilitler kendiliğinden kalkar.
- **Kısıtlar:** onay gelmeden öğrencinin verisi sunucuya gitmez; sunucuya yalnız velinin e-postası gider.
  Öğrenci onayı kendisi veremez; veli web sayfasında kodla doğrular.
- **Kaynak:** apps/mobile/src/app/account/consent.tsx

---

## 6. Destek

### 6.1 Destek

- **Nereden:** Ayarlar "Destek"; Bugün hafif mod bandı "Destek"; "Kötü hissediyorum" seçilmiş kart "Destek";
  Koç'ta akut risk yanıtından sonra **kendiliğinden** ya da "Destek ekranını aç".
- **Ne için:** zor bir anda ücretsiz hatlar, güvendiği birine haber verme ve planı birkaç gün hafifletme.
- **İçerik:**
  - Başlık "Destek"
  - Giriş metni: "Zor bir an yaşıyor olabilirsin. Bunu biriyle paylaşmak işe yarar. Aşağıdaki hatlar ücretsiz;
    güvendiğin bir yetişkine ya da rehber öğretmenine de haber verebilirsin."
  - Küçük gri taslak notu (uzman onayına kadar): "Taslak metin: uzman onayından önce yayına çıkmaz."
  - Kalın "Ücretsiz hatlar"; her hat için birincil düğme ve altında gri açıklama:
    - "112 Acil Çağrı" / "Hemen tehlikedeysen ya da biri tehlikedeyse."
    - "ALO 183 Sosyal Destek Hattı" / "Şiddet, istismar ya da zor bir durum için; ücretsiz."
  - Arama açılamazsa kırmızı: "Arama açılamadı. {numara} numarasını elle arayabilirsin."
  - Çerçeveli "Velime ya da rehberime haber ver" ve gri "Kendi telefonundan, seçtiğin kişiye kısa bir mesaj
    gönderirsin. Uygulama kimseye bir şey göndermez."
  - Hafifletme:
    - Kapalıyken: çerçeveli "Planımı birkaç gün hafiflet" ve gri "Bugün ve sonraki üç gün yükün yarıya iner,
      koç daha yumuşak konuşur."
    - Açıkken (düğmenin yerine) renkli zeminli band: "Hafif mod açık. Planın birkaç gün yarı yarıya."
- **Eylemler:**
  - Hat düğmesi → telefonun arama ekranı açılır.
  - "Velime ya da rehberime haber ver" → sistem paylaşım menüsü, hazır mesaj: "Merhaba, şu an zor bir an
    yaşıyorum ve biriyle konuşmaya ihtiyacım var. Müsait olunca bana ulaşabilir misin?"
  - "Planımı birkaç gün hafiflet" → güvenli mod hemen açılır; Bugün'de hafif mod bandı çıkar.
- **Durumlar:** hafif mod kapalı/açık; arama hatası; taslak notu (PDR onayından sonra kalkar).
- **Kısıtlar:**
  - Hesap ya da veli onayı gerekmez; 18 altında onaydan önce de açılır. Sunucuya bir şey gitmez.
  - Metinler sabit; yapay zekâ üretmez. PDR danışmanı onaylamadan yayın yok. Tasarım metni değiştirmez,
    sakin ve okunur sunar; numaralar büyük ve tek dokunuşla aranabilir.
  - Veliye otomatik bildirim yok; haber vermeyi öğrenci kendisi seçer.
- **Kaynak:** apps/mobile/src/app/support/index.tsx, packages/safety/src/texts.ts

---

## 7. Veli web sayfaları

Telefonda ya da bilgisayarda tarayıcıda açılır; tek sütun, dar (en çok ~600 px) düzen. Sayfa başlığında
bugün eski ad var ("Veli onayı · YKS Koç", "Haftalık rapor · YKS Koç"). Linkler gizli bir kod taşır; arama
motorlarına kapalıdır.

### 7.1 Veli onayı sayfası

- **Nereden:** öğrencinin WhatsApp ya da paylaşım menüsüyle gönderdiği link.
- **Ne için:** velinin aydınlatma metnini okuyup rızalarını ayrı ayrı vermesi, e-posta koduyla doğrulaması;
  sonradan onayı geri çekebilmesi.
- **İçerik:** üstte başlık "Veli onayı", altında duruma göre:
- **Yükleniyor:** gri "Yükleniyor…"
- **Geçersiz link:** "Bu link geçersiz. Öğrenciden uygulamadan yeni bir link isteyin."
- **Süresi dolmuş:** "Bu linkin süresi dolmuş. Öğrenciden uygulamadan yeni bir link isteyin."
- **Geri çekilmiş:** "Onay geri çekildi. Öğrencinin sunucudaki verisi silindi."
- **Bekliyor (ana form):**
  1. Gri giriş: "Çocuğunuz YKS AI Koç'u kullanmak için onayınızı istiyor. Lütfen aşağıdaki açıklamayı okuyun."
  2. Gri zeminli kutu, kalın "Aydınlatma metni (taslak)" ve 4 paragraf:
     - "YKS AI Koç, öğrencinin kendi kitaplarına göre günlük çalışma planı çıkaran bir uygulamadır. 18 yaşından
       küçük kullanıcıların verisi, veli onayı gelmeden sunucularımıza gönderilmez; o süre boyunca plan yalnız
       öğrencinin telefonunda çalışır."
     - "Onay verirseniz: öğrencinin planı, kitap listesi ve günlük check-in kayıtları yedek amacıyla
       Supabase'in Frankfurt (AB) sunucularında saklanır. Sohbet mesajları ve kitap içindekiler fotoğrafları,
       ad, e-posta, telefon, okul ve şehir bilgileri ayıklandıktan sonra yanıt üretmek için Anthropic'in (ABD)
       Claude modeline gönderilir. İçindekiler fotoğrafları saklanmaz."
     - "Sohbet içeriği hiçbir zaman velilere gösterilmez. Haftalık veli raporu yalnız çalışma günlerini, kitap
       ilerlemesini ve seriyi içerir."
     - "Onayınızı bu sayfadan istediğiniz zaman geri çekebilirsiniz. Geri çekildiğinde öğrencinin sunucudaki
       hesabı ve verisi silinir; onay kayıtları (metin sürümü, zaman, doğrulama özeti) ispat için saklanır."
  3. Onay kutusu (zorunlu, işaretsiz başlar): "Öğrencinin verisinin yukarıda anlatıldığı şekilde saklanmasına
     ve AI sohbet ile içindekiler okuma için yurt dışına (Anthropic, ABD) aktarılmasına açık rıza veriyorum."
  4. Onay kutusu (isteğe bağlı, işaretsiz başlar): "Öğrencinin haftalık çalışma özetinin bu e-posta adresine
     gönderilmesine açık rıza veriyorum (isteğe bağlı)."
  5. Alan "Adınız ve soyadınız"
  6. Alan "E-posta adresiniz ({maskeli ipucu})": öğrencinin yazdığı adresin kısmen gizli hâli gösterilir
     (biçimi sunucuda belirleniyor, kodda görünmüyor).
  7. Tam genişlik koyu düğme "Doğrulama kodu gönder" (e-posta geçerli, ilk kutu işaretli ve ad en az 2
     karakter değilse soluk)
  8. Kod gönderilince: e-posta alanı kilitlenir; yeni alan "E-postanıza gelen 6 haneli kod"; düğme
     "Onay veriyorum" (6 hane olmadan soluk)
  9. Hata satırı (kırmızı):
     - "Bu e-posta adresi, öğrencinin onay isteğinde yazdığı adresle eşleşmiyor."
     - "Linkin süresi dolmuş. Öğrenciden yeni bir link isteyin."
     - "Bu istek için zaten karar verilmiş."
     - "Bir sorun oldu; lütfen tekrar deneyin." (yanlış kod dahil diğer her şey)
- **Onay verilmiş:** "Onay verildi. Haftalık rapor: açık." (ya da "kapalı.") ve altı çizili yazı bağlantısı
  "Onayı geri çekmek istiyorum". Basınca aynı e-posta + kod formu açılır; son düğme "Onayı geri çek".
  Başarılıysa sayfa "Geri çekilmiş" durumuna geçer.
- **Kısıtlar:** rızalar ayrı ayrı; önceden işaretli kutu yok; aydınlatma metni okunur yerde; kod doğrulaması
  görünür. Metinler taslak; avukat metniyle değişecek. Haftalık rapor rızası sonradan ayrıca değiştirilemiyor
  (yalnız tüm onay geri çekilebiliyor).
- **Kaynak:** apps/web/src/app/onay/[token]/page.tsx, consent-form.tsx, apps/web/src/lib/consent-text.ts

### 7.2 Haftalık rapor sayfası

- **Nereden:** öğrencinin "Haftalık raporu velime gönder" ile WhatsApp'tan paylaştığı link.
- **Ne için:** velinin haftalık çalışma özetini görmesi. Sohbet yok.
- **İçerik:**
  1. Başlık "Haftalık rapor"
  2. Gri tarih aralığı: "20 Ekim – 26 Ekim"; hafta bitmediyse "(24 Ekim itibarıyla)" eki
  3. **7 günlük şerit**: her gün için kısa ad ("Pzt" "Sal" "Çar" "Per" "Cum" "Cmt" "Paz") ve altında kutu:
     - Tamamlanan gün: "✓", yeşil dolu
     - Planlı ama tamamlanmamış: "–", gri
     - Planlı değil: "·", çok soluk
  4. Haftanın notu (büyük yazı), sayılardan kuralla seçilir:
     - "Bu hafta için planlanmış çalışma günü yok."
     - "Planlanan her günü tamamladı."
     - "Bu hafta planı tutturamadı. Uygulama planı, verdiği nedenlere göre yeniden ayarlıyor."
     - "Planlanan {n} günün {m} tanesini tamamladı."
  5. **3 sayı kutusu** yan yana:
     - "Tamamlanan gün": "{m}/{n}"
     - "Çalışma": "{süre}" ve altında küçük "plan: {süre}"
     - "Seri": "{n} gün"
  6. **Kitaplar** (en az bir kitap varsa): başlık "Kitaplar"; her kitap için ad ve sağda "%{n}", ilerleme çubuğu,
     altında küçük "Bu hafta {n} sayfa" ("test", "video" de olabilir)
  7. Alt not (küçük gri): "Rapor uygulamadaki plan ve check-in kayıtlarından hesaplanır. Öğrencinin AI koçla
     konuşmaları raporda hiçbir zaman yer almaz."
- **Durumlar:** yükleniyor ("Yükleniyor…"); geçersiz ya da süresi dolmuş link ("Bu link geçersiz ya da süresi
  dolmuş. Öğrenciden uygulamadan yeni bir link isteyin."); kitapsız hafta (Kitaplar bölümü yok). Sunucu hatası
  için özel bir ekran yok (**belirsiz**: genel hata sayfasına düşüyor olabilir).
- **Kısıtlar:** sohbet içeriği, mesaj sayısı, alıntı yok. Doğru/yanlış sayıları ve "kötü hissediyorum" gibi
  nedenler raporda yok. Not yargısız dilde. Yeşil "tamamlandı" rengi marka paletinde yok; yeniden tasarlanmalı.
- **Kaynak:** apps/web/src/app/rapor/[token]/page.tsx

---

## 8. Bir kez tasarlanacak ortak bileşenler

### Yapı

- **Sekme çubuğu:** 4 sekme (Bugün, Kütüphane, Koç, Ayarlar); seçili/seçili değil.
- **Üst çubuk:** başlıksız, yalnız geri oku. Sekme ekranlarında yok.
- **Sekme ekranı başlığı:** büyük başlık + isteğe bağlı gri alt satır (Bugün'de tarih, geri sayım, seri).
- **Adım ekranı:** isteğe bağlı "Adım {n}/6", başlık, isteğe bağlı gri alt başlık, kaydırılan içerik, altta
  klavyenin üstüne yapışan tam genişlik birincil düğme; isteğe bağlı ikinci yazı düğmesi ("Şimdilik geç").
  Kurulumda, kitap ekleme formlarında, check-in'de, hesap ve onay formlarında kullanılıyor. Kurulum için
  ilerleme göstergesi tasarlanabilir.

### Girdi ve seçim

- **Seçim kartı:** başlık + isteğe bağlı gri açıklama; seçili/seçili değil; basılı. Dört kullanım:
  - Tam genişlik alt alta liste (sınıf, alan, neden, katalog sonuçları)
  - Izgara (ay 3 sütun, yıl 4 sütun, sabah saati 4 sütun)
  - Eşit genişlikte yan yana 2-4 kutu (sıralama/puan, sayfa/test, dakika, izleme hızı, not payı)
  - Gezinme kartı, seçim yok (Ekleme yolu seçimi)
  - Aç/kapa onay (Hesap bağla'daki rıza); onay kutusu olarak tasarlanması daha doğru
- **Sayaç:** etiket, − düğmesi, değer, + düğmesi; sınırda pasif uç.
- **Metin alanı:** tek satır büyük; sayı (ortalı); 6 haneli kod (ortalı, aralıklı); URL; çok satırlı sohbet
  alanı; sorunlu alan (bugün kırmızı çerçeve). İpucu yazısı rengi.
- **Satır içi hata metni** (bugün kırmızı küçük yazı; marka kuralına göre renksiz bir işaretle yeniden
  tasarlanmalı).

### Düğmeler

- Birincil (dolu), çerçeveli, ikincil (yalnız barkod ekranında, kamera üstünde), yazı düğmesi (ghost),
  yıkıcı ("Verilerimi sil"), yıkıcı yazı düğmesi ("Kaldır").
- Boyutlar: küçük (kart içi), normal, büyük (Başla, Planımı kur), ikon (sayaç).
- Durumlar: normal, basılı, pasif (bugün %50 saydam), meşgul (metin değişir: "Gönderiliyor…").

### Bilgi ve durum blokları

- **Bilgi bandı + küçük düğme:** veli onayı bandı, hafif mod bandı.
- **Bilgi kutusu:** Hazırsın'daki "Veli onayı gerekecek" kutusu; Destek'teki "Hafif mod açık" bandı.
- **Kilitli durum:** başlık, açıklama, tek eylem ("Veli onayı iste" ya da "Hesap bağla"). Koç, İçindekilerden
  ekle, YouTube listesi ekranlarında aynı kalıp. Suçlayıcı değil, bilgilendirici.
- **Boş durum:** Bugün kitap yok kutusu, Bugün dinlenme / iş kalmadı satırı, Kütüphane boş.
- **Yükleniyor:** dönen gösterge + metin; ayrıca ekranların boş beklediği yerler için iskelet.
- **Uyarı satırı:** Bugün'deki fazla yük / sığmayan bölüm uyarıları.

### Plan ve kütüphane

- **Görev kartı**, varyantlar:
  - Tür: sayfa, test, video
  - Check-in: bekliyor (2 ya da 3 düğme), tamamlandı / izlendi, yapılmadı + neden + etki, yarım + neden + etki,
    "Kötü hissediyorum" + Destek düğmesi
  - Video: bilgi var / "Video bilgisi yenileniyor"; "YouTube'da aç" var/yok
- **YouTube etiketi:** "▶ YouTube" (video kartı, liste önizlemesi). Resmi YouTube marka kurallarına göre
  değişecek; her zaman görünür.
- **Doğru/yanlış formu** ve kaydedildi satırı.
- **Kütüphane kartı:** ad, özet (kitap / liste / liste süresi geçti), ilerleme çubuğu, yüzde, Kaldır.
- **Rapor paylaşma bloğu:** çerçeveli "Haftalık raporu velime gönder" (basınca WhatsApp açılır, hazır mesaj
  "Bu haftaki çalışma raporum: {link}"), altında seçilebilir link metni, hata satırı ("Velin haftalık rapora izin
  vermedi." / "Rapor linki alınamadı; internet bağlantını kontrol et."). Bugün'de yalnız pazar, Ayarlar'da her
  gün; ikisinde de yalnız hesap bağlı ve veli rapora izin vermişse.

### Sohbet

- **Öğrenci balonu** (sağ, dolu) + "Gönderilemedi · Tekrar dene"
- **Koç balonu** (sol, gri) + "Bildir" / "Bildirildi, teşekkürler"
- **Akut yanıt balonu** + "Destek ekranını aç" düğmesi
- **Giriş çubuğu:** çok satırlı alan + Gönder / Gönderiliyor…; üstünde hata satırı
- Ek, fotoğraf, ses düğmesi **yok**.

### Sistem pencereleri (yalnız içerik)

- Kaldırma onayı (Kütüphane), silme onayı (Ayarlar), paylaşım menüsü, kamera/galeri izni. Bunlar sistemin
  kendi görünümünde kalır.

### Web (veli sayfaları)

- Sayfa başlığı, gri bilgi kutusu (aydınlatma metni), onay kutusu satırı, etiketli metin alanı, tam genişlik
  düğme, 7 günlük şerit (3 gün durumu), sayı kutusu, ilerleme çubuğu, alt not.
