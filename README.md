# SeansCure — Clinical Management Platform · Klinik Yönetim Platformu

[🇬🇧 English](#english) · [🇹🇷 Türkçe](#türkçe)

---

## English

A full-stack clinical management SaaS built for the Turkish healthcare market.
Designed for psychologists, dietitians, physiotherapists and clinic administrators.

**Live:** [seanscure.com](https://seanscure.com)

### Stack

| Layer | Technologies |
|---|---|
| Frontend | Vue 3, TypeScript, PrimeVue, Tailwind CSS |
| Backend | .NET 8, PostgreSQL, SignalR |
| Mobile | Capacitor (Android) |
| Infrastructure | Self-hosted key vault, Cloudflare |

### Key Technical Features

**End-to-End Encryption**
Patient data — names, clinical notes, identity numbers — is encrypted on the
client before it reaches the server. The backend stores only ciphertext and
cannot read the data it holds.

Built with the Web Crypto API using AES-256-GCM + RSA-OAEP hybrid encryption.
Each record gets a fresh 256-bit DEK wrapped in two independent RSA envelopes:
one for the record owner, one for backend key recovery via a self-hosted key vault.

→ [Encryption architecture](https://gist.github.com/mehmettalhaaksoy/1ebe8b6c288b5032de953640e9220b4c)
→ [vault.ts — core implementation](https://gist.github.com/mehmettalhaaksoy/4c299861e5d896b0be3a4a2418a89b5a)

**Role-Based Permission System**
Granular per-employee permission overrides on top of role defaults.
Supports mixed permission types: boolean flags, string enums, and
clinicEmployee ID arrays — all stored as JSONB and merged at query time.

**Real-Time Notifications**
SignalR hub with per-user and per-clinic group routing.
Appointment reminders, clinic invites, join requests — all pushed instantly.

**Appointment Scheduling**
Conflict detection, slot generation from weekly schedules, leave blocking,
public holiday awareness, per-session duration overrides.

**Multi-Platform**
Same codebase runs as a web app and native Android APK via Capacitor.
Platform-aware layout: sidebar navigation on web, bottom tab bar on mobile.

### Architecture Highlights

- **No plaintext on the wire** — E2EE enforced at the service layer
- **HMAC trigram search** — searchable encrypted names without exposing plaintext
- **DEK rotation** — weekly re-keying without bulk re-encryption
- **Cross-device private key** — RSA private key stored in IndexedDB, recoverable across devices via PBKDF2-wrapped backup

*Source code is private. Technical writing and implementation samples available on request.*

---

## Türkçe

Türkiye sağlık sektörüne yönelik tam kapsamlı klinik yönetim SaaS'ı.
Psikologlar, diyetisyenler, fizyoterapistler ve klinik yöneticileri için tasarlandı.

**Canlı:** [seanscure.com](https://seanscure.com)

### Teknoloji Yığını

| Katman | Teknolojiler |
|---|---|
| Frontend | Vue 3, TypeScript, PrimeVue, Tailwind CSS |
| Backend | .NET 8, PostgreSQL, SignalR |
| Mobil | Capacitor (Android) |
| Altyapı | Self-hosted key vault, Cloudflare |

### Öne Çıkan Teknik Özellikler

**Uçtan Uca Şifreleme (E2EE)**
Hasta verileri — ad, klinik not, TC kimlik numarası — sunucuya ulaşmadan
önce istemci tarafında şifrelenir. Backend yalnızca şifreli veri saklar,
içeriğe erişemez.

Web Crypto API ile AES-256-GCM + RSA-OAEP hibrit şifreleme kullanıldı.
Her kayıt için rastgele 256-bit DEK üretilir; bu anahtar iki bağımsız
RSA zarfına sarılır: biri kayıt sahibi için, biri self-hosted key vault
üzerinden kurtarma için.

→ [Şifreleme mimarisi](https://gist.github.com/mehmettalhaaksoy/1ebe8b6c288b5032de953640e9220b4c)
→ [vault.ts — çekirdek implementasyon](https://gist.github.com/mehmettalhaaksoy/4c299861e5d896b0be3a4a2418a89b5a)

**Rol Tabanlı İzin Sistemi**
Rol varsayılanları üzerine kişi bazlı override desteği.
Boolean, string enum ve çalışan ID dizisi olmak üzere karışık izin tipleri
JSONB olarak saklanır, sorguda birleştirilir.

**Gerçek Zamanlı Bildirimler**
Kullanıcı ve klinik bazlı grup yönlendirmesiyle SignalR hub.
Randevu hatırlatmaları, klinik davetleri, katılım istekleri anlık iletilir.

**Randevu Yönetimi**
Çakışma tespiti, haftalık programa göre slot üretimi, izin bloklama,
resmi tatil desteği, randevu bazlı süre override.

**Çok Platform**
Aynı kod tabanı web uygulaması ve Android APK olarak çalışır.
Web'de sidebar, mobilde alt sekme çubuğu — platforma göre otomatik layout.

### Mimari Kararlar

- **Wire'da plaintext yok** — E2EE servis katmanında zorunlu
- **HMAC trigram arama** — plaintext açmadan şifreli adlarda arama
- **DEK rotasyonu** — toplu yeniden şifreleme olmadan haftalık anahtar yenileme
- **Cihazlar arası private key** — IndexedDB'de saklanan RSA private key, PBKDF2 ile şifrelenmiş yedek üzerinden yeni cihazda kurtarılabilir

*Kaynak kod gizlidir. Teknik yazı ve implementasyon örnekleri talep üzerine paylaşılır.*
