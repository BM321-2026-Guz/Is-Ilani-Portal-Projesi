# Ürün Backlog'u (Product Backlog)

## Proje Kapsamı ve Kurallar
- **Aktörler:** Öğrenci (`student`), İşe Alım Uzmanı (`recruiter`)
- **İlan Tipleri:** Staj (`internship`), Yarı Zamanlı (`part-time`)
- **İlan Durumları:** Açık (`open`), Kapalı (`closed`)
- **Başvuru Durumları:** Başvuruldu (`applied`), Kısa Listeye Alındı (`shortlisted`), Reddedildi (`rejected`)

---

## Kullanıcı Hikâyeleri (User Stories)

### US-01: Kullanıcı Kaydı ve Girişi (Auth)
**Hikâye:** Bir Öğrenci veya İşe Alım Uzmanı olarak, sisteme güvenli şekilde kayıt olmak ve JWT ile giriş yapmak istiyorum.
**Kabul Kriterleri:**
- Kullanıcılar e-posta ve şifre ile kayıt olabilmeli, rollerini (`student` veya `recruiter`) belirtebilmelidir.
- Başarılı girişte JWT token dönmelidir.
**Story Point:** 5
**Öncelik:** Yüksek (P1)

---

### US-02: Öğrenci Profili Oluşturma ve Güncelleme
**Hikâye:** Bir Öğrenci olarak; okul, bölüm, beceriler, portföy bağlantısı ve CV bağlantısı bilgilerimi profilime eklemek ve güncellemek istiyorum.
**Kabul Kriterleri:**
- Öğrenci okul, bölüm, beceriler, portföy ve CV linklerini profilinde görebilmeli ve düzenleyebilmelidir.
- Profil bilgileri işe alım uzmanları tarafından başvuru incelemesinde görüntülenebilmelidir.
**Story Point:** 3
**Öncelik:** Yüksek (P1)

---

### US-03: İşe Alım Uzmanı Profili Oluşturma
**Hikâye:** Bir İşe Alım Uzmanı olarak; şirket adı ve ünvan bilgilerimi profilime eklemek istiyorum.
**Kabul Kriterleri:**
- İşe alım uzmanı şirket adı ve ünvanını belirtebilmelidir.
**Story Point:** 2
**Öncelik:** Orta (P2)

---

### US-04: İlan Yayınlama (Staj veya Yarı Zamanlı)
**Hikâye:** Bir İşe Alım Uzmanı olarak; staj (`internship`) veya yarı zamanlı (`part-time`) iş ilanı oluşturmak ve yayınlamak istiyorum.
**Kabul Kriterleri:**
- İlan tipi yalnızca `internship` veya `part-time` olabilir.
- Yeni yayınlanan ilan varsayılan olarak `open` durumunda olmalıdır.
**Story Point:** 5
**Öncelik:** Yüksek (P1)

---

### US-05: İlan Durumu Yönetimi (Açık/Kapalı)
**Hikâye:** Bir İşe Alım Uzmanı olarak; yayınladığım ilanların durumunu `open` veya `closed` olarak değiştirebilmek istiyorum.
**Kabul Kriterleri:**
- İşe alım uzmanı ilanını kapattığında status `closed` olmalı ve yeni başvuru kabul edilmemelidir.
**Story Point:** 2
**Öncelik:** Orta (P2)

---

### US-06: İlanları Listeleme ve İlan Detayı Görme
**Hikâye:** Bir Öğrenci olarak; açık iş ilanlarını listelemek ve detaylarını incelemek istiyorum.
**Kabul Kriterleri:**
- Sadece `open` durumundaki ilanlar listelenebilmelidir.
- İlan detayında ilan tipi, açıklama ve şirket bilgisi yer almalıdır.
**Story Point:** 3
**Öncelik:** Yüksek (P1)

---

### US-07: Portföy Bağlantısı ile İlana Başvurma
**Hikâye:** Bir Öğrenci olarak; profilimdeki portföy bağlantım ile açık bir ilana başvurmak istiyorum.
**Kabul Kriterleri:**
- Öğrenci başvurduğunda başvuru durumu otomatik olarak `applied` olmalıdır.
- Profildeki portföy ve CV bağlantıları başvuruya dahil edilmelidir.
**Story Point:** 5
**Öncelik:** Yüksek (P1)

---

### US-08: Başvuru Değerlendirme (Kısa Liste / Red)
**Hikâye:** Bir İşe Alım Uzmanı olarak; ilanıma gelen başvuruları inceleyip durumunu `shortlisted` veya `rejected` olarak güncellemek istiyorum.
**Kabul Kriterleri:**
- İşe alım uzmanı adayın portföyünü inceleyip adayı kısa listeye alabilir (`shortlisted`) veya reddedebilir (`rejected`).
**Story Point:** 3
**Öncelik:** Yüksek (P1)
