# Instagram Agent Skill 

Besplatan paket od **13 Claude vještina** koji vodi tvoj Instagram račun. Bez registracije, bez API ključa, ništa se ne spaja na vanjski servis. Claude piše — ti objavljuješ.

---

## Što radi

Jedna vještina piše Reels prema 26 provjerenih "hook" formula i boduje otvor prije nego potrošiš snimku. Druga pretražuje što trenutno radi u tvojoj niši i rangira po tome koliko je svaki video nadmašio vlastiti kanal. Treća piše caption i pokazuje točno onih prvih 125 znakova koje korisnik vidi prije **"... više"**. Jedna ocjenjuje profil iz 100 bodova i prepisuje ono što je bodove izgubilo. Jedna planira tjedan.

I jedna je **humanizer** — zbog njega je sve ostalo upotrebljivo. Miče em-crtice, "slop" rječnik i nevidljive watermark znakove iz draft teksta, a onda bodovanjem kroz 5 provjera pokaže je li tekst spreman da ga vidiš.

**Ništa se ne objavljuje dok ti ne kažeš "da".** Vještine pišu. Ti objavljuješ.

---

## Instalacija

Zalijepi ovaj prompt u Claude:

```
https://github.com/pisacai/piskeai_sud

Instaliraj ovu skill, pa potvrdi da /ig-reel radi.
```

Ili ručno u Claude Code:

```bash
git clone https://github.com/pisacai/piskeai_sud.git
cp -r piskeai_sud/skills/ig-* ~/.claude/skills/
```

Ili kao plugin:

```
/plugin marketplace add pisacai/piskeai_sud
/plugin install pisacai
```

Lokalno u projekt umjesto globalno: iste foldere kopiraj u `.claude/skills/` svog repoa. Nemaš Claude Code? Zalijepi bilo koji `SKILL.md` na vrh chata i radi kao mode (gubiš 5 Python alata, ali tekstualni dio radi).

Nakon instalacije — provedi **10 minuta na `templates/voice.md`**. Kopiraj ga u `~/.claude/instagram/voice.md` i popuni, ili pošalji Claudu tri svoja reela i reci: *"napiši mi voice.md iz ovoga"*. Svaka vještina čita taj fajl. Ovdje je važniji nego na drugim platformama jer riječi moraš izgovoriti naglas.

---

## 13 slash komandi

| komanda | što radi |
| --- | --- |
| `/ig-reel` | Jedna ideja → Reel. Tri hook-a iz 26 formula, bodovana, pa scenarij, tekst na ekranu i razrađen beat sheet po sekundama. |
| `/ig-viral` | Nalazi što radi u tvojoj niši, rangira po multiplikatoru nad vlastitim medijanom računa, imenuje formulu, piše swipe file. |
| `/ig-caption` | Caption, lintan. Pokazuje točno onih 125 znakova koje feed prikaže prije "... više". |
| `/ig-carousel` | Swipe postovi. Cover koji zasluži swipe, tekst po slajdovima i 1080×1350 fajlovi. |
| `/ig-story` | Dnevni niz storyja, koji sticker radi koji posao, i DM funnel koji počinje tako da *oni* prvi pišu. |
| `/ig-profile` | Boduje profil po 12-dijelnoj rubrici iz 100, pa prepisuje po "fix-first" redoslijedu. |
| `/ig-plan` | Tjedan. Što objaviti, u kojem formatu, kada, i 10 računa s kojima treba komunicirati. |
| `/ig-human` | Humanizer. Dvije Python skripte koje stvarno rade. |
| `/ig-comment` | Komentari na tuđe postove. 9 tipova, bira se po tome što post stvarno je. Nikad "🔥🔥🔥". |
| `/ig-reply` | Thread ispod tvog posta. Sortira u ključna riječ / lead / substance / pitanje / podrška / šum, pa piše tim redoslijedom. |
| `/ig-dm` | Keyword delivery, prva poruka, collab pitch, i dva follow-upa. Dva. |
| `/ig-repurpose` | Jedan video, podcast ili newsletter → tjedan dana reelsa i karusela koji svaki stoji sam za sebe. |
| `/ig-audit` | Post-mortem na ono što si već objavio. Rangira po outlier multiplikatoru i šalje per reach, ne per views. |

