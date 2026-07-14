# SoulQ — web pro publikaci aplikace

Statický web (čisté HTML/CSS, žádné závislosti) se stránkami, které vyžadují Google Play a Apple App Store pro publikaci aplikace SoulQ.

## Struktura

| Stránka | CZ | EN | K čemu slouží |
|---|---|---|---|
| Landing | `index.html` | `en/index.html` | Marketing URL (App Store), domovská stránka |
| Zásady ochrany os. údajů | `privacy.html` | `en/privacy.html` | **Povinné** — Privacy Policy URL (Play i App Store) |
| Smazání účtu | `delete-account.html` | `en/delete-account.html` | **Povinné pro Play** — aplikace umožňuje registraci |
| Podmínky užití | `terms.html` | `en/terms.html` | App Store (EULA), doporučené pro Play |
| Podpora | `support.html` | `en/support.html` | **Povinné pro App Store** — Support URL |

Sdílené styly: `assets/style.css`, logo: `assets/logo.svg`. Barvy odpovídají aplikaci (`lib/theme/app_colors.dart`): teal `#047283`, krémová `#FFF7ED`, zlatá `#FFC14A`. Web podporuje světlý i tmavý režim.

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

- [ ] **Právní identita správce** — v `privacy.html` a `terms.html` je zatím jen „provozovatel aplikace SoulQ" + e-mail. Pro plný soulad s GDPR doplňte jméno/firmu (příp. IČO a adresu) do sekce „Správce osobních údajů".
- [ ] **Kontaktní e-mail** — na stránkách je `ondra.srostlik@gmail.com`. Pokud chcete doménový e-mail (např. `podpora@soulq.cz`), přepište ho na všech stránkách (`grep -rl "ondra.srostlik" .`).
- [ ] **Region Supabase projektu** — pokud je projekt hostovaný mimo EU, věta o předávání dat mimo EHP v privacy policy platí; pokud je v EU, můžete ji upřesnit („data jsou uložena v EU").
- [ ] **Odkazy na obchody** — na landing page jsou placeholdery „již brzy"; po publikaci nahraďte skutečnými odkazy na Play/App Store.
- [ ] **Retence záloh (30 dnů)** — v privacy i delete-account je uvedeno max. 30 dnů; ověřte, že odpovídá nastavení záloh v Supabase.
- [ ] Datum účinnosti (14. 7. 2026) aktualizujte, pokud texty před publikací změníte.

## Lokální náhled

```bash
python3 -m http.server 8000
# otevřít http://localhost:8000
```
