<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=soft&color=0:FCAF01,50:FE2C6B,100:FC05AC&height=160&section=header&text=AntiBot&fontSize=60&fontColor=FFFFFF&fontAlignY=42&desc=Spigot%20%2F%20Paper%20%E2%80%A2%201.8%20%E2%86%92%201.21.11&descSize=15&descAlignY=72&animation=fadeIn" alt="AntiBot" width="100%" />
</p>

<p align="center">
  <a href="https://github.com/coslant/AntiBot/releases/latest"><img src="https://img.shields.io/github/v/release/coslant/AntiBot?style=for-the-badge&label=%C4%B0ndir&color=FE2C6B&logo=github" alt="Download" /></a>
  <a href="https://discord.gg/forges"><img src="https://img.shields.io/badge/Discord-Forges%20Studio-5865F2?style=for-the-badge&logo=discord&logoColor=white" alt="Discord: Forges Studio" /></a>
</p>

<p align="center">
  <a href="https://github.com/coslant/AntiBot/actions/workflows/build.yml"><img src="https://img.shields.io/github/actions/workflow/status/coslant/AntiBot/build.yml?branch=main&style=flat-square&label=build" alt="Build" /></a>
  <img src="https://img.shields.io/badge/Minecraft-1.8%20%E2%86%92%201.21.11-FCAF01?style=flat-square" alt="Minecraft 1.8 - 1.21.11" />
  <img src="https://img.shields.io/badge/Spigot%20%7C%20Paper-FE9808?style=flat-square" alt="Spigot | Paper" />
  <img src="https://img.shields.io/badge/Java-8-FD6C29?style=flat-square&logo=openjdk&logoColor=white" alt="Java 8" />
  <a href="LICENSE"><img src="https://img.shields.io/github/license/coslant/AntiBot?style=flat-square&color=FB0C9E&label=lisans" alt="License" /></a>
</p>

<p align="center">
  <b>Bot saldırılarına karşı bağlantı limiti ve GUI doğrulama.</b>
  <br>
  <sub><kbd>EN</kbd> Multi-layer bot protection: connection rate limits, per-IP caps and a GUI captcha.</sub>
</p>

Bot saldırıları sunucuyu saniyeler içinde düşürebilir. AntiBot dört katmanlı bir savunma kurar:
saldırıyı otomatik algılar, kilit moduna geçer ve gerçek oyuncuları basit bir GUI doğrulamasıyla ayırır.
Tek jar **1.8 – 1.21.11** arası çalışır.

## ✨ Özellikler

- 🚦 **Bağlantı hızı limiti** — kısa sürede çok fazla giriş olursa otomatik **kilit moduna** geçer
- 🌐 **IP limitleri** — aynı IP'den eş zamanlı ve dakikalık giriş sınırı
- 🔤 **İsim filtresi** — `Player1234` gibi bot kalıplarını regex ile reddeder
- 🧩 **GUI doğrulama** — yeni oyuncu doğru eşyaya tıklayana kadar hareket edemez, konuşamaz, vuramaz
- 💾 Bir kez doğrulanan oyuncu kaydedilir, bir daha sorulmaz
- 🔔 Saldırı bildirimi `antibot.notify` yetkisi olanlara gider
- ⚡ Giriş kontrolleri **ana thread dışında** yapılır; saldırı anında bile sunucu donmaz
- 🧰 Hiçbir bağımlılığı yok

## 🛡️ Katmanlar

| Katman | Ne yapar |
| :-- | :-- |
| 1. Bağlantı hızı | `interval-seconds` içinde `max-joins` aşılırsa kilit modu açılır |
| 2. IP limitleri | Aynı IP'den eş zamanlı ve dakikalık giriş sayısını sınırlar |
| 3. İsim filtresi | Regex kalıplarına uyan kullanıcı adlarını reddeder |
| 4. GUI doğrulama | Oyuncu doğru eşyaya tıklayana kadar donar |

