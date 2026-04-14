# kubraengudar.com — Proje Görüşme Notları

**Tarih:** 14 Nisan 2026  
**Katılımcılar:** Batu (Teknik), Kübra Turan Engüdar  
**Proje:** kubraengudar.com — Kişisel/Profesyonel Psikolog Web Sitesi

---

## Mevcut Durum

Site şu anda yayında ve temel yapı tamamlanmış durumda:

- **Domain:** kubraengudar.com (Namecheap → Vercel)
- **Sayfalar:** index.html (ana sayfa) + hakkimda.html (hakkımda)
- **İletişim formu:** Formspree üzerinden aktif (bildirimler tturankubra@gmail.com adresine gidiyor)
- **Deploy:** GitHub main branch'e push → Vercel otomatik deploy

---

## Tamamlanan İşler

| # | İş | Durum |
|---|-----|-------|
| 1 | Site tasarımı ve kodlama | ✅ |
| 2 | Domain bağlantısı (Namecheap → Vercel) | ✅ |
| 3 | Formspree entegrasyonu | ✅ |
| 4 | Hakkımda sayfası (eğitim, sertifikalar, üyelikler) | ✅ |
| 5 | Mobil uyumluluk (responsive) | ✅ |
| 6 | Schema.org SEO yapılandırması | ✅ |

---

## Yapılacaklar — Karar Bekleyen Maddeler

### 1. Cal.com Randevu Sistemi
- Cal.com hesabı açılacak
- Google Calendar bağlanacak
- Booking linki alınıp siteye entegre edilecek
- **Kübra'dan beklenen:** Uygun seans saatleri ve gün bilgisi, seans süresi, online mı yüz yüze mi, ücretlendirme bilgisi

### 2. Google Search Console Kaydı
- kubraengudar.com eklenmesi gerekiyor
- Meta verification tag alınıp index.html'e eklenecek
- Sitemap submit edilecek
- **Kübra'dan beklenen:** Google hesap erişimi veya Batu'nun kendi hesabıyla mı yapılacağı

### 3. Sitemap Oluşturma
- sitemap.xml hazırlanacak (Batu + Claude)
- Mevcut sayfalar: `/`, `/hakkimda`
- Blog sayfaları eklendiğinde güncellenecek

### 4. Blog Sistemi
- Henüz CMS kararı verilmedi
- **Seçenekler:** Statik HTML blog yazıları, headless CMS (Contentful, Sanity), veya basit markdown tabanlı çözüm
- **Kübra'dan beklenen:** Blog yazma sıklığı tahmini, hangi konularda yazacağı, görseller nasıl hazırlanacak

### 5. Google Ads
- Henüz planlanmadı
- **Kübra'dan beklenen:** Bütçe ve hedef kitle bilgisi, ne zaman başlamak istediği

---

## İçerik Review — Kübra'nın Kontrol Etmesi Gerekenler

Aşağıdaki metinlerin doğruluğu ve uygunluğu Kübra tarafından onaylanmalı:

- [ ] Ana sayfa hero metni: *"Sağlıklı zihin, sağlıklı yaşam"*
- [ ] Alıntı: *"Kendinize zaman ayırmak, yaşamınızın her alanına yansır."*
- [ ] Hakkımda sayfasındaki biyografi paragrafları
- [ ] 6 hizmet kartının başlık ve açıklamaları
- [ ] Süreç bölümündeki 3 adım açıklamaları
- [ ] Blog placeholder başlıkları ve tarihleri
- [ ] Eğitim ve sertifika listesinin eksiksizliği
- [ ] Üyelik listesinin güncelliği

---

## Görseller

| Görsel | Konum | Durum |
|--------|-------|-------|
| hero.jpg | Ana sayfa hero alanı | Mevcut |
| kubra.jpg | Hakkımda + Ana sayfa about | Mevcut |
| Blog görselleri | Blog kartları | ⬜ Henüz yok (gradient placeholder) |

- **Kübra'dan beklenen:** Blog görselleri için fotoğraf veya görsel tercihi

---

## Teknik Notlar (Batu İçin)

- Tüm değişiklikler (içerik + Cal.com + Search Console + sitemap) tek commit'te toplanacak
- Formspree form ID sabit: `xaqlllkn` — değiştirilmeyecek
- vercel.json'da cleanUrls aktif → `/hakkimda` şeklinde çalışıyor
- Dil switcher (TR/EN) şu an görsel — İngilizce sayfa henüz yok

---

## Sonraki Adımlar

1. Kübra içerik review'unu tamamlar
2. Cal.com hesabı açılır ve yapılandırılır
3. Google Search Console kaydı yapılır
4. sitemap.xml oluşturulup repo'ya eklenir
5. Tüm değişiklikler tek commit ile deploy edilir
6. Blog stratejisi belirlenir

---

*Bu doküman her görüşme sonrası güncellenecektir.*
