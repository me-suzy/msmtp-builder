# msmtp Static Binary Builder

🚀 **Compilare automată a binarului static msmtp pentru Linux folosind GitHub Actions**

[![Build Static msmtp Binary](https://github.com/me-suzy/msmtp-builder/actions/workflows/build-msmtp.yml/badge.svg)](https://github.com/me-suzy/msmtp-builder/actions/workflows/build-msmtp.yml)

## 📋 Ce Face Acest Repository?

Acest repository folosește **GitHub Actions** pentru a compila automat un **binar static msmtp** (versiunea 1.8.25) care funcționează pe **orice distribuție Linux x86_64** fără dependențe externe.

## ✨ Caracteristici

- ✅ **Binar 100% static** - zero dependențe externe
- ✅ **Compilare automată în cloud** - nu necesită instalare locală
- ✅ **Gratuit** - GitHub Actions este gratuit pentru repository-uri publice
- ✅ **Build rapid** - ~2-3 minute
- ✅ **Funcționează pe orice Linux** - Ubuntu, Debian, CentOS, Alpine, etc.
- ✅ **SHA256 checksum inclus** - pentru verificare

## 🚀 Cum Folosești?

### Metoda 1: Fork & Build (Recomandat)

1. **Fork acest repository** (click pe butonul "Fork" sus-dreapta)
2. În fork-ul tău, mergi la tab-ul **"Actions"**
3. Click pe **"Build Static msmtp Binary"**
4. Click pe **"Run workflow"** (buton albastru dreapta) → **"Run workflow"**
5. Așteaptă ~2-3 minute până workflow-ul se termină (✅ verde)
6. Click pe workflow-ul finalizat
7. Scroll jos la secțiunea **"Artifacts"**
8. **Download "msmtp-linux-static"** (se descarcă ca ZIP)
9. Extrage ZIP-ul și obții binarul gata de folosit!

### Metoda 2: Download Direct

Dacă sunt disponibile release-uri, poți descărca binarul direct din secțiunea [Releases](https://github.com/me-suzy/msmtp-builder/releases).

## 🔧 Verificare Binar pe Linux

După ce descarci binarul:

```bash
# Setează permisiuni de execuție
chmod +x msmtp-linux-static

# Verifică tipul fișierului
file msmtp-linux-static
# Output: ELF 64-bit LSB executable, x86-64, statically linked

# Verifică că este static (fără dependențe dinamice)
ldd msmtp-linux-static
# Output: not a dynamic executable

# Testează versiunea
./msmtp-linux-static --version
# Output: msmtp version 1.8.25

# Verifică SHA256 (opțional)
sha256sum msmtp-linux-static
# Compară cu fișierul .sha256 inclus
```

## 📦 Ce Conține Workflow-ul?

Workflow-ul GitHub Actions (`build-msmtp.yml`):

1. Pornește un Ubuntu runner în cloud
2. Instalează dependențele de build (GnuTLS, GSASL, IDN2)
3. Descarcă sursa msmtp 1.8.25 de la https://marlam.de/msmtp/
4. Compilează static cu flag-uri `-static`
5. Strip symbols pentru dimensiune mai mică
6. Verifică că binarul e static și funcțional
7. Creează SHA256 checksum
8. Upload ca artifact (păstrat 90 zile)

## 🔄 Rebuild Manual

Poți reface build-ul oricând:

1. Mergi la **Actions** → **Build Static msmtp Binary**
2. Click **Run workflow** → **Run workflow**
3. Descarcă noul binar din Artifacts după finalizare

## 📝 Configurare msmtp

După ce ai binarul, creează fișierul `~/.msmtprc`:

```bash
# Setări implicite
defaults
auth           on
tls            on
tls_trust_file /etc/ssl/certs/ca-certificates.crt
logfile        ~/.msmtp.log

# Cont Gmail (exemplu)
account        gmail
host           smtp.gmail.com
port           587
from           your-email@gmail.com
user           your-email@gmail.com
password       YOUR_APP_PASSWORD_HERE

# Cont implicit
account default : gmail
```

Setează permisiuni:
```bash
chmod 600 ~/.msmtprc
```

⚠️ **Pentru Gmail**: Folosește un [App Password](https://myaccount.google.com/apppasswords), nu parola ta normală!

## 🧪 Test Trimitere Email

```bash
echo "Test email body" | ./msmtp-linux-static -a gmail recipient@example.com
```

## 🛠️ Personalizare Build

Dacă vrei să modifici configurația build-ului:

1. Editează `.github/workflows/build-msmtp.yml`
2. Modifică flag-urile `CFLAGS` și `LDFLAGS` sau opțiunile `./configure`
3. Commit changes
4. Workflow-ul va rula automat cu noile setări

## 📊 Informații Build

- **Versiune msmtp**: 1.8.25
- **TLS Support**: GnuTLS
- **SASL Support**: GNU SASL
- **IDN Support**: libidn2
- **Tip**: Static binary (musl libc)
- **Platformă**: Linux x86_64
- **Dimensiune**: ~350-500 KB

## ❓ Întrebări Frecvente

**Q: De ce binarul e atât de mare?**  
A: Binarul static include toate bibliotecile necesare (GnuTLS, GSASL, etc.). Alternativ, poti folosi binare dinamice mai mici dar care necesită biblioteci instalate pe sistem.

**Q: Funcționează pe ARM/aarch64?**  
A: Nu, acest build e doar pentru x86_64. Pentru ARM, modifică workflow-ul să folosească un runner ARM.

**Q: Pot compila o altă versiune msmtp?**  
A: Da! Editează workflow-ul și schimbă versiunea în URL-ul de download.

**Q: Cât timp sunt păstrate artifacts?**  
A: 90 de zile. Pentru păstrare permanentă, creează un Release.

## 📚 Resurse

- [msmtp Official Site](https://marlam.de/msmtp/)
- [msmtp Documentation](https://marlam.de/msmtp/msmtp.html)
- [GitHub Actions Documentation](https://docs.github.com/actions)

## 📄 Licență

Acest repository conține doar fișierele de build automation. msmtp în sine este distribuit sub licența GPL v3. Vezi [msmtp license](https://marlam.de/msmtp/).

## 🤝 Contribuții

Contribuțiile sunt binevenite! Dacă întâmpini probleme sau ai sugestii:

1. Deschide un [Issue](https://github.com/me-suzy/msmtp-builder/issues)
2. Sau trimite un Pull Request

## ⭐ Support

Dacă acest repository ți-a fost util, lasă un ⭐ star! 

---

**Made with ❤️ using GitHub Actions**
