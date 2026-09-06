# Karbon FPV

FPV yarış ve freestyle drone parçaları satan bir e-ticaret sitesi için arayüz tasarımı. Tek dosyalık, bağımlılıksız statik prototip (`index.html`).

**Canlı:** https://ysfce.github.io/karbon-fpv/
**2D vektör sürümü (karşılaştırma için):** https://ysfce.github.io/karbon-fpv/2d.html

Aynı site iki farklı montaj sahnesiyle duruyor; ikisi de tek dosya, ikisi de aynı içeriği kullanıyor:

| | `index.html` (3D) | `2d.html` (2D) |
| --- | --- | --- |
| Parçalar | Three.js ile mm ölçeğinde katı geometri | Üst üste dizilmiş SVG çizimleri |
| Derinlik | Gerçek perspektif kamera, yörünge hareketi | CSS 3D ile eğilmiş düz düzlemler |
| Işık | Gölge haritalı anahtar ışık + ortam yansıması | Elle çizilmiş gradyan ve spekülar |
| Oturma | Parçalar gerçekten üst üste oturuyor | Katmanlar yaklaşık hizalanıyor |
| Ağırlık | +Three.js (~600 KB, cdnjs) | Ek yük yok |
| Yedek | WebGL yoksa 2D çizimlere düşer | — |

## Ne var

