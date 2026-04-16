# kubraengudar.com — Claude Code Talimatları

Bu dosya, Psikolog Kübra Engüdar'ın web sitesinin Next.js ile yeniden yazılması için Claude Code'a verilen tam talimat dosyasıdır.

---

## PROJE GENEL BAKIŞ

**Site:** kubraengudar.com  
**Kişi:** Uzman Klinik Psikolog Kübra Engüdar  
**Teknik Sorumlu:** Batu (GitHub: Batu-CorvenX)  
**Repo:** github.com/Batu-CorvenX/kubraengudar-website  
**Hosting:** Vercel (otomatik deploy — main branch push)  
**Domain:** kubraengudar.com (Namecheap)  
**Form:** Formspree ID `xaqlllkn` → tturankubra@gmail.com  

---

## TEKNİK STACK

- **Framework:** Next.js (static export — `next export`, Mode 1)
- **Stil:** Tailwind CSS
- **Yapı:** `src/app` (App Router)
- **Bileşen:** Component tabanlı
- **Öncelik:** Mobile-first
- **Fontlar:** Cormorant Garamond (serif) + DM Sans (sans) — Google Fonts
- **Deploy:** Vercel, main branch push → otomatik

### next.config.js
```js
/** @type {import('next').NextConfig} */
const nextConfig = {
  output: 'export',
  trailingSlash: false,
  images: { unoptimized: true },
}
module.exports = nextConfig
```

### Tailwind Renk Paleti (tailwind.config.js'e ekle)
```js
colors: {
  sage: {
    DEFAULT: '#7A9E7E',
    light: '#EBF2EC',
    mid: '#B8CFBA',
    dark: '#4A6E4E',
  },
  cream: {
    DEFAULT: '#F5F0E8',
    dark: '#EDE5D8',
  },
  warm: '#FDFBF6',
  brown: {
    DEFAULT: '#2C2417',
    mid: '#6B5C4A',
    light: '#9A8878',
  },
  accent: {
    DEFAULT: '#C4956A',
    light: '#F5EAE0',
  },
}
```

---

## DOSYA YAPISI

```
src/
├── app/
│   ├── layout.tsx              # Root layout (font, meta)
│   ├── page.tsx                # Ana Sayfa (TR)
│   ├── hakkimda/
│   │   └── page.tsx            # Hakkımda (TR)
│   ├── blog/
│   │   ├── page.tsx            # Blog listesi (TR)
│   │   └── [slug]/
│   │       └── page.tsx        # Blog yazısı (TR)
│   ├── gizlilik-politikasi/
│   │   └── page.tsx            # Gizlilik Politikası (TR)
│   ├── kvkk/
│   │   └── page.tsx            # KVKK Aydınlatma Metni (TR)
│   └── en/
│       ├── layout.tsx          # EN layout (hreflang)
│       ├── page.tsx            # Home (EN)
│       ├── about/
│       │   └── page.tsx        # About (EN)
│       ├── blog/
│       │   ├── page.tsx        # Blog list (EN)
│       │   └── [slug]/
│       │       └── page.tsx    # Blog post (EN)
│       └── privacy-policy/
│           └── page.tsx        # Privacy Policy (EN)
├── components/
│   ├── Navbar.tsx              # Nav (TR/EN switcher dahil)
│   ├── Footer.tsx              # 3 kolonlu footer
│   ├── Hero.tsx                # Hero section
│   ├── About.tsx               # About section
│   ├── Services.tsx            # 9 hizmet kartı
│   ├── Process.tsx             # 3 adım
│   ├── ContactForm.tsx         # Formspree formu
│   ├── BlogGrid.tsx            # Blog kart listesi
│   ├── BlogCard.tsx            # Tek blog kartı
│   └── LegalPage.tsx           # Yasal sayfa layout
├── data/
│   ├── blog-tr.ts              # TR blog yazıları (13 adet)
│   ├── blog-en.ts              # EN blog yazıları (13 adet)
│   └── services.ts             # Hizmet kartı verileri
public/
├── images/
│   ├── kubra.jpg               # Psikolog profil fotoğrafı (2.jpeg → rename)
│   └── hero.jpg                # Hero görseli (puzzle/beyin fotoğrafı)
└── sitemap.xml
```

