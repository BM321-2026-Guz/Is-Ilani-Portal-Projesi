# Git-Flow ve GitHub organizasyonu

Sürüm: Sprint 1 başlangıcı  
Tarih: 15 Ekim 2026

## Organizasyon

- Organizasyon: [BM321-2026-Guz](https://github.com/BM321-2026-Guz)
- Depo: [Is-Ilani-Portal-Projesi](https://github.com/BM321-2026-Guz/Is-Ilani-Portal-Projesi)
- Lisans: MIT (`LICENSE`)

## Dallar

Şartnamenin saydığı dallar: `main`, `develop`, `feature/`.

| Dal | Anlamı |
|---|---|
| `main` | Yayınlanan kod. Doğrudan push yok. |
| `develop` | Entegrasyon dalı. İş buraya pull request ile girer. |
| `feature/<iş>` | Tek iş. `develop` dalından açılır, birleşince silinir. |

Kişisel dal açılmaz. Dal adında kişi adı veya rol kodu yer almaz.

## Şu anki dallar

Üç dal yeter. Başka dal açılmaz.

| Dal | Durum |
|---|---|
| `main` | Yayın dalı. Uzaktaki depoda var. |
| `develop` | Entegrasyon dalı. Yerelde açıldı. |
| `feature/project-foundation` | Sprint 1 belge seti. Yerelde açıldı. |

Yeni bir `feature/` dalı, o iş gerçekten başlayınca `develop` dalından açılır. Önceden dal listesi tutulmaz.

Dal adı işi tarif eder: İngilizce, küçük harf, kelimeler kısa çizgiyle ayrılır. Kişi adı ve rol kodu yazılmaz.

## Akış

1. Dalı güncel `develop` dalından aç.
2. Tek iş koy. `main` ve `develop` dallarına doğrudan push yapma.
3. Pull request’i `develop` dalına aç.
4. Onaydan sonra birleştir ve dalı sil.
5. Yayın hazır olunca `develop` dalından `main` dalına ayrı bir pull request açılır.

## Onay

- Model, route, klasör yapısı, API sözleşmesi: Lead Software Architect onayı şart.
- Login, JWT, yetki, şifre: DevSecOps onayı da şart.
- Docker, CI, ortam: DevOps onayı da şart.
- Diğer işler: en az bir takım arkadaşı.

Karar: `main` ve `develop` dallarına doğrudan push yapılmaz. Pull request zorunludur, en az bir onay gerekir, admin bu kuralı aşamaz. Kuralı mimar koyar. Scrum Master işletir.

## Bu dal

`feature/project-foundation`

Sprint 1 belge seti bu daldadır. Çalışan ürün bu teslimde yoktur.
