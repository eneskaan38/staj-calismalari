# Gün 2 – CSS Temelleri ve Görsel Stil

Gün 1'de kurduğum anlamsal HTML yapısı **hiç değiştirilmedi** (`index.html` birebir aynı).
Bugün sadece `styles.css` yazıldı. JavaScript, framework ve inline stil yok.

## Gün 1 – HTML yapısı (kısa hatırlatma)

`header` (site adı + menü), `main` (3 adet `article`), `aside` (yazar bilgisi) ve `footer`
kullanıldı. Başlık sırası h1 → h2 → h3, `div` kullanılmadı. Meta bilgi için `time` etiketi var.

## CSS nasıl organize edildi?

Dosya 6 bölümden oluşuyor:

1. **Base / Reset**: Kendi yazdığım minimal reset. `box-sizing: border-box`, margin sıfırlama, liste stillerini kaldırma.
2. **Variables**: 5 renk, 5 kademeli boşluk ölçeği, yazı boyutları. Rastgele `17px` gibi değerler yok.
3. **Global Styles**: `body`, `h1–h3`, `p`, `a` ile tipografi.
4. **Layout**: Gün 1'deki Grid düzeni korundu (küçük ekranda alt alta, büyük ekranda `main` + `aside` yan yana).
5. **Sections (Box Model)**: `header`, `main`, `article`, `aside`, `footer` için margin/padding/border.
6. **Components**: Menü, bölüm başlıkları, yazı kartının içi, meta bilgi.

## Bugün pratik ettiğim CSS kavramları

- **Sözdizimi:** `selector { property: value; }`, her kuralın tek bir görevi var.
- **Element seçici:** `body`, `header`, `main`, `article`, `aside`, `h1`, `p`, `a`, `time`.
- **Class seçici:** `.site-footer`, `.post__meta`, `.post__author`, `.section-title`.
- **Descendant seçici:** `header nav a` (header içindeki menü bağlantıları) ve `aside p + p`.
- **Box model:**
  - `padding`: kart ve bölümlerin iç boşluğu
  - `border`: kartların, header'ın ve aside'ın çizgileri
  - `margin`: kartlar arası boşluk (`article` için `margin-bottom`)
  - `box-sizing: border-box`: padding eklenince genişlik taşmasın diye
- **Tipografi:** `body`'de temel yazı tipi ve `line-height: 1.6`, başlıklarda daha sıkı `1.25`.
  Boyutlar bir ölçekten geliyor (2rem / 1.5rem / 1.25rem / 1rem / 0.875rem).
- **Renk ve boşluk sistemi:** CSS değişkenleri (`--color-*`, `--space-*`).
- **Hover durumu:** Menü bağlantıları normalde beyaz zeminli, üzerine gelince vurgu renginde.

## Boşluk ve tipografiye nasıl yaklaştım?

Önce 5 kademeli bir boşluk ölçeği (0.25 / 0.5 / 1 / 1.5 / 2.5 rem) belirledim ve tüm margin/padding
değerlerini bunlardan seçtim. Böylece sayfa tutarlı duruyor. Tipografide `body`'ye temel yazıyı verdim,
başlıkları `rem` ile ölçekledim ve paragraf genişliğini `65ch` ile sınırladım.

## Neyi anlamadım / neyi zorlandım?

Bu görevde en çok seçicileri anlamakta zorlandım. Özellikle `header nav a` gibi iç içe yazılan seçicinin
tam olarak neyi seçtiğini ilk başta kavrayamadım. Sonra bunun "header'ın içindeki menünün içindeki
linkler" demek olduğunu fark ettim.

Margin ile padding'i de karıştırıyordum. Değerleri değiştirip sayfada ne olduğuna bakınca farkı gördüm:
padding kutunun içindeki boşluk, margin ise kutuların arasındaki boşluk.

CSS değişkenleri (`var(--space-3)` gibi) bana yeni geldi. Renkleri ve boşlukları tek yerde toplayınca
sonradan değiştirmenin kolay olduğunu anladım ama kendi başıma sıfırdan yazmakta hâlâ emin değilim.
Ayrıca `box-sizing: border-box`'ın tam olarak neyi çözdüğünü daha iyi oturtmam gerekiyor.
