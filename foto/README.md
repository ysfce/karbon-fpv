# Ürün fotoğrafları

Bu klasördeki fotoğraflar ürün sayfası galerisinde, katalog kartlarında ve
sepette kullanılır. Fotoğrafı olan ürünler fotoğrafı gösterir, olmayanlar
3D render'da kalır — ikisi bir arada çalışır.

## Şu an dolu olan ürünler

Ana sayfadaki build'in dokuz parçası (`b1`–`b9`): gövde, motor, ESC,
uçuş kontrol kartı, VTX, kamera, alıcı, pervane, batarya.
Görseller üreticilerin ürün kareleridir; mağaza sahibi bayi olarak
kullanım iznine sahip olduğunu beyan etmiştir. Dosyalar bu depoda
barındırılıyor, dışarıya link verilmiyor.

Kalan ürünler prosedürel 3D render kullanmaya devam ediyor.

## Yeni fotoğraf ekleme

1. Fotoğrafı bu klasöre koyun. Ürün kodunu kullanmak en pratiği:
   `b2-1.jpg`, `b2-2.jpg`, `b2-3.jpg` …
2. `index.json` dosyasına ekleyin:

```json
{
  "b1": ["b1-1.jpg", "b1-2.jpg"],
  "m3": ["m3-1.jpg"]
}
```

3. Kaydedin. Kod değişikliği gerekmez.

Galeri en fazla 4 fotoğraf gösterir. Tam adres de yazabilirsiniz
(`https://cdn.magazaniz.com/...`); `http` ile başlamayan her şey bu
klasöre göre çözülür.

## Ürün kodları

`index.html` içindeki ürün listesinde `id:` alanında. Build parçaları:
`b1` gövde, `b2` motor, `b3` ESC, `b4` uçuş kontrol kartı, `b5` VTX,
`b6` kamera, `b7` alıcı, `b8` pervane, `b9` batarya. Kitler `kit1`–`kit3`.

## Çekim önerisi

- Düz, tek renk arka plan (beyaz en yaygını)
- Kare kadraj, ürün ortada, kenarlarda ~%10 boşluk
- 1200×1200 px yeterli; JPEG kalite 80 civarı
- İlk fotoğraf 3/4 açı olsun — katalog kartında o görünüyor

## Telif

Buraya yalnızca kullanım hakkına sahip olduğunuz görselleri koyun.
Üreticiler genelde bayilerine ayrı bir medya kiti verir; en temizi odur.
Başka bir satıcının kendi çektiği fotoğraflar onların telifindedir.