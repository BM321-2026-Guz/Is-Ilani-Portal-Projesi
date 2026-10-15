# Proje öneri dokümanı

Sürüm: Sprint 1 başlangıcı  
Tarih: 15 Ekim 2026  
Ders: BM 321 Yazılım Mühendisliği  
Proje: İş İlanı Portalı  
Depo: [BM321-2026-Guz/Is-Ilani-Portal-Projesi](https://github.com/BM321-2026-Guz/Is-Ilani-Portal-Projesi)

## Problem

Üniversite öğrencileri ve yeni mezunlar staj ile yarı zamanlı iş ararken genel iş platformlarında deneyimli adaylarla aynı havuzda yarışır. Bu platformlar öğrenciyi, okulunu ve öğrenim yılını ayırmaz. İlanların çoğu tam zamanlı ve tecrübe ister.

Öğrenci arayan şirketlerin de sorunu vardır. Başvuranlar arasından yalnızca üniversite öğrencilerini ayıklamak için ayrı bir süzgeçleri yoktur.

## Öneri

Yalnızca üniversite öğrencilerine açık bir iş ilanı portalı.

İşe alım uzmanı staj veya yarı zamanlı ilan yayınlar. Öğrenci profilindeki okul, bölüm, beceri ve portföy linkiyle başvurur. İşe alım uzmanı kendi ilanının adaylarını görür ve kısa listeye alır ya da reddeder.

İlk sürümün kabul akışı: ilan yayınla, başvur, kısa listeye al.

## Kullanıcılar

- **Öğrenci.** İlanları inceler, profilini tutar, başvurur, sonucunu görür.
- **İşe alım uzmanı.** Şirket adına ilan açar, adayları inceler, durumu günceller.

Başka kullanıcı rolü yoktur.

## Kapsam

İçinde:

- İki rolle kayıt ve JWT ile giriş
- Öğrenci profili ve işe alım profili
- Açık ilanların herkese listelenmesi
- Başvuru, aday listesi, kısa liste ve ret

Dışında:

- Yönetici rolü, mesajlaşma, ödeme, tam zamanlı genel iş ilanı
- Dosya yükleme. Portföy ve CV birer bağlantıdır
- Ayrı mikroservisler

Kapsam değişirse ürün sahibi backlog’u, mimar API sözleşmesini günceller.

## Başarı

Aşağıdaki yol, ek işlev olmadan, baştan sona çalışır:

1. İşe alım uzmanı hesap açar ve bir staj ya da yarı zamanlı ilan yayınlar.
2. Öğrenci hesap açar, profiline portföyünü yazar ve o ilana başvurur.
3. İşe alım uzmanı adayı görür ve kısa listeye alır.
4. Öğrenci başvurusunun kısa listede olduğunu görür.

## Teknoloji

MERN: MongoDB, Express, React, Node.js. Kimlik doğrulama JWT. Sözleşme koddan önce yazılır; taslak `docs/openapi.yaml` dosyasındadır. Sistemin sınırı `docs/sistem-vizyonu-ve-sinirlar.md` dosyasındadır.

Şekil, modüler tek servistir. Bir web istemcisi, bir API, bir veritabanı.

## Lisans

Açık kaynak lisansı **MIT**’tir. Metin depo kökündeki `LICENSE` dosyasındadır.

MIT, kodun kullanılmasını, değiştirilmesini ve paylaşılmasını serbest bırakır; lisans metninin kopyada kalmasını şart koşar. React ve Express bu lisansla uyumludur. Yeni bir bağımlılık MIT ile çatışırsa, eklenmeden önce DevSecOps bakar.

## Takım

| Üye | Rol |
|---|---|
| Tuğberk | Product Owner ve Requirements Engineer |
| Cem | Scrum Master ve Agile Process Coach |
| Yusuf | Lead Software Architect ve Tech Lead |
| Eda | QA ve Test Automation Engineer |
| Deniz Tuna | DevOps ve CI/CD Infrastructure Engineer |
| Esma | DevSecOps ve Security Specialist |

Görev dağılımı `docs/takim-ve-raci.md` dosyasındadır. Başlangıç backlog’u `docs/urun-backlogu.md` dosyasındadır.

## Bu sprintte teslim edilen belgeler

| Belge | Dosya |
|---|---|
| Proje önerisi ve problem tanımı | `docs/proje-oneri-dokumani.md` |
| Sistem vizyonu ve sınırları | `docs/sistem-vizyonu-ve-sinirlar.md` |
| Taslak API sözleşmesi | `docs/openapi.yaml` |
| Takım rolleri ve RACI | `docs/takim-ve-raci.md` |
| GitHub organizasyonu ve Git-Flow | `docs/git-flow.md` |
| Başlangıç ürün backlog’u | `docs/urun-backlogu.md` |
| Lisans | `LICENSE` |

Çalışan ürün, C4 modeli ve UML bu sprintin teslimi değildir.