---

## 5 Python alata koji stvarno rade

Bez dependencyja, bez mreže, ništa se ne uploada. Rade na tvom računalu, nad tvojim tekstom.

**Hooks:**
```bash
python3 hookscore.py hooks.txt              # rangiraj hook-ove
python3 beats.py script.txt --target 30     # tempiraj prije snimanja
```
Boduje po: SPECIFICITY, STAKES, FRONTLOAD, ADDRESS. Diskvalificira hook-ove koji počinju s "stop scrolling", pozdravom ili preambulom.

**Caption:**
```bash
python3 caption.py caption.txt --keywords "ključna riječ 1,ključna riječ 2"
```
Pokaže ti prozor od 125 znakova kao kutiju — način na koji stranac u feedu čita. Enforcea trenutnu kapu od **5 hashtagova po postu** (Instagram je rezao 18. prosinca 2025.), ne 30.

**Humanizer:**
```bash
python3 humanize.py draft.txt --report      # očisti, pokaži svaku promjenu
python3 detect.py draft.txt                 # bodovanje, 5 provjera
python3 detect.py prije.txt poslije.txt     # dokaži razliku
```
Automatski miče: nevidljive znakove (zero-width spaces, word joiners, soft hyphens, BOM, Unicode tag znakove), em-crtice → zarez, en-crtice → crtica, "pametne" navodnike → ravne, ellipsis → tri točke, i 154 "slop" fraze. Last block je Instagram-specifičan: *stop scrolling, in today's video, follow for more, tag someone who needs this, the algorithm loves, run don't walk*. Živi u `slop.json` i trebaš ga editirati pod svoj glas.

Flagga umjesto da popravi: *"nije samo X, nego Y"*, rule-of-three trijade, video preambule, emoji bullet liste, tri uzastopne riječi u capsu, zidove hashtagova, uniformna duljina rečenica. Mijenjanje oblika rečenice traži prosudbu — ne regex.

**Swipe file:**
```bash
python3 swipe.py captured.tsv --out ~/.claude/instagram/swipe.md
```
Sirov broj pregleda nije dokaz. Račun s 2.000.000 pratitelja koji napravi 400.000 pregleda imao je tihi utorak. Račun s 4.000 pratitelja koji napravi istih 400.000 pregleda — našao je nešto. Rangira po multiplikatoru nad vlastitim medijanom računa.

---

## Što je autor stvarno izmjerio

Testirano na **74 realna short-form hooka** (prve 3 sekunde auto-caption trackova, top 8 i bottom 8 shortsa po kanalu, kroz 5 kanala, views od 931 do 550.000).

- **Hvata loše hook-ove dobro:** AUC 0.83, 9/10 namjerno loše pisanih hookova palo ispod medijana.
- **Ne pogađa pobjednike:** AUC 0.56 (0.50 je bacanje novčića) za razlikovanje dobrih od loših hookova istog kreatora. Samo SPECIFICITY je stvarno razlikovala.
- **Prvotni classifier formula je bio slomljen:** regex iz `hooks.json` prepoznao je 8% stvarnih hookova. Nakon prepisivanja prema stvarno transkribiranom govoru — 49%. Dodane su 4 formule koje su se ponavljale: *Contrarian Flip, The Statistic, The Reveal, Someone Else's Result* + *The Superlative*.

Pošteno korištenje: **ubij očito slabe hook-ove prije snimanja, dalje se oslanjaj na vlastiti retention graph.** Nijedan tekstualni alat ne može reći koji od dva pristojna hook-a će putovati — to odlučuju lice, montaža, zvuk i kome Instagram pokaže.

---

