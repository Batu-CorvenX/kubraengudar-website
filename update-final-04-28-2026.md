# kubraengudar.com — Final Update Notları
**Tarih:** 28 Nisan 2026  
**Kapsam:** TR + EN tüm sayfalar (aksi belirtilmedikçe)

---

## UPDATE 1 — Global Mobile Spacing Fix

**Etkilenen dosyalar:** Tüm sayfalar (`index.html`, `hakkimda.html`, `blog.html`, `en/index.html`, `en/about.html`, `en/blog.html` vb.)

**Sorun:** `@media(max-width:768px)` içinde `.container{padding:0 20px}` shorthand kullanıldığı için `.about`, `.services` gibi section class'ları yatay padding'i eziyor. Metin ekran kenarına binuyor.

**Fix 1 — Container padding:**
```css
/* @media(max-width:768px) içinde ÖNCE: */
.container{padding:0 20px}

/* SONRA: */
.container{padding-left:20px;padding-right:20px}
```

**Fix 2 — TR/EN "TREN" bug (mobile menu lang-switch):**
```css
/* @media(max-width:768px) içinde ÖNCE: */
.mobile-menu .lang-switch{margin-top:4px;border:1px solid var(--border);border-radius:6px;overflow:hidden;display:inline-flex}

/* SONRA: */
.mobile-menu .lang-switch{margin-top:4px;border:1px solid var(--border);border-radius:6px;overflow:hidden;display:inline-flex;width:auto;align-self:flex-start}
.mobile-menu .lang-switch a{min-width:44px;text-align:center;padding:8px 14px}
```

**Not:** Aynı fix tüm sayfalardaki `<style>` bloğuna uygulanacak.

---

## UPDATE 2 — CTA + Form Metin Değişikliği

**Etkilenen dosyalar:** `index.html`, `en/index.html`

**2a — CTA açıklama metni (sarı alan):**
> TR Eski: "Size özel destek sunuyorum. Aşağıdaki formu doldurarak başvurunuzu yapın."  
> TR Yeni: "Formunuz ulaştıktan sonra en kısa sürede sizinle iletişime geçilecektir."

> EN Yeni: "Once your form is received, you will be contacted as soon as possible."

**2b — Form alt metni (mavi alan):**
- `Danışmanlık Başvuru Formu` başlığının altındaki açıklama metni **tamamen kaldırılacak**

---

## UPDATE 3 — ABD Denkliği Eklenmesi

**Etkilenen dosyalar:** `hakkimda.html`, `en/about.html`

**Diploma yanına küçük not (Uludağ ve Arel diplomaları için):**
> TR: "Diplomaları ABD denkliğine sahiptir."  
> EN: "Holds U.S. credential equivalency for both degrees."

**Hakkımda marketing paragrafına ekleme (40 soft / 60 bold ton):**
- Eğitim geçmişini anlatan bölüme ABD denkliği doğal bir güven unsuru olarak yedirilecek
- "Lisans verildi" algısı yaratılmayacak, uluslararası kalite güvencesi izlenimi verilecek
- Örnek ton: *"Lisans ve yüksek lisans diplomaları ABD denkliğine sahip olan Kübra Engüdar, uluslararası alanda tanınan bir eğitim geçmişiyle online danışmanlık sunmaktadır."*

---

## UPDATE 4 — Terapi/Seans Terminoloji Değişikliği

**Etkilenen dosyalar:** `index.html`, `hakkimda.html`, `en/index.html`, `en/about.html`  
**Dokunulmayacak:** Blog yazıları ve `blog.html` / `en/blog.html` listeleri

| Eski | Yeni |
|------|------|
| terapi | danışmanlık |
| seans | görüşme |
| terapötik | bağlama göre değerlendirilecek |

**Not:** "Terapötik" kelimesinin geçtiği her yer ayrıca gözden geçirilecek, bağlama göre silinecek veya nötr ifadeyle değiştirilecek.

---

## UPDATE 5 — Blog Açıklama Metni Hizalaması

**Etkilenen dosyalar:** `blog.html`, `en/blog.html`

**Sorun:** Blog sayfasındaki açıklama metni ("Kaygı, ilişkiler, ebeveynlik...") sola yaslanmış görünüyor.

**Fix:** İlgili paragraf veya container'a `text-align:center` eklenecek.

---

## GENEL NOTLAR
- Tüm değişiklikler TR ve EN versiyonlarına eş zamanlı uygulanacak
- Blog yazılarının içeriklerine hiçbir değişiklik yapılmayacak
- Mobile fix tüm sayfalardaki `<style>` bloklarına ayrı ayrı uygulanacak
