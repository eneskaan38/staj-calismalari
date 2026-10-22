# Gün 1 – Semantic HTML & CSS Yapısı

"Defter" adında, içerik odaklı bir platformun (blog / bilgi bankası) açılış sayfası.
JavaScript ve CSS framework'ü kullanılmadı. Sadece `index.html` ve `styles.css` var.

## Neden bu HTML yapısını seçtim?

- **`header`**: Platform adı (`h1`) ve ana menü (`nav`) burada. Menüye `aria-label` verdim,
  böylece ekran okuyucular bunun ana menü olduğunu anlıyor.
- **`main`**: Sayfanın asıl içeriği. Sayfada tek bir `main` var.
- **`article` (3 adet)**: Her yazı kendi başına anlamlı: başlık, kısa açıklama ve yazar/tarih bilgisi var.
  Tarih için `time` etiketi kullandım, makine tarafından okunabilen `datetime` değeriyle.
  Meta bilgi, article'ın kendi `footer`'ında duruyor.
- **`aside`**: Ana içerikle doğrudan ilgili olmayan yazar bilgisi. `aria-labelledby` ile başlığına bağlı.
- **`footer`**: Telif bilgisi.
- **Başlık hiyerarşisi**: `h1` (site adı) → `h2` (bölüm başlıkları) → `h3` (yazı başlıkları). Seviye atlanmadı.
- **`div` kullanmadım.** Her öğenin anlamlı bir etiketi vardı, bu yüzden ihtiyaç duyulmadı.

## CSS nasıl organize edildi?

Dosya, istenen 5 bölüme ayrıldı:

1. **Base / Reset**: `box-sizing` ve varsayılan margin/liste stillerinin sıfırlanması.
2. **Variables**: Renkler, boşluk ölçeği (`--space-1` … `--space-5`), yazı tipi ve okunabilir satır
   genişliği (`--measure: 65ch`). Değerler tek yerde durduğu için değişiklik kolay.
3. **Global Styles**: `body`, başlıklar, paragraflar, bağlantılar ve klavye odağı (`:focus-visible`).
4. **Layout**: CSS Grid. `header`, `main`, `aside` ve `footer` doğrudan `body`'nin grid öğeleri.
   Küçük ekranda tek sütun, `60rem` ve üstünde `main` + `aside` yan yana. Grid seçtim çünkü
   sayfa düzeni iki boyutlu (satır ve sütun birlikte) ve `grid-template-areas` ile düzen okunaklı oluyor.
5. **Components**: Menü, bölüm başlığı, yazı kartı (`.post`), yan panel (`.sidebar`), footer.
   Sınıf isimleri BEM benzeri (`post__title`, `site-nav__link`); böylece stiller birbirine karışmıyor.

Ayrıca: satır genişliği sınırlandı, menü bağlantılarında `:hover` durumu var, mobilde menü
`flex-wrap` ile alt satıra geçiyor ve sayfa taşmıyor (`minmax(0, 1fr)`).

## Proje büyürse neyi geliştirirdim?

- CSS'i tek dosyadan çıkarıp bölümlere ayırırdım (`base.css`, `layout.css`, `components/…`).
- Koyu tema için renk değişkenlerini `prefers-color-scheme` ile genişletirdim.
- React'e geçildiğinde `.post`, `.site-nav` ve `.sidebar` doğrudan birer bileşen olabilir.
- Gerçek içerik gelince yazılar için ayrı sayfalar, sayfalama ve arama eklenirdi.
- "İçeriğe geç" (skip link) bağlantısı ve daha kapsamlı erişilebilirlik testi yapardım.
