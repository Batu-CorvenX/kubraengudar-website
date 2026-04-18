# Kubraengudar.com — Site Güncelleme Talimatları

Bu dosya, aşağıdaki 4 değişikliğin uygulanması için Claude Code'a verilecek talimatlardır.
Her değişiklik için hangi dosyanın nerede değiştirileceği tam olarak belirtilmiştir.

---

## DEĞİŞİKLİK 1 — index.html: Blog kartlarını tıklanabilir yap

**Dosya:** `index.html`  
**Bölüm:** `#blog` section içindeki `.blog-grid`

### Sorun
Şu an 3 blog kartı `<div class="blog-card">` olarak yazılmış — tıklanabilir değil.

### Yapılacak
Her `<div class="blog-card">` → `<a href="..." class="blog-card" style="text-decoration:none;color:inherit;display:block">` olarak değiştirilecek.

Kart başına eklenecek href'ler:

| Kart başlığı | href |
|---|---|
| Göç ettikten sonra neden kendimizi kaybolmuş hissederiz? | `/blog/goc-psikolojisi-10-oneri.html` |
| Kaygıyla yaşamayı bırakıp kaygıyı yönetmeye başlamak | `/blog/psikolojik-saglamlik.html` |
| Çocuğunuz ekrandan ayrılamıyor mu? | `/blog/cocuk-ekran-bagimliligi.html` |

### Örnek — değiştirilecek blok (1. kart):
```html
<!-- ÖNCE -->
<div class="blog-card">
  <div class="blog-thumb" style="background:linear-gradient(135deg,#EBF2EC,#B8CFBA)"></div>
  <div class="blog-card-body">
    <div class="blog-date">15 Mart 2026</div>
    <h3>Göç ettikten sonra neden kendimizi kaybolmuş hissederiz?</h3>
    <p>Yeni bir ülkeye taşınmak sadece fiziksel değil, duygusal bir yolculuktur...</p>
  </div>
</div>

<!-- SONRA -->
<a href="/blog/goc-psikolojisi-10-oneri.html" class="blog-card" style="text-decoration:none;color:inherit;display:block">
  <div class="blog-thumb" style="background:linear-gradient(135deg,#EBF2EC,#B8CFBA)"></div>
  <div class="blog-card-body">
    <div class="blog-date">15 Mart 2026</div>
    <h3>Göç ettikten sonra neden kendimizi kaybolmuş hissederiz?</h3>
    <p>Yeni bir ülkeye taşınmak sadece fiziksel değil, duygusal bir yolculuktur...</p>
  </div>
</a>
```

