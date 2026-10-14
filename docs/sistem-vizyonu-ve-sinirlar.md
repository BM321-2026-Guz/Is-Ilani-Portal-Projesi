# Sistem vizyonu ve sınırları şartnamesi

Sürüm: Sprint 1  
Tarih: 15 Ekim 2026  
Sahip: Lead Software Architect ve Tech Lead  
Durum: Sprint 1 mimar teslimi

Bu belge, sistemin ne olduğunu ve nereye kadar uzandığını sabitler. Uçların ayrıntısı `docs/openapi.yaml` dosyasındadır. Dal kuralı `docs/git-flow.md` dosyasındadır.

Bu belge C4 modeli değildir. C4 ve UML 10. haftanın teslimidir.

## Amaç

Üniversite öğrencileri staj ve yarı zamanlı iş ararken genel platformlarda deneyimli adaylarla aynı havuzda kalır. Öğrenci arayan şirket de başvurular arasından yalnızca üniversite öğrencisini ayıramaz.

Sistem, yalnız bu iki iş için bir portal kurar. İşe alım uzmanı staj veya yarı zamanlı ilan yayınlar. Öğrenci, profilindeki portföyle başvurur. İşe alım uzmanı kendi ilanının adaylarını görür ve kısa listeye alır ya da reddeder.

Kabul akışı: ilan yayınla → başvur → kısa listeye al.

## Sistem

Sistemin adı İş İlanı Portalıdır. Üç parçadan oluşur:

- React web istemcisi
- Express API
- MongoDB

İstemci ile API arasında HTTP ve JSON vardır. API ile veritabanı sistemin içindedir. Dışarıya açılan kapı API sözleşmesidir.

## Paydaşlar

Atamadaki paydaşlar bunlardır. Başka kullanıcı rolü yoktur.

| Paydaş | Sistemdeki rol | İhtiyacı |
|---|---|---|
| Öğrenci | `student` | Staj ve yarı zamanlı ilanları görür, portföyüyle başvurur, sonucu izler |
| İşe alım uzmanı | `recruiter` | İlan yayınlar, yalnızca öğrencilerden gelen başvuruları görür, kısa listeye alır veya reddeder |

Atamadaki “işe alım sorumlusu” ile “işe alım uzmanı” aynı paydaştır. Metinlerde ünvan **işe alım uzmanı**, API rolü `recruiter` olarak durur.

## Sınırın içi

- Kayıt ve giriş. Rol kayıtta seçilir. Kimlik belirteci JWT’dir.
- Öğrenci profili: okul, bölüm, beceriler, portföy bağlantısı, CV bağlantısı.
- İşe alım profili: şirket adı, ünvan. Şirket adı ilan kartında görünür.
- İlan: staj (`internship`) veya yarı zamanlı (`part-time`). Durum açık veya kapalıdır.
- Başvuru: `applied`, sonra `shortlisted` veya `rejected`.
- Başvuru, öğrencinin o andaki profilini taşır. Portföy başvuru formuna ayrıca yazılmaz ve dosya olarak yüklenmez.

Filtrelenmiş öğrenci havuzu, herkese açık bir öğrenci dizini değildir. Havuz, bir ilana başvuran öğrencilerdir. Yalnızca öğrenci rolü başvurabildiği için aday listesi üniversite öğrencilerinden oluşur.

## Sınırın dışı

Atamada olmayan ve bu sürümde kurulmayan şeyler:

- LinkedIn, Naukri veya başka bir ilan platformuyla entegrasyon. Bunlar problemin tarifidir, sistemin parçası değildir.
- Üniversite öğrenci işleri sisteminden veri çekmek
- Herkese açık öğrenci dizini
- Yönetici rolü, mesajlaşma, ödeme, tam zamanlı genel iş ilanı
- Dosya yükleme
- Ayrı mikroservisler
- Arayüz prototipi. Bu, 7. haftanın Figma teslimidir
- SLA, SLO ve ayrıntılı NFR. Bu, 7. haftanın teslimidir

Kapsam büyürse ürün sahibi backlog’u, mimar bu belgeyi ve OpenAPI dosyasını birlikte günceller.

## Sınırdaki arabirim

```text
Öğrenci ─────────────┐
                     │  tarayıcı
İşe alım uzmanı ─────┴── React istemcisi
                              │
                         HTTP / JSON
                              │
                         Express API ──── MongoDB
                              │
                         JWT ve rol kontrolü
```

Dış dünya sisteme yalnız bu API’den girer. İlan listesi ve ilan detayı belirteç istemez. Profil, ilan yönetimi ve başvuru JWT ister.

| Kim | Yapabildiği | Yapamadığı |
|---|---|---|
| Ziyaretçi | Açık ilanları ve ilan detayını okur | Başvuramaz, ilan açamaz |
| Öğrenci | Profilini günceller, açık ilana başvurur, kendi başvurularını görür | İlan açamaz, başkasının başvurusunu göremez, başvuru durumunu değiştiremez |
| İşe alım uzmanı | İlan açar, kendi ilanını günceller ve kapatır, kendi adaylarını görür, kısa listeye alır veya reddeder | Başvuru yapamaz, başkasının ilanını yönetemez |

Yetki kuralının tasarımı bu belgededir. JWT’nin sertleştirilmesi, OWASP incelemesi ve lisans uyumu DevSecOps rolündedir. O inceleme 7. haftanın güvenlik şartnamesine girer.

## Mimari karar

**API-First.** `docs/openapi.yaml` koddan önce yazılmış taslak sözleşmedir. İstemci ve API bu dosyaya uyar.

**Modüler tek servis.** Bir istemci, bir API, bir veritabanı. Atama MERN yığınını söyler. Takım altı kişidir. Bu koşullarda mikroservis kurulmaz.

API içindeki modül sınırları üç kaynaktır: kimlik, ilan, başvuru. İleride ayrılma gerekirse kesim bu kaynaklardan yapılır. Sprint 1’de ayrılma yoktur.

Lisans **MIT**’tir. Metin depo kökündeki `LICENSE` dosyasındadır.

## Sözleşmeye bağ

| Atamadaki iş | Uç |
|---|---|
| İki rolle kimlik | `register`, `login`, `getMe` |
| Öğrenci profili ve portföy | `updateStudentProfile` |
| İşe alım profili | `updateRecruiterProfile` |
| İlanları görme | `listJobs`, `getJob` |
| İlan yayınlama, düzeltme, kapatma | `createJob`, `updateJob`, `closeJob` |
| Portföyle başvuru | `applyToJob` |
| Öğrencinin kendi sonucu | `listMyApplications` |
| İşe alım uzmanının aday listesi | `listJobApplications` |
| Kısa liste veya ret | `updateApplicationStatus` |

## Sprint 1’de bu rolden kalan

Bu üç dosya, Lead Software Architect’in Sprint 1 teslimidir:

| Teslim | Dosya | Durum |
|---|---|---|
| Sistem vizyonu ve sınırları şartnamesi | `docs/sistem-vizyonu-ve-sinirlar.md` | Bu belge |
| Taslak OpenAPI sözleşmesi | `docs/openapi.yaml` | Taslak `0.1.0` |
| Git-Flow kuralı | `docs/git-flow.md` | `main`, `develop`, `feature/` |

Sprint 1’de bu rolden yazılmayanlar, takvime göre başkasına aittir: proje önerisinin ürün sahibi metni, RACI’nin işletilmesi, backlog panosu, Figma, SRS, NFR, OWASP şartnamesi, C4, UML, çalışan ürün, test kodu, CI ve Docker.
