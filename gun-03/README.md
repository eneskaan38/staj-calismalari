# Gün 3 – CSS Layout ve Responsive Tasarım

Gün 1'deki anlamsal HTML ve Gün 2'deki stil üzerine kuruldu. `index.html` **değiştirilmedi**.
Bugün yalnızca `styles.css` güncellendi. JavaScript, framework ve `position: absolute` kullanılmadı.

## Hangi layout sistemlerini neden kullandım?

**Flexbox: sayfa seviyesi**
HTML değiştirilemediği için ekstra bir sarmalayıcı (`div`) ekleyemedim. Bu yüzden `body`'yi flex konteyner
yaptım; `header`, `main`, `aside` ve `footer` doğrudan flex öğeleri oldu.
- `flex-wrap: wrap` + header/footer için `width: 100%`: header ve footer kendi satırında durur.
- `main` için `flex: 2 1 0`, `aside` için `flex: 1 1 0`: main iki pay, aside bir pay alır.
- `.site-header` içinde `justify-content: space-between` (başlık solda, menü sağda) ve `align-items: center`.
- Küçük ekranda `flex-direction: column` ile alt alta dizilir.

**Grid: içerik seviyesi**
`main` içindeki yazı listesi Grid ile dizildi:
`grid-template-columns: repeat(auto-fit, minmax(12rem, 1fr))`. Ekran genişliğine göre 3, 2 ya da 1 sütun
kendiliğinden oluşur. Başlık (`h2`) `grid-column: 1 / -1` ile tüm genişliği kaplar. Kartlar arası boşluk `gap` ile verildi.

Neden ikisi ayrı? Flexbox tek yönde (satır veya sütun) düzen kurar, sayfanın büyük parçalarını yan yana ya da alt alta
koymak için uygun. Grid ise satır ve sütunu birlikte yönetir, kart listesi için daha uygun.

**Display türleri**
- `block`: `aside` içindeki başlık ve paragraflar
- `inline`: yazar adı (`span`) ve `time`
- `inline-block`: menü bağlantıları (yan yana durur ama padding dikeyde de çalışır)
- `flex`: `body`, `.site-header`, `.site-nav__list`, `.post__meta`
- `grid`: `main`

## Responsive yaklaşım

- **Masaüstü (60rem üstü):** `main` ve `aside` yan yana, yazılar 3 veya 2 sütun (alana göre kendiliğinden).
- **Tablet ve mobil (60rem ve altı):** `body` `flex-direction: column` olur, `aside` `main`'in altına iner, yazılar tek sütun.
- **Küçük telefon (40rem ve altı):** boşluklar azalır, header alt alta dizilir. Menü `flex-wrap` sayesinde sığmazsa alt satıra geçer.
- Yatay kaydırma çıkmaması için `min-width: 0` ve `minmax` kullanıldı. 375px, 800px, 1000px ve 1280px genişliklerinde kontrol ettim.

## Karşılaştığım zorluklar

- HTML değişmeyeceği için ekstra wrapper kullanamadım. Header ve footer'ın tam genişlikte kalıp
  `main` ile `aside`'ın yan yana durması için `flex-wrap` ve `width: 100%` çözümünü kullanmam gerekti.
- Sütun yönünde (`column`) `flex: 2 1 0` değerinin yükseklik gibi davrandığını fark ettim, bu yüzden küçük
  ekranda `main` ve `aside` için `flex: none` ile sıfırlamam gerekti.
- `auto-fit` ve `minmax` ilk bakışta karışık geldi.

## Büyük projede neyi geliştirirdim?

- HTML'e düzenleme izni olsaydı `main` ve `aside` için bir sarmalayıcı eklerdim. Düzen `body` yerine ona ait olurdu.
- Breakpoint değerlerini ve boşlukları değişkenlere taşırdım.
- Kart listesi için bileşen yapısı (React) düşünürdüm.
- Menüyü küçük ekranda daha kompakt göstermek için hamburger menü eklerdim.
