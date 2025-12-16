
Ho implementato diverse misure di sicurezza per proteggere il sito da attacchi di Broken Access Control (violazione del controllo degli accessi), uno dei principali rischi OWASP Top 10. Ho modificato controller, rotte, middleware, template Blade e navbar per garantire che gli utenti accedano solo alle risorse autorizzate.

Pagine Modificate e Misure Implementate
1. ArticleController (punti 5,6,7)
edit(): Controllo if(Auth::id() !== $article->user_id && !Auth::user()->isAdmin()) - solo autore o admin possono modificare.

update(): Stesso controllo prima dell'update per prevenire modifiche non autorizzate.

destroy(): Controllo if(Auth::id() !== $article->user_id) - solo autore può eliminare.

2. web.php Routes
Punto 1: Da /users/{id} (ID manipolabile) a /profile (solo utente autenticato).

Punto 7: Da GET delete a DELETE /articles/{article}/delete (metodo HTTP sicuro).

Punto 9: Dashboard nascosto su /dashboard/home.

Punto 11: Tutte le rotte admin protette da middleware(['admin']).

3. Navbar (Blade) - punto 3
Dashboard link visibile solo con @if(auth()->user()->isAdmin()).

Profile link usa route('profile') invece di ID manipolabile.

4. show.blade.php (Article Show) - punto 4
Bottoni Edit/Delete visibili solo con @if(auth()->user()->isAdmin() || auth()->user()->id == $article->user_id).

5. AdminMiddleware
Controllo !$request->user()->isAdmin() con redirect a articles.index per non-admin.

Risultato
Principio del privilegio minimo: ogni utente vede/sa/fà solo ciò che gli è consentito. Eliminati ID manipolabili nelle URL, implementati controlli server-side, middleware dedicati e conditional rendering lato client.


-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

I implemented several security measures to protect the site from Broken Access Control attacks (OWASP Top 10). I modified controllers, routes, middleware, Blade templates, and navbar to ensure users access only authorized resources.

Modified Files & Security Measures
1. ArticleController (points 5,6,7)
edit(): Check if(Auth::id() !== $article->user_id && !Auth::user()->isAdmin()) - only author or admin can edit.

update(): Same check before update to prevent unauthorized modifications.

destroy(): Check if(Auth::id() !== $article->user_id) - only author can delete.

2. web.php Routes
Point 1: From /users/{id} (manipulable ID) to /profile (authenticated user only).

Point 7: From GET delete to DELETE /articles/{article}/delete (secure HTTP method).

Point 9: Dashboard hidden at /dashboard/home.

Point 11: All admin routes protected by middleware(['admin']).

3. Navbar (Blade) - point 3
Dashboard link visible only with @if(auth()->user()->isAdmin()).

Profile link uses route('profile') instead of manipulable ID.

4. show.blade.php - point 4
Edit/Delete buttons visible only with @if(auth()->user()->isAdmin() || auth()->user()->id == $article->user_id).

5. AdminMiddleware
Check !$request->user()->isAdmin() with redirect for non-admins.

Result
Principle of least privilege: each user sees/does/knows only what they're allowed. Removed manipulable IDs from URLs, implemented server-side checks, dedicated middleware, and client-side conditional rendering.

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------









# VulnBlog12 - Blog Vulnerabile per Studio Sicurezza

<p align="center">
<img src="https://img.shields.io/badge/OWASP-Top%2010%202021-red" alt="OWASP Top 10 2021">
<img src="https://img.shields.io/badge/Laravel-12.x-orange" alt="Laravel 10">
<img src="https://img.shields.io/badge/Purpose-Educational-blue" alt="Educational Purpose">
</p>

## ⚠️ AVVERTENZA IMPORTANTE

**Questo progetto è intenzionalmente vulnerabile e contiene numerosi bug di sicurezza!**

Questo blog è stato creato **esclusivamente a scopo educativo** per studiare e comprendere i rischi della OWASP Top 10 2021. **NON utilizzare questo codice in produzione o in ambienti reali.**

## 🎯 Scopo del Progetto

VulnBlog12 è un'applicazione web vulnerabile basata su Laravel che serve come laboratorio per:

- **Studiare** le vulnerabilità della OWASP Top 10 2021
- **Sperimentare** tecniche di hacking e penetration testing
- **Implementare** e testare mitigazioni di sicurezza
- **Comprendere** come funzionano gli attacchi web comuni

## 🐛 Vulnerabilità Intenzionali

Questo blog contiene deliberatamente diverse vulnerabilità di sicurezza, incluse ma non limitate a:

- **Injection** (SQL, XSS, Command)
- **Broken Authentication**
- **Sensitive Data Exposure**
- **XML External Entities (XXE)**
- **Broken Access Control**
- **Security Misconfiguration**
- **Cross-Site Scripting (XSS)**
- **Insecure Deserialization**
- **Using Components with Known Vulnerabilities**
- **Insufficient Logging & Monitoring**

## 🚀 Installazione

### Prerequisiti
- PHP 8.1+
- Composer
- MySQL/PostgreSQL
- Node.js (per Vite)

### Setup
```bash
# Clona il repository
git clone <repository-url>
cd vulnBlog12

# Installa le dipendenze PHP
composer install

# Installa le dipendenze Node.js
npm install

# Copia il file di configurazione
cp .env.example .env

# Genera la chiave dell'applicazione
php artisan key:generate

# Configura il database nel file .env
# DB_CONNECTION=mysql
# DB_HOST=127.0.0.1
# DB_PORT=3306
# DB_DATABASE=vulnblog12
# DB_USERNAME=root
# DB_PASSWORD=

# Esegui le migrazioni
php artisan migrate

# Popola il database con dati di esempio
php artisan db:seed

# Avvia il server di sviluppo
php artisan serve
```

## 📚 Risorse per lo Studio

- [OWASP Top 10 2021](https://owasp.org/Top10/)
- [OWASP Testing Guide](https://owasp.org/www-project-web-security-testing-guide/)
- [Laravel Security Best Practices](https://laravel.com/docs/security)
- [OWASP Cheat Sheet Series](https://cheatsheetseries.owasp.org/)

## 🔒 Ambiente Sicuro

**IMPORTANTE**: Utilizza questo progetto solo in un ambiente isolato:

- ✅ Ambiente di sviluppo locale
- ✅ Macchine virtuali isolate
- ✅ Container Docker dedicati
- ❌ Server di produzione
- ❌ Ambienti connessi a reti reali
- ❌ Database con dati sensibili

## 📝 Licenza

Questo progetto è rilasciato sotto licenza MIT. Ricorda che è stato creato esclusivamente a scopo educativo.

## ⚖️ Disclaimer

Gli autori non si assumono alcuna responsabilità per l'uso improprio di questo software. Questo progetto è destinato esclusivamente all'educazione e alla ricerca in sicurezza informatica in ambienti controllati e autorizzati.

---

**🔍 Buon studio della sicurezza informatica!**
