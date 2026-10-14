# Başlangıç ürün backlog’u

Sürüm: Sprint 1 başlangıcı  
Tarih: 15 Ekim 2026  
Bu dosya başlangıç taslağıdır. Şartname backlog için bir dosya türü söylemez. Tam puan için hikâyeler Jira veya GitHub panosunda güncel durur.  
Sahip: Product Owner. Sözleşme: `docs/openapi.yaml`.

Puanlar göreli efordur, saat değildir. Dizi: 1, 2, 3, 5, 8. Bu listedeki bütün kalemler ilk sürümün kabul akışı için gereklidir.

Toplam: 45 puan.

## Kimlik ve profil

### US-01 Öğrenci kaydı

Puan: 3. Öncelik: yüksek.

Bir üniversite öğrencisi olarak öğrenci rolüyle hesap açmak istiyorum, böylece ilanlara başvurabileyim.

Kabul kriterleri:

- Kayıt e-posta, en az 8 karakterlik şifre, rol `student`, okul ve bölüm ister.
- Aynı e-posta ile ikinci kayıt 409 döner.
- Yanıtta JWT ve profil vardır. Şifre yanıtta yer almaz.

### US-02 İşe alım uzmanı kaydı

Puan: 3. Öncelik: yüksek.

Bir işe alım uzmanı olarak şirketim adına hesap açmak istiyorum, böylece ilan yayınlayabileyim.

Kabul kriterleri:

- Kayıt rol `recruiter` ve şirket adı ister.
- İşe alım hesabı öğrenci profili taşımaz. Öğrenci hesabı şirket profili taşımaz.
- Yanıtta JWT ve profil vardır.

### US-03 Giriş

Puan: 3. Öncelik: yüksek.

Kayıtlı bir kullanıcı olarak giriş yapmak istiyorum, böylece kendi işlerimi yapabileyim.

Kabul kriterleri:

- Doğru e-posta ve şifre JWT döner.
- Yanlış şifre 401 döner.
- `GET /api/auth/me` bu belirteçle kullanıcıyı ve profili döner. Belirteç yoksa 401 döner.

### US-04 Öğrenci profili

Puan: 5. Öncelik: yüksek.

Bir öğrenci olarak okulum, bölümüm, becerilerim, portföy ve CV bağlantım güncel kalsın istiyorum, böylece başvuru beni doğru anlatsın.

Kabul kriterleri:

- Öğrenci `PATCH /api/students/me` ile profilini günceller.
- İşe alım uzmanı bu uca istek atarsa 403 döner.
- Portföy ve CV birer bağlantıdır. Dosya yüklenmez.

### US-05 İşe alım profili

Puan: 2. Öncelik: yüksek.

Bir işe alım uzmanı olarak şirket adımı ve ünvanımı güncellemek istiyorum.

Kabul kriterleri:

- İşe alım uzmanı `PATCH /api/recruiters/me` ile profilini günceller.
- Öğrenci bu uca istek atarsa 403 döner.
- Şirket adı, ilan kartında görünür.

## İlan

### US-06 Açık ilanları görme

Puan: 3. Öncelik: yüksek.

Bir ziyaretçi olarak giriş yapmadan staj ve yarı zamanlı ilanları görmek istiyorum.

Kabul kriterleri:

- `GET /api/jobs` belirteç istemez.
- Yalnızca durumu açık olan ilanlar döner.
- Tür süzgeci `internship` ve `part-time` değerlerini kabul eder.
- Her ilanda başlık, tür, konum, son tarih ve şirket adı vardır.

### US-07 İlan detayı

Puan: 2. Öncelik: yüksek.

Bir ziyaretçi olarak bir ilanın açıklamasını okumak istiyorum.

Kabul kriterleri:

- `GET /api/jobs/{jobId}` belirteç istemez.
- Olmayan ilan 404 döner.

### US-08 İlan yayınlama

Puan: 5. Öncelik: yüksek.

Bir işe alım uzmanı olarak staj veya yarı zamanlı ilan yayınlamak istiyorum.

Kabul kriterleri:

- `POST /api/jobs` yalnızca `recruiter` rolüne açıktır. Öğrenci 403 döner.
- Başlık, açıklama ve tür zorunludur.
- Yeni ilanın durumu `open` olur ve `recruiterId` oturumdaki kullanıcıdır.

### US-09 İlanı güncelleme ve kapatma

Puan: 3. Öncelik: yüksek.

Bir işe alım uzmanı olarak yalnızca kendi ilanımı düzeltmek veya kapatmak istiyorum.

Kabul kriterleri:

- `PATCH /api/jobs/{jobId}` ve `POST /api/jobs/{jobId}/close` ilanın sahibine açıktır.
- Başka bir işe alım uzmanı 403 döner.
- Kapanan ilan açık listeden düşer.

## Başvuru

### US-10 Başvuru

Puan: 5. Öncelik: yüksek.

Bir öğrenci olarak açık bir ilana profilimdeki portföyle başvurmak istiyorum.

Kabul kriterleri:

- `POST /api/jobs/{jobId}/applications` yalnızca `student` rolüne açıktır.
- İşe alım uzmanı başvuramaz.
- Kapalı veya olmayan ilana başvuru yapılamaz.
- Aynı öğrenci aynı ilana ikinci kez başvuramaz; yanıt 409 olur.
- Başvurunun ilk durumu `applied` olur. İsteğe bağlı bir not eklenebilir.

### US-11 Başvurularım

Puan: 3. Öncelik: yüksek.

Bir öğrenci olarak kendi başvurularımın durumunu görmek istiyorum.

Kabul kriterleri:

- `GET /api/applications/me` yalnızca oturumdaki öğrencinin başvurularını döner.
- Durum `applied`, `shortlisted` veya `rejected` olabilir.
- İşe alım uzmanı bu ucu kullanamaz.

### US-12 Aday listesi

Puan: 5. Öncelik: yüksek.

Bir işe alım uzmanı olarak kendi ilanıma kimlerin başvurduğunu ve portföylerini görmek istiyorum.

Kabul kriterleri:

- `GET /api/jobs/{jobId}/applications` yalnızca ilanın sahibine açıktır.
- Her adayda başvuru notu, durum ve öğrenci profili vardır.
- Öğrenci bu listeyi göremez.

### US-13 Kısa liste ve ret

Puan: 3. Öncelik: yüksek.

Bir işe alım uzmanı olarak adayı kısa listeye almak veya reddetmek istiyorum.

Kabul kriterleri:

- `PATCH /api/applications/{applicationId}` durumu `shortlisted` veya `rejected` yapar.
- İstek, ilanın sahibi olmayan bir kullanıcıdan gelirse 403 döner.
- Öğrenci kendi başvurusunun durumunu değiştiremez.
- Kısa listeye alınan öğrenci, kendi başvuru listesinde yeni durumu görür.

## Bilinçli olarak bu listede olmayanlar

Sonraki sprintlerin işidir, bu backlog’a puanlanmamıştır:

- Ayrıntılı SRS, NFR, SLA ve SLO
- Figma prototipi
- OWASP şartnamesi ve SAST/DAST
- C4, UML ve çalışan MVP
- GitHub Actions, Docker, E2E raporu, SonarQube
