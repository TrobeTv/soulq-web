# SoulQ — web pro publikaci aplikace

Statický web (čisté HTML/CSS, žádné závislosti) se stránkami, které vyžadují Google Play a Apple App Store pro publikaci aplikace SoulQ.

## Struktura

| Stránka | CZ | EN | K čemu slouží |
|---|---|---|---|
| Landing | `index.html` | `en/index.html` | Marketing URL (App Store), domovská stránka |
| Zásady ochrany os. údajů | `privacy.html` | `en/privacy.html` | **Povinné** — Privacy Policy URL (Play i App Store) |
| Smazání účtu | `delete-account.html` | `en/delete-account.html` | **Povinné pro Play** — aplikace umožňuje registraci |
| Podmínky použití | `terms.html` | `en/terms.html` | App Store (EULA), doporučené pro Play |
| Podpora | `support.html` | `en/support.html` | **Povinné pro App Store** — Support URL |

Sdílené styly: `assets/style.css`. Brand assety podle „SoulQ Brand Identity & Experience Guidelines“ (2026):

- `assets/logo.svg` — SoulQ Symbol, *primary digital* (gradient #0A9BB0 → #047283 → #034E5A, zlatý Moment #FFC14A). Master artwork — nepřekreslovat, neotáčet, nedeformovat.
- `assets/logo-reversed.svg` — *reversed* varianta (krémový symbol #FFF7ED) pro tmavé nebo teal plochy.
- `assets/favicon.svg`, `assets/favicon-32.png`, `assets/apple-touch-icon.png` — ikona aplikace (vertikální gradient #6A3DE8 → #0F859D), stejná jako v obchodech.
- Wordmark „SoulQ.“ — Bricolage Grotesque 600, teal ink #0E2A2E, zlatá tečka (`<span class="dot">.</span>`).

Barvy: primary teal `#047283`, teal accent `#0A9BB0`, teal deep `#034E5A`, mint `#D4EBE8`, signal gold `#FFC14A`, paper `#F6FBFA`.

## Nasazení

Web musí být na **veřejné, trvalé URL** (Google nepřijímá PDF ani geograficky blokované stránky). Nejjednodušší možnosti (zdarma):

- **GitHub Pages:** repo → Settings → Pages → deploy z branche `main`. URL bude `https://<user>.github.io/soulq-web/`.
- **Netlify / Vercel / Cloudflare Pages:** přetáhnout složku nebo propojit repo.
- **Vlastní doména** (např. `soulq.cz` / `soulq.app`) — nejlepší varianta; package id je `cz.soulq.app`, doména `soulq.cz` by seděla.

## Kam URL vyplnit

### Google Play Console
1. **Store listing → Privacy policy** → URL na `privacy.html`.
2. **App content → Data safety** → vyplnit formulář **konzistentně s privacy policy**. Podle aktuálního stavu aplikace deklarovat:
   - *Collected:* e-mail, uživatelské jméno, rok narození, fotografie (avatar), „Other info" (záznamy nálad/pocitů — kategorie *Health and fitness / Other*), app interactions ne.
   - *Shared:* nic se nesdílí s třetími stranami.
   - Šifrování při přenosu: ano (TLS). Možnost požádat o smazání: ano.
3. **App content → Account deletion** → URL na `delete-account.html` (povinné, protože app má registraci).
4. **Store listing → kontaktní e-mail** musí fungovat.

### App Store Connect
1. **App Privacy** → Privacy Policy URL → `en/privacy.html` (nebo CZ).
2. **App Information → Support URL** → `support.html`; **Marketing URL** (volitelné) → `index.html`.
3. **App Privacy „nutrition labels"** — deklarovat stejná data jako v Data safety (Contact Info: email; User Content: photos, other user content; Identifiers: user ID; Health data: mood — *není* linked to advertising, *není* tracking).
4. Sign in with Apple už je implementováno (vyžadováno, protože app nabízí Google sign-in).

## Před publikací zkontrolovat / doplnit

- [x] **Právní identita správce** — Mikuláš Báča (doplněno v privacy, terms i delete-account).
- [x] **Kontaktní e-mail** — info@soulq.cz (na všech stránkách; schránka musí existovat a někdo ji musí číst).
- [x] **Region Supabase projektu** — Frankfurt (eu-central-1), uvedeno v privacy v2.0.
- [ ] **Odkazy na obchody** — na landing page jsou placeholdery „již brzy"; po publikaci nahraďte skutečnými odkazy na Play/App Store.
- [x] **Retence** — delete-account odpovídá tabulce dob uchování v privacy v2.0 (logy 90 dní, zpětná vazba 12 měsíců, evidence souhlasů 3 roky).
- [x] **Právní texty verze 2.0** (účinnost 5. 11. 2026, aktualizace 4. 11. 2026) — privacy i terms v CZ; EN verze jsou překlad s doložkou, že rozhodná je česká verze.
- [ ] Stejnou verzi 2.0 právních textů nasadit i do aplikace (`lib/data/legal_documents.dart`), aby se shodovala s webem.
- [ ] Datum účinnosti aktualizujte, pokud texty před publikací změníte.

## Lokální náhled

```bash
python3 -m http.server 8000
# otevřít http://localhost:8000
```