> Kilit modundayken **daha önce doğrulanmış oyuncular girmeye devam eder** — saldırı sırasında
> sunucun düzenli oyuncularına kapanmaz.

## 📥 Kurulum

1. [Releases](https://github.com/coslant/AntiBot/releases/latest) sayfasından `AntiBot.jar` dosyasını indir.
2. Sunucunun `plugins/` klasörüne at.
3. Sunucuyu yeniden başlat.
4. `plugins/AntiBot/config.yml` dosyasından limitleri sunucunun büyüklüğüne göre ayarla.

## 🎮 Komutlar

| Komut | Açıklama | Yetki |
|-------|----------|-------|
| `/antibot status` | Kilit modu ve sayaç durumunu gösterir | `antibot.admin` |
| `/antibot lock` | Kilit modunu elle açar | `antibot.admin` |
| `/antibot unlock` | Kilit modunu kapatır | `antibot.admin` |
| `/antibot reload` | Ayarları yeniden yükler | `antibot.admin` |

**Alias:** `/ab`

## 🔑 Yetkiler

| Yetki | Açıklama | Varsayılan |
|-------|----------|------------|
| `antibot.bypass` | Doğrulamadan muaf tutulur | op |
| `antibot.notify` | Saldırı bildirimlerini görür | op |
| `antibot.admin` | AntiBot yönetimi | op |

## ⚙️ Ayarlar (config.yml)

| Anahtar | Açıklama |
|---------|----------|
| `join-rate.max-joins` / `interval-seconds` | Bu süre içinde bu sayıyı aşan giriş = saldırı |
| `join-rate.lockdown-seconds` | Kilit modu kaç saniye sürer |
| `per-ip.max-online` | Aynı IP'den eş zamanlı en fazla oyuncu |
| `per-ip.max-joins-per-minute` | Aynı IP'den dakikada en fazla giriş |
| `name-filter.blocked-patterns` | Reddedilecek isim kalıpları (regex) |
| `captcha.only-first-join` | Doğrulama yalnızca ilk girişte sorulsun |
| `captcha.only-during-attack` | Doğrulama yalnızca kilit modunda sorulsun |
| `captcha.attempts` / `timeout` | Hak sayısı ve süre sınırı |
| `whitelist-ips` | Tüm kontrollerden muaf IP'ler |

> ⚠️ Sunucun bir **proxy** (BungeeCord / Velocity) arkasındaysa tüm bağlantılar proxy'nin IP'sinden
> gelir. Bu durumda `per-ip` limitlerini kapat (`0`) ya da proxy IP'sini `whitelist-ips` listesine ekle.

## 🛠️ Derleme

```bash
mvn clean package
```

Çıktı: `target/AntiBot.jar`

> 1.8 uyumluluğu için Java 8 hedefiyle derlenir. En sorunsuz derleme **JDK 8, 11 veya 17** iledir.

Her push'ta [GitHub Actions](https://github.com/coslant/AntiBot/actions/workflows/build.yml) projeyi otomatik derler; etiketlenen sürümler (`v*`) jar'ıyla birlikte [Releases](https://github.com/coslant/AntiBot/releases) sayfasında yayınlanır.

## 💬 Destek

- 🐛 Hata bildirimi ve öneriler için [Issues](https://github.com/coslant/AntiBot/issues) sekmesini kullan.
- 💬 Sorular ve destek için [Forges Studio Discord](https://discord.gg/forges) sunucusuna katıl.

## 📄 Lisans

[MIT](LICENSE) — dilediğin gibi kullan, değiştir, dağıt.

<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=rect&color=0:FCAF01,50:FE2C6B,100:FC05AC&height=4&section=footer" width="100%" alt="" />
  <br>
  <sub>🔥 <a href="https://github.com/coslant">coslant</a> tarafından geliştirildi · <a href="https://discord.gg/forges">Forges Studio</a></sub>
</p>