- **Kaydırmalı 3D montaj sahnesi** — ana sayfada pinlenmiş bir WebGL sahnesinde quad adım adım kuruluyor: gövde → motorlar → ESC → uçuş kontrol → VTX → kamera → alıcı & anten → pervaneler → kapak ve batarya. Son adım iki hareketli: gövdenin üst kapağı standoff'lara iner, batarya da onun üstüne oturur (kapak ayrı bir kalem değil, gövde kitinin parçası). Sağdaki montaj listesi doldukça kalkış ağırlığı (AUW) ve sepet toplamı canlı olarak akıyor. En sonda kataloğa giden buton ve "bu build'i sepete ekle" seçeneği var.
- **Yapılandırıcı** (`#/yapilandir`) — sınıf seçilir (5" freestyle / 5" yarış / 7" long range), dokuz yuva sırayla doldurulur. Her seçimde parçalar ikişerli denetlenir ve uyumsuzluğun **nedeni** yazılır: montaj deseni (20×20 / 25,5×25,5 / 30,5×30,5), pervane çapı, hücre sayısı, ESC akım payı (%25 kuralı), dijital VTX + ayrı kamera çakışması. Kalkış ağırlığı ve tutar anlık birikir, sınıfın tipik aralığı aşılırsa uyarır; liste tek tıkla sepete eklenir. Seçimler `localStorage`'da saklanır.
- **Katalog** — 12 kategori, filtre rayı (kategori, marka, boyut, hücre, stack montaj deseni, stok), sıralama, aktif filtre çipleri, arama.
- **Ürün sayfası** — varyant seçimi, adet, teknik özellik tablosu, uyumluluk listesi, kargo/iade sekmesi, uyumlu ürün önerileri.
- **Sepet çekmecesi** — adet güncelleme, ücretsiz kargo ilerleme çubuğu, `localStorage` ile kalıcılık.
- **Rehber** — sınıf/pervane/motor/KV/batarya/AUW uyumluluk tablosu ve üç adımlı build sırası.

## 3D modeller

Parçalar hazır model dosyası değil, `index.html` içinde Three.js (r134, cdnjs'ten) ile **kodla, milimetre ölçeğinde** kuruluyor — 1 birim = 1 mm, Y ekseni yukarı. Ölçüler gerçek parçalardan alındı:

| Parça | Ölçü |
| --- | --- |
| Gövde | 226 mm köşegen, 5 mm kol, 30,5×30,5 stack deseni |
| Motor | 2207 (27,9 mm çan), 36 mm standoff yüksekliği |
| Kartlar | 36×36 mm ESC/FC, 30×30 mm VTX, 1,6 mm PCB |
| Pervane | 5 inç (127 mm), 3 kanat, kökte 27° uca doğru 10° hatve burulması |
| Batarya | 6S 1400 → 34×32×74 mm, üst plakaya kayışlı |

Kanat profili düz bir levha değil: planform şekli extrude edilip her köşe noktası, merkeze olan uzaklığına göre kendi ekseninde döndürülerek gerçek hatve burulması veriliyor. Karşılıklı iki pervane CW, diğer ikisi CCW.

Sahnede tek yönlü anahtar ışık (gölge haritalı), mavi dolgu, turuncu kenar ışığı ve prosedürel bir stüdyo ortamı var; metaller o ortamı yansıtıyor. Malzeme renkleri sRGB'den doğrusala çevriliyor — bu yapılmazsa r134 çıkışta gama uygulayıp bütün yüzeyleri soluk griye çeviriyor.

Modeli incelemek için tarayıcı konsolunda `__karbon3D.apply(0.5)` yazarak montajın herhangi bir anını dondurabilirsiniz (0 = boş gövde, 1 = tamamlanmış quad).

WebGL yoksa ya da kütüphane yüklenmezse sahne sessizce SVG çizimlerine düşer; içerik hiçbir durumda kaybolmaz.

## Tasarım kararları

- Tek taahhütlü koyu dünya: FPV gözlüğünün OSD/telemetri katmanı ve havacılık patlatılmış montaj çizimi.
- Vurgu rengi `#FF5A1F` (hazard turuncu) yalnızca eylem ve aktif katman için; `#3FE0BF` (telemetri turkuazı) yalnızca veri ve stok durumu için.
- Tipografi: Archivo (variable, `wdth` ekseni ile genişletilmiş başlıklar), IBM Plex Sans (gövde), IBM Plex Mono (telemetri, gramaj, fiyat).
- Tüm görseller inline SVG — hiçbir resim dosyası yok, sayfa tek istekte yükleniyor.
- `prefers-reduced-motion`, `prefers-reduced-transparency` ve `prefers-contrast` desteklenir; JavaScript kapalıyken de tüm içerik görünür kalır.

## Gerçek fotoğraf ekleme

Montaj sahnesindeki dokuz parça, kod değişikliği gerektirmeden gerçek fotoğrafla değiştirilebilir. Depoda `parca/` klasörü açıp dosyaları şu adlarla koyun; sayfa dosyayı bulursa vektör çizimin yerine fotoğrafı kullanır, bulamazsa sessizce çizimde kalır:

```
parca/01-govde.png     parca/04-fc.png      parca/07-alici.png
parca/02-motor.png     parca/05-vtx.png     parca/08-pervane.png
parca/03-esc.png       parca/06-kamera.png  parca/09-batarya.png
```

Fotoğrafların katman hâlinde üst üste binmesi için üç kural önemli:

1. **Tam tepeden çekim.** Kamera parçanın tam dikine bakmalı; perspektifli çekimler katmanlar üst üste gelince kaymış görünür.
2. **Şeffaf arka plan, 1600×1600 px kare PNG.** Parça karenin ortasında, kenarlarda yaklaşık %8 boşluk.
3. **Ortak ölçek.** Dokuz fotoğrafın hepsi *aynı* mm/piksel oranıyla kırpılmalı — yani 226 mm'lik gövde kareyi doldururken 36 mm'lik FC kareye göre küçük kalmalı. Aksi hâlde FC gövdeden büyük görünür.

Motor ve pervanede tek parçanın fotoğrafını değil, dördünün doğru köşelere yerleştirildiği tek bir kare hazırlayın (gövde fotoğrafını şablon olarak kullanabilirsiniz).

Ürün kartları ve ürün sayfası için de aynı mantık var: `index.html` içindeki `P` dizisinde bir ürüne `img:'foto/b2.jpg'` alanı eklerseniz kartta ve galeride o fotoğraf görünür, eklemezseniz kategori ikonu kullanılır.

## Shopify eşlemesi

Prototip bir Shopify temasına şu şekilde taşınır:

| Prototipteki bölüm | Shopify karşılığı |
| --- | --- |
| Montaj sahnesi | `sections/build-scroll.liquid` — 9 parça `blocks` ile yönetilir (parça adı, gramaj, ürün referansı) |
| Kategori ızgarası | `sections/collection-list.liquid` |
| Katalog + filtreler | `templates/collection.json` + metafield filtreleri (`montaj_deseni`, `hucre`, `boyut`) |
| Ürün sayfası | `templates/product.json`, varyantlar KV / kapasite / renk olarak |
| Hazır kit "sepete ekle" | çoklu `/cart/add.js` çağrısı |
| Sepet çekmecesi | `snippets/cart-drawer.liquid` + Cart AJAX API |

Ürün verisi `index.html` içindeki `P` dizisinde duruyor; Shopify'a geçerken bu dizi `{{ collection.products }}` döngüsüyle değiştirilir.

## Çalıştırma

Bağımlılık yok. `index.html` dosyasını tarayıcıda açmak yeterli.
