# Renk token'ları

Uygulamanın bileşenleri doğrudan renk değil **anlamsal adlar** kullanır (`bg-primary`, `text-foreground`).
Yeni tasarım bu adlara eşlenir; böylece geliştirici yalnız tema dosyasını değiştirerek tüm ekranları yeni
kimliğe geçirir. Şu anki geçici tema: [current-theme.css](current-theme.css) (siyah-beyaz yer tutucu).

Aşağıdaki eşleme marka paletinden türetilmiş bir **öneri**dir; tasarım sırasında değişebilir. Değişirse bu
tabloyu güncelle.

| Token | Kullanıldığı yer | Koyu tema (ana kimlik) | Açık tema |
|---|---|---|---|
| `background` | Ekran zemini | gece moru `#1C1330` | krem `#F6EEE0` |
| `foreground` | Ana metin | krem `#F6EEE0` | gece moru `#1C1330` |
| `card` | Görev kartı, panel | koyu yüzey `#2A1F45` | açık yüzey `#FBF6EC` |
| `card-foreground` | Kart içi metin | krem `#F6EEE0` | gece moru `#1C1330` |
| `primary` | Tek ana buton, seçili çip | turuncu `#FF9F43` | gece moru `#1C1330` |
| `primary-foreground` | Ana buton yazısı | gece moru `#1C1330` | krem `#F6EEE0` |
| `secondary` / `muted` / `accent` | İkincil buton, bant, pasif alan | koyu yüzey `#2A1F45` | açık yüzey `#FBF6EC` |
| `muted-foreground` | Açıklama, ipucu | koyu ikincil `#BDB2CF` | açık ikincil `#5C5170` |
| `border` / `input` | Ayırıcı, kenarlık, giriş alanı | koyu çizgi `#3A2D57` | açık çizgi `#D9CCB4` |
| `ring` | Odak halkası | turuncu `#FF9F43` | gece moru `#1C1330` |
| `destructive` | Hata, "Kaldır", "Verileri sil" | **Karar bekliyor** | **Karar bekliyor** |

**`destructive` için not:** marka kılavuzu kırmızıyı yasaklıyor (doğru/yanlış/uyarı renkle verilmez).
Tehlikeli eylemler ve hatalar ikon, metin ve şekille ayrılmalı (ör. çarpı işareti, çerçeveli buton, "Geri
alınamaz" yazısı). Tasarımda bunun nasıl görüneceği belirlenince bu satır doldurulur.

Yazı tipleri: başlık **Bricolage Grotesque**, metin ve butonlar **Source Sans 3** (ikisi de Google Fonts,
açık lisans).
