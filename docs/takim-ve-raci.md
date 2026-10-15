# Takım rolleri ve RACI

Sürüm: Sprint 1 başlangıcı  
Tarih: 15 Ekim 2026

Altı üye, altı rol. Her üyenin hesaptan sorumlu olduğu bir alan vardır.

| Üye | Rol | Hesaptan sorumlu olduğu alan |
|---|---|---|
| Tuğberk | Product Owner ve Requirements Engineer | Gereksinim, kullanıcı hikâyesi, kabul kriteri, backlog önceliği, ürün kabulü |
| Cem | Scrum Master ve Agile Process Coach | Çevik süreç, daily, retrospective, engel, RACI’nin işletilmesi, pano |
| Yusuf | Lead Software Architect ve Tech Lead | Sistem sınırı, API-First sözleşme, C4 ve UML, Git-Flow kuralı, pull request incelemesi, mimari savunma |
| Eda | QA ve Test Automation Engineer | Birim, entegrasyon ve E2E testleri, %50 ve üzeri birim test kapsamı |
| Deniz Tuna | DevOps ve CI/CD Infrastructure Engineer | GitHub Actions, Docker, docker-compose, tek komutla ayağa kalkma |
| Esma | DevSecOps ve Security Specialist | OWASP Top 10, SAST/DAST, JWT katmanının sertleştirilmesi, bağımlılıkların MIT ile uyumu |

## Matris

Harfler:

- **R:** işi yapar
- **A:** hesaptan sorumludur. Her satırda tek A vardır
- **C:** danışılır
- **I:** haberdar edilir

| İş paketi | Tuğberk | Cem | Yusuf | Eda | Deniz Tuna | Esma |
|---|---|---|---|---|---|---|
| Proje önerisi, problem, kapsam | A/R | I | C | I | I | I |
| Ürün backlog’u, kabul kriteri, öncelik | A/R | C | C | C | I | I |
| Çevik süreç, pano, engel | C | A/R | I | I | I | I |
| Sistem vizyonu, OpenAPI, Git-Flow | C | I | A/R | C | C | C |
| C4, UML, mimari savunma | I | I | A/R | C | I | C |
| Test ve kapsam oranı | C | I | C | A/R | I | C |
| CI/CD, Docker, dağıtım | I | I | C | C | A/R | C |
| Güvenlik, JWT sertleştirme, lisans uyumu | I | I | C | I | C | A/R |
| Ürün kabulü | A/R | I | C | C | I | I |

Ürün özelliğini, backlog’tan o işi alan üye geliştirir. Pull request’i Lead Software Architect inceler. Model, route, klasör yapısı veya API sözleşmesi değişiyorsa bu inceleme olmadan `develop` dalına girmez. Kimlik, JWT, yetki veya şifre değişiyorsa Esma’nın onayı da gerekir. Docker, CI veya ortam değişiyorsa Deniz Tuna’nın onayı da gerekir.

## Sprint sınırı

Bu matris dönem boyu geçerlidir. Sprint 1’de üretilen şey belgedir. Test kodu, pipeline, Docker ve güvenlik taraması kendi sprintlerinde, yukarıdaki sahibinin hesabındadır.
