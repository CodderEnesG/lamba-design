# Tasarımda uyulacak kurallar

Bunların bir kısmı ürünün **değişmez kuralları** (hukuk, güvenlik, platform politikaları); tasarım tercihi
değildir, hiçbir gerekçeyle gevşetilmez. Bir kısmı marka kılavuzundan, bir kısmı teknik kısıttır.

## Değişmez ürün kuralları (ekrana yansıyanlar)

- **Soru metni, çözüm ve kitap sayfası görüntüsü yok.** Ne kütüphanede ne sohbette. Sohbete fotoğraf ya da
  dosya ekleme düğmesi konmaz; **sohbet yalnız metin**.
- **İçindekiler fotoğrafı** yalnız okunup silinir; uygulamada saklanmış görüntü, galeri ya da önizleme
  geçmişi gösterilmez.
- **Sohbet içeriği veliye hiçbir yerde görünmez.** Veli raporunda, veli sayfasında mesaj, alıntı ya da sohbet
  sayısı yok. Sohbet ekranında bu söz kullanıcıya verilir ("Yazdıkların velinle paylaşılmaz").
- **18 yaş altı, veli onayı gelmeden:** sohbet, içindekiler fotoğrafı, YouTube listesi ve yedekleme kilitli;
  plan telefonda çalışır. Kilitli durum suçlayıcı değil, bilgilendirici ve "Veli onayı iste" eylemiyle
  tasarlanır.
- **Kriz anı:** akut riskte koç yanıtı yerine **sabit destek metni** ve Destek ekranı (112, ALO 183, güvendiğin
  biri). Bu metin ve düzen PDR danışmanının onayından geçecek; tasarım metni değiştirmez, okunur ve sakin
  sunar. Acil numaralar tek dokunuşla aranabilir, büyük ve net.
- **Güvenli mod:** "kendimi kötü hissediyorum" ya da risk sinyalinden sonra 3 gün: yük yarıya iner, sert ton
  kapanır. Görsel olarak da yumuşak (ör. "Soluk"/"Sakin" duman, Alaaddin "Sakin"), kırmızı ya da alarm dili
  yok.
- **Sert ton davranışa yöneliktir, kişiye değil.** Mikro metinde utandırma, kıyaslama, tehdit yok.
- **YouTube:** video kartında içeriğin YouTube'dan geldiği açıkça görünür (şu an "▶ YouTube" etiketi; resmi
  YouTube logosu ve marka kurallarına göre değiştirilecek) ve kanal adı yazar. Video uygulama içinde
  oynatılmaz, "YouTube'da aç" ile açılır; oynatıcı taklidi, üstüne katman, kapak görüntüsünü değiştirme yok.
  Video izleme hiçbir zaman ödeme duvarının arkasına konmaz.
- **Plan rakamlarını kural motoru üretir;** yapay zekâ sayı uydurmaz. Tasarımda "AI planı" ifadesi yerine
  plan ve koç ayrı tutulur.
- **Veli onay sayfası:** rızalar **ayrı ayrı** işaretlenir (AI sohbet + yurt dışı aktarım zorunlu, haftalık
  rapor isteğe bağlı); önceden işaretli kutu yok. Aydınlatma metni okunur yerde, kod doğrulaması görünür.
- **Hesap ve veri silme** Ayarlar'da bulunur, geri alınamaz olduğu açıkça yazar, onay ister (Apple şartı).

## Marka kılavuzundan (özet; asıl kaynak `brand/kilavuz/`)

- **Palet:** gece moru `#1C1330`, krem `#F6EEE0`, turuncu `#FF9F43`; oran ≈ 60 / 30 / 10. Destek tonları:
  koyu yüzey `#2A1F45`, koyu çizgi `#3A2D57`, koyu ikincil metin `#BDB2CF`; açık yüzey `#FBF6EC`, açık çizgi
  `#D9CCB4`, açık ikincil metin `#5C5170`. Kılavuzda olmayan renk kullanılmaz.
- **Doğru / yanlış / uyarı için renk yok** (yeşil, kırmızı, sarı yok): işaret, metin ve şekille (tik, çarpı,
  "Tekrar bak"). Bu, uygulamadaki şu anki kırmızı hata ve "Kaldır / Verileri sil" butonlarını da kapsar;
  tehlikeli eylemlerin yeni dili tasarımla belirlenecek.
- **Turuncu yalnız gece moru zeminde** (lamba, tek ana buton, önemli vurgu). Krem zeminde turuncu yazı ya da
  çizgi yok (kontrast 1,8:1); açık temada vurgu gece moruyla.
- Gradyan ve şeffaf renk yok (tek istisna "soluk" duman).
- **Yazı:** başlık Bricolage Grotesque, metin ve butonlar Source Sans 3. Marka adı hep küçük harf: **lamba**.
- **Logo:** uygulama içi üst çubukta ya yazı logosu ya simge; ikisi aynı ekranda değil. Logo yeniden
  çizilmez, renklendirilmez, esnetilmez.
- **Alaaddin:** ekranda en fazla bir tane, yanında kısa bir cümle. Kutlama günde en fazla bir kez, gerçek
  dönüm noktalarında. Lambaya yüz çizilmez.
- **Gölge modu:** kılavuz siyah-beyaz bir mod tanımlıyor; uygulamada henüz yok (**ürün kararı bekliyor**). Yine
  de hiçbir bilgi yalnız renkle verilmez: durumlar şekil, ikon ve metinle de ayrılır.

## Erişilebilirlik

- Metin kontrastı kılavuzdaki tabloya uyar (ana metin ≥ 7:1 hedef).
- Dokunma alanı en az 44 × 44 pt. Check-in düğmeleri tek elle, başparmakla rahat.
- Dinamik yazı boyutu büyüdüğünde kartlar taşmaz; uzun Türkçe kelimeler ("İzleyemedim", "Yapamadım") sığar.
- Her ikon düğmenin ekran okuyucu için bir adı var (ör. geri düğmesi "Geri").

## Teknik çerçeve (tasarımın gerçekleşebilir kalması için)

- Uygulama React Native (Expo SDK 58). **Alt sekme çubuğu iOS'un yerel sekme çubuğu** (4 sekme: Bugün,
  Kütüphane, Koç, Ayarlar; SF Symbols ikonları); görünümü sınırlı özelleştirilir (renk, ikon).
- Alt ekranlar yerel yığın gezinmesi: üstte sade başlık ve geri oku.
- Formlarda klavye açıkken alt "Devam" butonu klavyenin üstüne yapışır.
- Bileşenler anlamsal renk adları kullanır (`background`, `foreground`, `card`, `primary`, `muted`,
  `border`, `destructive`…); yeni tasarım bu adlara eşlenir (bkz. [TOKENS.md](TOKENS.md)).
- Animasyon mümkün (Reanimated); duman durumları ve Alaaddin ifadeleri PNG/SVG olarak hazır.
