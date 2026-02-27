# Predloženi zadaci nakon pregleda baze koda

## 1) Tipografske greške
**Naslov:** Ispraviti tipografske greške u korisničkim porukama i komentarima

**Problem:**
- U `SnakeGame` postoje tipfeleri u tekstu i komentaru, npr. poruka `"সর্বনিম্ন বেড"` (vjerovatno treba `"বেট"`) i komentar `"1. 1.5x is usually successful."` gdje je numeracija duplirana.

**Opseg:**
- Proći sve korisničke notifikacije i komentare u `components/SnakeGame.tsx` i uskladiti terminologiju (`bet`/`bete`/`bed`) i numeraciju.

**Kriterij prihvata:**
- Nema očitih tipfelera u `SnakeGame` korisničkim porukama i komentarima.
- Terminologija je konzistentna kroz komponentu.

---

## 2) Ispravljanje greške
**Naslov:** Očistiti `onValue` listener za perzistentnu sesiju korisnika

**Problem:**
- U `App.tsx` se unutar `useEffect` registruje dodatni `onValue` listener za `users/${savedUid}` bez čuvanja i pozivanja unsubscribe funkcije pri cleanup-u, što može dovesti do curenja listenera i duplih ažuriranja.

**Opseg:**
- Sačuvati unsubscribe funkciju za `userRef` listener.
- Pozvati cleanup za taj listener u povratnoj funkciji `useEffect`.

**Kriterij prihvata:**
- Svi `onValue` listeneri registrovani u efektu se uredno odjavljuju pri unmount-u.
- Nema duplog ažuriranja korisničkih podataka nakon višestrukog mount/unmount ciklusa.

---

## 3) Ispravka komentara / neslaganja u dokumentaciji
**Naslov:** Uskladiti README sa stvarnim konfiguracionim zahtjevima projekta

**Problem:**
- README navodi postavljanje `GEMINI_API_KEY`, dok aplikacija koristi Firebase konfiguraciju i ne referencira Gemini ključ.

**Opseg:**
- Ažurirati README sekciju za lokalno pokretanje: navesti stvarne env varijable ili eksplicitno reći da je Firebase trenutno hardkodiran.
- Po potrebi dodati napomenu o sigurnosnim implikacijama hardkodiranih ključeva.

**Kriterij prihvata:**
- README instrukcije odgovaraju realnim zavisnostima i konfiguraciji aplikacije.
- Novi developer može pokrenuti aplikaciju bez kontradiktornih uputa.

---

## 4) Poboljšanje testa
**Naslov:** Uvesti osnovne testove za poslovnu logiku kritičnih tokova

**Problem:**
- Projekt nema test skripte ni test fajlove (`package.json` nema `test` script), pa nema automatske verifikacije ključnih pravila.

**Opseg:**
- Dodati test framework (npr. Vitest + React Testing Library).
- Napisati minimalno 1-2 testa za:
  - računanje/provjeru stanja nakon `deposit`/`withdraw` toka,
  - logiku `SnakeGame` (npr. forced-loss prag i osnovni payout scenarij).

**Kriterij prihvata:**
- `npm test` (ili `npm run test`) postoji i prolazi lokalno.
- Testovi pokrivaju barem jedan bug-prone tok i jednu igru.
