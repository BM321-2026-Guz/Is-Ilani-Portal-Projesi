# Güvenlik Gereksinimleri (Security Requirements)

## BM321 - İş İlanı Portalı Projesi
**Sprint:** 1 (4. Hafta)  
**Sorumlu Rol:** DevSecOps & Security Specialist  
**Durum:** Taslak güvenlik gereksinimleri

## 1. Amaç

Bu doküman, üniversite öğrencileri için geliştirilen İş İlanı Portalı'nın güvenlik gereksinimlerini tanımlar.

Sistemde öğrenci (student) ve işe alım uzmanı (recruiter) olmak üzere iki kullanıcı rolü bulunmaktadır.

Amaç; kullanıcı hesaplarını, kişisel bilgileri, iş ilanlarını ve başvuruları yetkisiz erişimlere karşı korumaktır.

## 2. Kimlik Doğrulama (Authentication)

**SEC-01:** Kullanıcılar e-posta ve şifre ile kayıt olabilmelidir.

**SEC-02:** Kullanıcı şifreleri veritabanında düz metin olarak saklanmamalı, Argon2id veya güvenli yapılandırılmış bcrypt ile hashlenmelidir.

**SEC-03:** Başarılı giriş işleminden sonra kullanıcıya JWT erişim token'ı verilmelidir.

**SEC-04:** JWT imzası, geçerlilik süresi ve beklenen algoritması backend tarafından doğrulanmalıdır.

**SEC-05:** Geçersiz veya süresi dolmuş token ile korunan API'lere erişim engellenmelidir.

**SEC-06:** JWT imzalama anahtarları kaynak kodda tutulmamalı ve GitHub'a yüklenmemelidir.

## 3. Yetkilendirme (Authorization)

**SEC-07:** Sistem öğrenci (student) ve işe alım uzmanı (recruiter) rollerini desteklemelidir.

**SEC-08:** Yalnızca recruiter rolündeki kullanıcılar iş ilanı oluşturabilmeli, güncelleyebilmeli ve kapatabilmelidir.

**SEC-09:** Yalnızca student rolündeki kullanıcılar iş ilanlarına başvurabilmelidir.

**SEC-10:** Öğrenciler yalnızca kendi profillerini ve başvurularını değiştirebilmelidir.

**SEC-11:** İşe alım uzmanları yalnızca kendilerine ait ilanları yönetebilmeli ve bu ilanlara gelen başvuruları görüntüleyebilmelidir.

**SEC-12:** Kullanıcıların kayıt veya profil güncelleme işlemleriyle izin verilmeyen roller kazanması engellenmelidir.

## 4. API Güvenliği

**SEC-13:** Korunan API endpoint'lerinde JWT Bearer kimlik doğrulaması uygulanmalıdır.

**SEC-14:** Yetkisiz veya kimliği doğrulanmamış istekler uygun HTTP hata kodlarıyla reddedilmelidir.

- 401 Unauthorized: Geçerli kimlik doğrulaması bulunmuyor.
- 403 Forbidden: Kullanıcının işlem için yeterli yetkisi bulunmuyor.

**SEC-15:** API'ye gönderilen kullanıcı verileri sunucu tarafında doğrulanmalıdır.

**SEC-16:** Giriş ve kayıt endpoint'lerinde kötüye kullanımı azaltacak istek sınırlama mekanizmaları uygulanmalıdır.

## 5. Kişisel Verilerin Korunması

**SEC-17:** Kullanıcıların kişisel bilgilerine yalnızca yetkili kullanıcılar erişebilmelidir.

**SEC-18:** Öğrencilerin CV ve portföy bilgileri yalnızca ilgili başvuruları inceleme yetkisi olan işe alım uzmanlarına gösterilmelidir.

**SEC-19:** API yanıtlarında şifreler, şifre hashleri ve gizli anahtarlar bulunmamalıdır.

**SEC-20:** Uygulama canlı ortamda HTTPS üzerinden hizmet vermelidir.

## 6. Güvenlik Testleri ve Kontrolleri

Aşağıdaki testlerin geliştirme aşamasında gerçekleştirilmesi planlanmaktadır:

| Test | Beklenen Sonuç |
|---|---|
| Yanlış şifreyle giriş | Giriş reddedilir |
| Geçersiz JWT ile erişim | 401 |
| Süresi dolmuş JWT ile erişim | 401 |
| Student rolüyle ilan oluşturma | 403 |
| Recruiter rolüyle ilana başvurma | 403 |
| Başkasının profilini değiştirme | Erişim reddedilir |
| Başka işverenin başvurularını görüntüleme | Erişim reddedilir |
| API yanıtında şifre bilgisi bulunması | Hassas bilgi döndürülmez |

Bu testler henüz gerçekleştirilmemiştir. Sonuçlar uygulama geliştirildikten sonra kaydedilecektir.

## 7. Sprint Planı

### Sprint 1 - 4. Hafta
- Güvenlik gereksinimlerinin belirlenmesi.
- Mevcut OpenAPI sözleşmesinin güvenlik açısından incelenmesi.
- JWT ve kullanıcı rollerine ilişkin güvenlik kurallarının belgelenmesi.

### Sprint 2 - 7. Hafta
- OWASP Top 10 güvenlik şartnamesinin hazırlanması.
- Güvenlik risklerinin değerlendirilmesi.
- SAST/DAST ve bağımlılık tarama yaklaşımının planlanması.

### Sprint 3 - 10. Hafta
- Geliştirilen güvenlik kontrollerinin incelenmesi.
- API kimlik doğrulama ve yetkilendirme testlerinin yapılması.

### Final - 13-14. Haftalar
- Son güvenlik kontrollerinin gerçekleştirilmesi.
- Güvenlik bulgularının ve alınan önlemlerin teknik rapora eklenmesi.

## 8. Referanslar

- `docs/openapi.yaml`
- `docs/sistem-vizyonu-ve-sinirlar.md`
- `docs/urun-backlogu.md`
- OWASP Top 10
- OWASP API Security Top 10