---

## SAYFALAR VE ROUTE'LAR

| Sayfa | TR URL | EN URL |
|---|---|---|
| Ana Sayfa | `/` | `/en/` |
| Hakkımda | `/hakkimda` | `/en/about` |
| Blog Listesi | `/blog` | `/en/blog` |
| Blog Yazısı | `/blog/[slug]` | `/en/blog/[slug]` |
| Gizlilik | `/gizlilik-politikasi` | `/en/privacy-policy` |
| KVKK / Privacy | `/kvkk` | — (KVKK TR'ye özel) |

---

## NAV BİLEŞENİ

- Topbar YOK (eski sitedeki kahverengi bar kaldırıldı)
- Logo solda: "Kübra Engüdar" (serif) + "Uzman Klinik Psikolog · Aile Danışmanı" (küçük)
- Linkler ortada: Ana Sayfa / Hakkımda / Blog / İletişim
- Sağda: "Randevu Al" (sage yeşil CTA butonu) + TR/EN switcher
- Mobilde: hamburger menü
- TR aktifken `/en/` prefix'li URL'lere yönlendir, EN'de prefix'siz URL'lere

### TR/EN Switcher Mantığı
```tsx
// Mevcut path'e göre karşı dil URL'sini üret
const getAltLangUrl = (pathname: string, currentLang: 'tr' | 'en') => {
  if (currentLang === 'tr') return `/en${pathname === '/' ? '/' : pathname}`
  return pathname.replace(/^\/en/, '') || '/'
}
```

---

## HERO SECTION

- **Sol:** `hero.jpg` (puzzle/beyin fotoğrafı) — tam genişlik, border-radius ile yumuşatılmış
- **Sağ:** Başlık metni
- **TR başlık:** "Sağlıklı zihin, sağlıklı yaşam"
- **EN başlık:** "A healthy mind, a healthy life"
- **TR açıklama:** "Güvenli bir terapötik ortamda; bireysel terapi, çocuk-ergen danışmanlığı ve aile danışmanlığı ile yaşam kalitenize katkı sunmaya eşlik ediyorum."
- **EN açıklama:** "In a safe therapeutic space, I accompany you on your journey to better wellbeing through individual therapy, child-adolescent counseling, and family counseling."
- **CTA:** "Randevu Al" / "Book a Session" → form'a scroll

---

## ABOUT SECTION (Ana Sayfa)

- Sol: `kubra.jpg` ile dekoratif çerçeve efekti
- Sağ: kısa biyografi
- Link: Hakkımda sayfasına yönlendirme

**TR metin:**
```
Uludağ Üniversitesi Psikoloji Bölümü'nden onur derecesiyle mezun olduktan
sonra İstanbul Arel Üniversitesi Klinik Psikoloji Bölümü'nde yüksek onur
derecesiyle yüksek lisansını tamamlayarak Uzman Klinik Psikolog unvanını
almıştır. 2023 yılında Biruni Üniversitesi Aile Danışmanlığı Sertifika
Programı'nı tamamlayarak Aile Danışmanı unvanına sahip olmuştur.
2025 yılından itibaren New York'ta online danışmanlık sunmaktadır.
Türk Psikologlar Derneği ve EMDR Türkiye Derneği üyesidir.
```

---

## HİZMETLER (9 KART)

Her kart: ikon + başlık + kısa açıklama + "Daha fazla bilgi →" linki

| # | TR Başlık | EN Başlık |
|---|---|---|
| 1 | Kaygı ve stres | Anxiety & Stress |
| 2 | İlişki sorunları | Relationship Issues |
| 3 | Tükenmişlik | Burnout |
| 4 | Yeni ülke, yeni hayat | New Country, New Life |
| 5 | Çocuk ve Ergen | Children & Adolescents |
| 6 | Kayıp ve yas | Grief & Loss |
| 7 | Öfke yönetimi | Anger Management |
| 8 | Depresyon | Depression |
| 9 | Aile Danışmanlığı | Family Counseling |

> **Not:** Eski "Çocuğum / Ergenim için endişeleniyorum" → "Çocuk ve Ergen" olarak güncellendi.

---

## DANIŞMANLIK BAŞVURU FORMU

**Formspree endpoint:** `https://formspree.io/f/xaqlllkn`  
**Yönlendirme:** `_next: https://kubraengudar.com`  
**E-posta bildirimi:** tturankubra@gmail.com (Formspree panelinde ayarlı)

### Form Alanları
1. Adınız Soyadınız (required)
2. E-posta Adresiniz (required)
3. Telefon Numaranız
   - **TR:** placeholder `+90 (5xx) xxx xx xx`
   - **EN:** placeholder `+1 (555) 000-0000`
4. Destek almak istediğiniz konu (select)
   - TR seçenekler: Bireysel Danışmanlık / Çocuk-Ergen Danışmanlığı / Aile Danışmanlığı
   - EN seçenekler: Individual Counseling / Child-Adolescent Counseling / Family Counseling
5. Başvuru Nedeniniz (textarea)
6. Bana nasıl ulaştınız? (select: Instagram / Google / Tavsiye / Diğer)
   - Diğer seçilince text input görünür

### Form Sol Kolon (bilgi alanı)
**TR liste:**
- Ücretsiz ön görüşme imkânı
- Online seans seçeneği
- Gizlilik ve güven ilkesi

**EN liste:**
- Free initial consultation
- Online session option
- Confidentiality guaranteed

> **Not:** "Türkçe ve İngilizce destek" maddesi KALDIRILDI.

---

## HAKKIMDA SAYFASI — TAM İÇERİK

### Biyografi
Kübra Engüdar, lisans eğitimini 2016 yılında Uludağ Üniversitesi Psikoloji Bölümü'nden **onur derecesiyle** tamamlamıştır. Yüksek lisans eğitimini 2019 yılında İstanbul Arel Üniversitesi Klinik Psikoloji Bölümü'nde *"Genç Yetişkin ve Yetişkinlerde Mükemmeliyetçilik ve Psikolojik Belirtiler Arasındaki İlişkide Öz-Duyarlık Faktörünün Aracı Rolü"* başlıklı teziyle **yüksek onur derecesiyle** tamamlayarak Uzman Klinik Psikolog unvanını almıştır.

2023 yılında Biruni Üniversitesi Aile Danışmanlığı Sertifika Programı'nı 450 saatlik öğretim ve süpervizyon süreciyle tamamlayarak Aile Danışmanı unvanına sahip olmuştur. 2025 yılı Haziran ayından itibaren New York'ta yaşamakta ve online danışmanlık sunmaya devam etmektedir.

### Eğitim
| Derece | Kurum | Yıl | Not |
|---|---|---|---|
| Lisans | Uludağ Üniversitesi — Psikoloji | 2011–2016 | Onur derecesi |
| Yüksek Lisans | İstanbul Arel Üniversitesi — Klinik Psikoloji | 2017–2019 | Yüksek onur derecesi |
| Sertifika | Biruni Üniversitesi — Aile Danışmanlığı | 2023 | 450 saat |

### Deneyimler
- **Mozaik Psikoloji, Bahçeşehir** — Uzman Klinik Psikolog, Aile Danışmanı (11.2022–06.2025)
- **Biruni Üniversitesi** — Misafir Öğretim Görevlisi (2024)
- **Lavien Psikoloji, Beylikdüzü** — Serbest Zamanlı Uzman Klinik Psikolog (06.2022–10.2022)
- **Sefaköy Çocuk Büro Amirliği** — Serbest Zamanlı Uzman Klinik Psikolog (06.2022–10.2022)
- **Özel Küçük Adımlar Anaokulu, Bahçeşehir** — Uzman Okul Psikoloğu (2017–2022)
- **Prof. Dr. Mazhar Osman Ruh Sağlığı Hastanesi, Bakırköy** — Stajyer Psikolog (2015)

### Uzmanlık Eğitimleri ve Sertifikalar
- EMDR Terapisi 1. ve 2. Düzey (Yetişkin) — Davranış Bilimleri Enstitüsü, Emre Konuk
- EMDR Terapisi 1. Düzey (Çocuk-Ergen) — Fide Danışmanlık, Ümran Korkmazlar
- AIP Perspektifinden Borderline Kişilik Bozukluğu ve EMDR — Febris Danışmanlık, Derya Altınay, Mustafa Çetinkaya
- EMDR ile Yetişkinlerde Bağlanma Sorunları — Enstitü Ay, Asena Yurtsever
- Çocuk Merkezli Oyun Terapisi — Oyun Terapileri Derneği, Dr. Birgül Emiroğlu Bakay
- Yapılandırılmış Oyun Terapisi (2. Düzey) — Oyun Terapileri Derneği, Dr. Birgül Emiroğlu Bakay
- Filial Terapi — Elif Macit Eğitim Akademisi
- Yetişkin Projektif Testler (Rorschach, TAT) — Rorschach ve Projektif Testler Derneği, Bengi Pirim Düşgör
- Çocuk-Ergen Projektif Testler (Rorschach, CAT, TAT) — Rorschach ve Projektif Testler Derneği, Neslihan Zabcı
- Kısa Süreli Çözüm Odaklı Terapi — Dr. Öğrt. Üyesi Nevin Dölek
- PERGEL — Performans Geliştirme Programı ve EMDR ile Sınav Kaygısı — Arkabahçe Psikoloji, Olcay Güner
- Güvenli Yuva Çocuk ve Ergenle Psikoterapi — Psikoloji İstanbul, Dr. Nilüfer Devecigil
- Psikolojik İlk Yardım ve TSSB Eğitimi — Ruh Sağlığı Derneği
- Yetişkin ve Çocuk Travmasında Sanat Terapisi ve Kısa Bilişsel Müdahaleler — Arkabahçe Psikoloji, Olcay Güner
- WISC-4 Çocuk Zeka Ölçeği — Türk Psikologlar Derneği
- Denver II Gelişimsel Tarama Testi — Türk Psikologlar Derneği
- MMPI (Minnesota Çok Yönlü Kişilik Envanteri)
- Çocuk Değerlendirme Testleri — Türk Psikologlar Derneği

### Verdiği Eğitimler ve Seminerler
Kişilik Kuramları · Sosyal Medyanın Aile İlişkileri Üzerine Etkisi · Teknoloji Bağımlılığı ve Önleyici Yaklaşımlar · Teknopozitif Ebeveyn Olmak ve Medya Rehberliği · Çocuk Merkezli Oyun Terapisi (Kolaylaştırıcı) · Çocuklarımıza Sağlıklı Sınır Koyma · Ergenliği Tanımak, Ergenleri Anlamak · Ebeveyn Tutumları · Mahremiyet ve Beden Sınırları · Psikolojik İlk Yardım · Anne Baba Olmak · Boşanma Süreci ve Çocuk · Aileye Yeni Bir Çocuğun Katılması · Kaynaklarımla Güçleniyorum

### Üyelikler
- Amerikan Psikoloji Derneği (APA)
- Türk Psikologlar Derneği
- EMDR Türkiye Derneği
- Anne-Çocuk Eğitim Vakfı (AÇEV)
- Kadın Emeğini Değerlendirme Vakfı (KEDV)
- Toplum Gönüllüleri Vakfı

---

## BLOG YAZILARI

### Yazı Dili ve Stili
- **Dil:** Türkçe (TR) + İngilizce (EN) her yazı için
- **Ses:** Üçüncü şahıs uzman dili ("Psikologlar şunu önerir...", "Araştırmalar gösteriyor ki...")
- **Uzunluk:** Minimum 800 kelime, ideal 1000–1500 kelime
- **SEO:** Her yazıda meta title, meta description, slug
- **Yapı:** Başlık → Giriş (lead) → Alt başlıklı bölümler → Kapanış CTA

### 13 Blog Yazısı Listesi

Tüm yazılar aşağıdaki kaynak içerikler genişletilerek ve SEO uyumlu hale getirilerek yazılmalıdır:

| # | Slug | TR Başlık | Kategori | Kaynak |
|---|---|---|---|---|
| 1 | `goc-psikolojisi-10-oneri` | Göç Psikolojisiyle Başa Çıkmak için 10 Öneri | Göç | 3.txt |
| 2 | `gaslighting-nedir` | Gaslighting: Gerçeklik Algınız Manipüle Ediliyor mu? | İlişkiler | 4.txt |
| 3 | `mukemmeliyetcilik` | Mükemmeliyetçilik: Sizi Koruyan mı, Kısıtlayan mı? | Kişisel Gelişim | 5.txt |
| 4 | `iliskilerde-donguler` | İlişkilerde Döngüler: Aynı Tartışmayı Neden Tekrar Ederiz? | İlişkiler | 2.txt |
| 5 | `cocuga-sorumluluk` | Çocuğunuza Sorumluluk Bilinci Nasıl Kazandırırsınız? | Ebeveynlik | 6.txt + docx |
| 6 | `kurban-rolu` | Kurban Rolü: Hayatınızın Kontrolünü Geri Alın | Kişisel Gelişim | 7.txt |
| 7 | `psikolojik-saglamlik` | Psikolojik Sağlamlık Nedir ve Nasıl Geliştirilir? | Psikolojik Sağlık | 10.txt |
| 8 | `psikolojik-ozbakım` | Psikolojik Özbakım: Duygularınızı Fark Edin, Sınır Koyun | Özbakım | 8+11+12+13+14.txt |
| 9 | `evcil-hayvan-cocuk` | Evcil Hayvanların Çocuk Gelişimine Etkisi | Ebeveynlik | docx |
| 10 | `okula-uyum` | Okula Uyum Sürecinde Ailelerin Yapabilecekleri | Ebeveynlik | docx |
| 11 | `afet-sonrasi-psikoloji` | Doğal Afet Sonrası Psikolojik Baş Etme Rehberi | Travma | docx |
| 12 | `ergenlik` | Ergenliği Tanımak, Ergenleri Anlamak | Ergenlik | docx |
| 13 | `pozitif-disiplin` | Pozitif Disiplin: Ebeveyn Tutumlarının Çocuk Gelişimine Etkisi | Ebeveynlik | .key |

### Blog Veri Yapısı (data/blog-tr.ts)
```ts
export interface BlogPost {
  slug: string
  title: string
  category: string
  date: string
  readTime: number // dakika
  excerpt: string
  content: string // Markdown veya JSX string
  metaTitle: string
  metaDescription: string
}
```

### Blog Thumbnail Renkleri
Her karta farklı gradient arka plan (gerçek görsel yoksa):
```ts
const gradients = [
  'from-sage-light to-sage-mid',
  'from-cream to-accent-light',
  'from-cream-dark to-brown-light/30',
  // ...
]
```

---

## FOOTER

3 kolon yapısı:

**Kolon 1 — Kimlik ve İletişim**
- Logo: "Kübra Engüdar" + "Uzman Klinik Psikolog · Aile Danışmanı"
- info@kubraengudar.com (tıklanabilir)
- @psikolog.kubraengudar (tıklanabilir, Instagram'a yönlendir) ← **aktif link olmalı**

**Kolon 2 — Instagram Mini Feed**
- 6 adet placeholder thumbnail (gerçek Instagram API entegrasyonu opsiyonel)
- Altında Instagram hesabına link

**Kolon 3 — Linkler**
- Gizlilik Politikası (→ `/gizlilik-politikasi`)
- KVKK Aydınlatma Metni (→ `/kvkk`)
- Ana Sayfa
- Hakkımda
- Blog

**Footer altı:** © 2026 kubraengudar.com · Tüm hakları saklıdır.

---

## GİZLİLİK POLİTİKASI (TR)

Türkiye mevzuatına uygun. Bölümler:
1. Veri Sorumlusu
2. Toplanan Kişisel Veriler
3. İşlenme Amaçları
4. Saklama Süresi
5. Üçüncü Kişilerle Paylaşım
6. Çerezler
7. Güvenlik
8. Haklarınız (düzeltme, silme, itiraz...)
9. İletişim: info@kubraengudar.com

## KVKK AYDINLATMA METNİ (TR)

6698 Sayılı Kanun kapsamında. Bölümler:
1. Veri Sorumlusu
2. İşlenen Kişisel Veriler
3. İşlenme Amaçları
4. Aktarım
5. Toplama Yöntemi ve Hukuki Sebep
6. Veri Sahibinin Hakları (KVKK Madde 11 — tam liste)
7. Başvuru Yöntemi
8. Veri Saklama Süresi

## PRIVACY POLICY (EN)

US law compliant (California CCPA). Sections:
1. Who We Are
2. Information We Collect
3. How We Use Your Information
4. Data Retention
5. Third-Party Sharing
6. Cookies
7. Security
8. Your Rights (access, deletion, opt-out)
9. Contact: info@kubraengudar.com

---

## SEO VE META

### Root Layout (layout.tsx)
```tsx
export const metadata = {
  metadataBase: new URL('https://kubraengudar.com'),
  alternates: {
    canonical: '/',
    languages: { 'tr': '/', 'en': '/en/' }
  },
}
```

### Her Sayfa İçin
- `title`: Sayfa başlığı | Kübra Engüdar
- `description`: Kısa açıklama (150 karakter)
- `openGraph`: title, description, url, type
- `alternates.canonical` ve `alternates.languages` (hreflang TR/EN)

### Schema.org (Ana Sayfa)
```json
{
  "@context": "https://schema.org",
  "@type": "ProfessionalService",
  "name": "Psikolog Kübra Engüdar",
  "description": "Uzman Klinik Psikolog ve Aile Danışmanı...",
  "url": "https://kubraengudar.com",
  "email": "info@kubraengudar.com",
  "serviceType": ["Bireysel Terapi","Çift Terapisi","Aile Danışmanlığı","EMDR Terapisi","Çocuk ve Ergen Terapisi"],
  "sameAs": ["https://www.instagram.com/psikolog.kubraengudar"]
}
```

### sitemap.xml (public/sitemap.xml)
```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9"
        xmlns:xhtml="http://www.w3.org/1999/xhtml">
  <!-- TR sayfaları -->
  <url>
    <loc>https://kubraengudar.com/</loc>
    <xhtml:link rel="alternate" hreflang="tr" href="https://kubraengudar.com/"/>
    <xhtml:link rel="alternate" hreflang="en" href="https://kubraengudar.com/en/"/>
    <changefreq>monthly</changefreq>
    <priority>1.0</priority>
  </url>
  <url>
    <loc>https://kubraengudar.com/hakkimda</loc>
    <xhtml:link rel="alternate" hreflang="tr" href="https://kubraengudar.com/hakkimda"/>
    <xhtml:link rel="alternate" hreflang="en" href="https://kubraengudar.com/en/about"/>
    <changefreq>monthly</changefreq>
    <priority>0.9</priority>
  </url>
  <url>
    <loc>https://kubraengudar.com/blog</loc>
    <changefreq>weekly</changefreq>
    <priority>0.8</priority>
  </url>
  <!-- EN sayfaları -->
  <url>
    <loc>https://kubraengudar.com/en/</loc>
    <xhtml:link rel="alternate" hreflang="en" href="https://kubraengudar.com/en/"/>
    <xhtml:link rel="alternate" hreflang="tr" href="https://kubraengudar.com/"/>
    <changefreq>monthly</changefreq>
    <priority>1.0</priority>
  </url>
  <!-- Blog slugları için dinamik olarak üret -->
</urlset>
```

---

## GÖRSELler

| Dosya | Kullanım | Kaynak |
|---|---|---|
| `public/images/kubra.jpg` | Profil fotoğrafı (hero + hakkımda + about) | 2.jpeg (yüklendi) |
| `public/images/hero.jpg` | Ana sayfa hero görseli | hero.jpg (yüklendi) |

**Fotoğraf yerleşimi:**
- **Ana Sayfa Hero:** Sol taraf `hero.jpg`, sağ taraf metin
- **Ana Sayfa About:** Sol `kubra.jpg` (dekoratif çerçeve), sağ metin  
- **Hakkımda Sayfası:** Sağ `kubra.jpg`, sol metin

---

## RENK VE TASARIM SİSTEMİ

### CSS Değişkenleri (globals.css'e ekle)
```css
:root {
  --sage: #7A9E7E;
  --sage-light: #EBF2EC;
  --sage-mid: #B8CFBA;
  --sage-dark: #4A6E4E;
  --cream: #F5F0E8;
  --cream-dark: #EDE5D8;
  --warm-white: #FDFBF6;
  --brown: #2C2417;
  --brown-mid: #6B5C4A;
  --brown-light: #9A8878;
  --accent: #C4956A;
  --accent-light: #F5EAE0;
  --border: rgba(44, 36, 23, 0.1);
}
```

### Tipografi
- **Serif (başlıklar):** Cormorant Garamond — weight 400, 500, 600
- **Sans (body):** DM Sans — weight 300, 400, 500, 600
- **Next.js font import:**
```tsx
import { DM_Sans } from 'next/font/google'
import { Cormorant_Garamond } from 'next/font/google'
```

### Hero Fotoğraf Çerçevesi (kubra.jpg için)
```tsx
// Üst köşeleri yuvarlak, kemer şekli
className="rounded-[150px_150px_110px_110px] overflow-hidden"
```

---

## ÖNEMLİ NOTLAR

1. **Formspree ID değişmez:** `xaqlllkn` — form action URL'si korunmalı
2. **Instagram linki aktif:** Footer'daki @psikolog.kubraengudar tıklanabilir olmalı
3. **Demo navigation bar:** Gerçek sitede YOK — sadece demo HTML'deydi
4. **Blog yazıları tam içerikle:** 13 yazının tamamı ayrı slug'larda, tam metin, SEO metaları ile
5. **EN sayfaları:** Tüm içerik İngilizceye çevrilmeli, TR ile paralel yapı
6. **Static export:** `next export` kullanılacak, server-side özellikler YOK
7. **Mobil öncelik:** Tüm bileşenler mobile-first Tailwind class'larıyla yazılmalı
8. **vercel.json:** Mevcut `cleanUrls: true`, `trailingSlash: false` ayarları korunmalı

---

## YAPILACAKLAR (Claude Code Kapsamı Dışı)

Bunlar ayrıca yapılacak, Claude Code'a dahil değil:
- [ ] Google Search Console doğrulama meta tag'i (Batu ekleyecek)
- [ ] Cal.com randevu entegrasyonu (sonraya bırakıldı)
- [ ] Google Ads (planlanmadı)

---

## VERİTABANI / CMS

Blog yazıları için CMS kullanılmıyor. Tüm içerik `data/blog-tr.ts` ve `data/blog-en.ts` dosyalarında statik TypeScript nesneleri olarak tutulacak. Yeni yazı eklemek için bu dosyalara obje eklenir ve `main` branch'e push yapılır.

---

*Son güncelleme: Nisan 2026*  
*Hazırlayan: Batu & Claude*