Aynı dönüşümü diğer 2 kart için de uygula (href'leri yukarıdaki tabloya göre).

---

## DEĞİŞİKLİK 2 — blog.html: Kategori filtresi için JavaScript ekle

**Dosya:** `blog.html`  
**Bölüm:** Her blog kartına `data-category` attribute ekle + `</body>` öncesine `<script>` bloğu ekle

### Adım 1 — Her `.blog-card`'a `data-category` attribute ekle

Her `<a href="..." class="blog-card">` etiketine o kartın kategorisine göre `data-category="..."` eklenir.
Kategori değeri, kartın içindeki `.blog-category` metninin küçük harfli, Türkçe orijinal halidir.

Eşleşmeler:
```
Göç                → data-category="göç"
İlişkiler          → data-category="ilişkiler"
Kişisel Gelişim    → data-category="kişisel gelişim"
Ebeveynlik         → data-category="ebeveynlik"
Travma             → data-category="travma"
Ergenlik           → data-category="ergenlik"
Özbakım            → data-category="özbakım"
Psikolojik Sağlık  → data-category="psikolojik sağlık"
```

Örnek:
```html
<a href="/blog/goc-psikolojisi-10-oneri.html" class="blog-card" data-category="göç">
```

### Adım 2 — `</body>` kapanmadan hemen önce şu script bloğunu ekle:

```html
<script>
  const catBtns = document.querySelectorAll('.cat-btn');
  const cards = document.querySelectorAll('.blog-card');

  catBtns.forEach(btn => {
    btn.addEventListener('click', function(e) {
      e.preventDefault();
      catBtns.forEach(b => b.classList.remove('active'));
      this.classList.add('active');

      const selected = this.textContent.trim().toLowerCase();

      cards.forEach(card => {
        if (selected === 'tümü') {
          card.style.display = 'block';
        } else {
          const cat = (card.dataset.category || '').toLowerCase();
          card.style.display = cat === selected ? 'block' : 'none';
        }
      });
    });
  });
</script>
```

---

## DEĞİŞİKLİK 3 — index.html: İletişim kutularının tamamını tıklanabilir yap

**Dosya:** `index.html`  
**Bölüm:** `#contact` section içindeki `.contact-grid`

### Sorun
`.contact-item` div'leri içindeki link sadece metni kapsıyor; kutunun tamamına tıklayınca link açılmıyor.

### Yapılacak
Her `<div class="contact-item">` → `<a href="..." class="contact-item" style="text-decoration:none">` olarak değiştirilecek.
İçindeki `<a>` tag'leri `<span>` ile değiştirilecek (iç içe `<a>` geçersiz HTML).

### E-posta kartı:
```html
<!-- ÖNCE -->
<div class="contact-item">
  <div class="contact-icon">...</div>
  <div>
    <span class="contact-label">E-posta</span>
    <span class="contact-value"><a href="mailto:info@kubraengudar.com">info@kubraengudar.com</a></span>
  </div>
</div>

<!-- SONRA -->
<a href="mailto:info@kubraengudar.com" class="contact-item" style="text-decoration:none">
  <div class="contact-icon">...</div>
  <div>
    <span class="contact-label">E-posta</span>
    <span class="contact-value" style="color:var(--primary-darker)">info@kubraengudar.com</span>
  </div>
</a>
```

### Instagram kartı:
```html
<!-- ÖNCE -->
<div class="contact-item">
  <div class="contact-icon">...</div>
  <div>
    <span class="contact-label">Instagram</span>
    <span class="contact-value"><a href="https://www.instagram.com/psikolog.kubraengudar/" target="_blank" rel="noopener">@psikolog.kubraengudar</a></span>
  </div>
</div>

<!-- SONRA -->
<a href="https://www.instagram.com/psikolog.kubraengudar/" target="_blank" rel="noopener" class="contact-item" style="text-decoration:none">
  <div class="contact-icon">...</div>
  <div>
    <span class="contact-label">Instagram</span>
    <span class="contact-value" style="color:var(--primary-darker)">@psikolog.kubraengudar</span>
  </div>
</a>
```

---

## DEĞİŞİKLİK 4 — hakkimda.html: Uzmanlık eğitimlerine 9 yeni madde ekle

**Dosya:** `hakkimda.html`  
**Bölüm:** "Uzmanlık Eğitimleri ve Sertifikalar" başlıklı section içindeki `<ul class="detail-list">`

### Yapılacak
Mevcut listenin **sonuna** (kapanış `</ul>` etiketinden önce) aşağıdaki 9 yeni `<li>` maddesini ekle:

```html
<li><strong>The Body Keeps the Score: Trauma Healing Through the Senses (Beden Kayıt Tutar: Duyular Yoluyla Travma İyileşmesi)</strong>Bessel van der Kolk, Online Konferans</li>
<li><strong>Healing Betrayal Trauma &amp; Grief (İhanet Travması ve Yasın İyileştirilmesi)</strong>John Gottman, Julie Gottman, David Kessler, Online Eğitim</li>
<li><strong>EMDR Therapy Crash Course: A Step-by-Step Review of Fundamental Techniques and Clinical Applications (EMDR Terapi Hızlandırılmış Eğitimi: Temel Teknikler ve Klinik Uygulamalar)</strong>Laura Swinford, Online Eğitim</li>
<li><strong>When a Spouse Dies: Support for the Loneliness No One Talks About (Eş Kaybı Sonrası: Konuşulmayan Yalnızlığa Destek)</strong>David Kessler, Online Eğitim</li>
<li><strong>Transformation Journey of Immigrant Women (Göçmen Kadınların Dönüşüm Yolculuğu)</strong>Gülseren Budayıcıoğlu, Webinar / Söyleşi</li>
<li><strong>Challenges in the Birth Process and Family Coping Mechanisms (Doğum Sürecinde Yaşanan Zorluklar ve Ailenin Başa Çıkma İşlevi)</strong>Mustafa Çetinkaya, Online Seminer</li>
<li><strong>Migration and Womanhood (Göç ve Kadınlık)</strong>Göçmen Psikologlar Platformu (GPPA), Webinar</li>
<li><strong>Applying Psychological Flexibility in Clinical Practice: Enhancing Effectiveness in Therapy (Klinik Uygulamada Psikolojik Esnekliğin Kullanımı: Terapötik Etkililiği Artırma)</strong>American Psychological Association – APA, Online Eğitim</li>
<li><strong>Inspired Parenting: Parenting from an Attachment and Trauma Perspective (İlham Veren Ebeveynlik: Bağlanma ve Travma Perspektifinden Ebeveynlik)</strong>Dafna Lender, Online Eğitim</li>
```

---

## ÖZET — Etkilenen Dosyalar

| Dosya | Değişiklik |
|---|---|
| `index.html` | Blog kartları `<a>` oldu (DEĞ. 1) + İletişim kutuları `<a>` oldu (DEĞ. 3) |
| `blog.html` | `data-category` attribute'ları + kategori filtre JS (DEĞ. 2) |
| `hakkimda.html` | 9 yeni eğitim maddesi eklendi (DEĞ. 4) |

**Dokunulmayacak dosyalar:** `gizlilik-politikasi.html`, `kvkk.html`, `sitemap.xml`, `vercel.json`

**Formspree action URL'si kesinlikle değiştirilmeyecek:** `https://formspree.io/f/xaqlllkn`
