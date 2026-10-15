# Katkı Rehberi

## Branch stratejisi (Git-Flow)
- `main`: sadece kararlı sürümler
- `develop`: entegrasyon dalı
- `feature/<kisa-aciklama>`: yeni iş, develop'tan açılır, develop'a PR ile döner
- `release/<surum>`: sürüm hazırlığı
- `hotfix/<aciklama>`: main'deki acil düzeltme

## İsimlendirme
Küçük harf, tire ile, Türkçe karakter yok. Örn: `feature/kullanici-girisi`

## Commit mesajları
`tip: kısa açıklama` (feat, fix, docs, chore, ci). Örn: `docs: proje önerisi eklendi`

## PR süreci
1. develop'tan branch aç
2. Küçük ve odaklı commit'ler at
3. PR aç, şablonu doldur
4. CI yeşil olmalı, en az 1 onay gerekir
5. Merge sonrası branch'i sil
