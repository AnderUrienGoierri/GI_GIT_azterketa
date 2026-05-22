# Git Azterketa: Gida eta Komandoak (Euskaraz)

Gida honek Git-eko azterketa praktiko batean eskatzen diren bi kasuistika nagusiak azaltzen ditu, pauso bakoitzean erabili beharreko `gitbash` komandoekin.

---

## 1. KASUA: Irakasleak emandako GitHub errepositorio batetik hastea

_(Azterketako 3, 4, 5, 6 eta 7. ariketei dagokie)_

Irakasleak emandako proiektua deskargatu, zure adarra (branch) sortu, aldaketak egin eta azkenik beste adar batekin merge egin behar da.

### Pausoak:

**1. Errepositorioa klonatu (Deskargatu) ("hartu GitHub-etik kodea"):**
Ireki Git Bash nahi duzun karpetan eta idatzi irakaslearen URL-a:

```bash
git clone https://github.com/ander-goierri/git-azterketa-taldea
```

📸 _Atera terminalaren argazkia._

**2. Proiektuaren karpetan sartu:**

```bash
cd git-azterketa-taldea
```

**3. Zure izen-abizenekin branch (adar) berri bat sortu eta bertara mugitu:**

```bash
git checkout -b izena-abizena
```

_(Oharra: Ordezkatu "izena-abizena" zure benetako izen-abizenekin)._

**4. Branch hori GitHub-era igo (publikatu):**

```bash
git push -u origin izena-abizena
```

📸 _Atera terminalaren argazkia._

**5. Egin 1. aldaketa eta Commit-a (Adib. formularioaren width-a aldatu):**

- Ireki proiektua zure editorean (adib. VS Code), joan fitxategira eta egin aldaketa.
- Gorde fitxategia, eta Git Bash-en idatzi:

```bash
git add .
git commit -m "Formularioaren width-a aldatuta"
```

- Commit-aren ID-a (identifikadorea) lortzeko:

```bash
git log --oneline
```

📸 _Atera terminalaren argazkia (Commit ID-a ikus dadin) eta kopiatu ID hori._

**6. Egin 2. aldaketa eta Commit-a (Adib. kolorea aldatu eta adina 18 defektuz):**

- Egin aldaketa kodean eta gorde.

```bash
git add .
git commit -m "Formularioaren kolorea aldatuta eta adina 18 defektuz ezarrita"
git log --oneline
```

📸 _Atera terminalaren argazkia eta ID-a gorde._

**7. Aurreko commit bat ezabatu (Adibidez, formularioaren width-a aldatu zenuenekoa):**
Commit zehatz bat ezabatzeko modu ezberdinak daude. Seguruena `revert` erabiltzea da (aldaketa desegiten duen commit berri bat sortzen du) edo historiatik kentzea `rebase` bidez.

- **Aukera A (Historiatik ezabatzeko - Interactive Rebase):**

  ```bash
  git rebase -i HEAD~2
  ```

  _(Honek azken 2 commit-ak irekiko ditu testu-editore batean. Ezabatu nahi duzun commit-aren hasieran `pick` hitza agertuko da; aldatu ezazu `drop` edo `d` hitzagatik. Gorde eta itxi editorea)._

- **Aukera B (Aldaketa desegiteko - Revert):**
  ```bash
  git revert <ezabatu-nahi-duzun-commit-aren-IDa>
  ```

📸 _Atera terminalaren argazkia prozesuarena eta gorde ID berria/historia._

**8. Merge egitea ("mergeEgiteko" branch-arekin):**

- Lehenengo, eguneratu zure tokiko (local) datu-basea GitHub-eko informazioarekin:

```bash
git fetch origin
```

- Orain, batu "mergeEgiteko" adarra zurea dagoen lekura:

```bash
git merge origin/mergeEgiteko
```

- **Gatazkak (Conflicts) badaude:** Bi adarrek lerro berdinak aldatu badituzte, VS Code-n ireki, eta ikusiko duzu testua nabarmenduta. Bertan botoiak agertuko dira: _Accept Current Change_ (zurea mantendu), _Accept Incoming Change_ (bestearena mantendu) edo _Accept Both Changes_ (biak mantendu). Aukeratu bat (kolorea, etab.), gorde fitxategia eta ondoren:

```bash
git add .
git commit -m "Merge eginda mergeEgiteko adarrarekin gatazkak konponduz"
```

📸 _Atera terminalaren argazkia eta `git log` bidez gorde ID-a._

---

## 2. KASUA: Errepositorio bat hutsetik sortzea

_(Azterketako 1. eta 2. ariketei dagokie)_

Karpeta lokal bat sortu, Git hasieratu, adar bat sortu, HTML bat egin, Commit egin eta dena GitHub-era igo.

### Pausoak:

**1. Karpeta berri bat sortu eta bertan sartu:**

```bash
mkdir nire-azterketa
cd nire-azterketa
```

**2. Git errepositorioa hasieratu (init):**

```bash
git init
```

**3. Branch (adar) bat sortu bertan:**

```bash
git checkout -b garapena
```

**4. HTML fitxategi bat sortu:**

```bash
touch index.html
```

_(Edota ireki karpeta VS Code-n eta sortu bertatik `index.html`)._

**5. Commit-a egin:**

```bash
git add .
git commit -m "Hasierako HTML fitxategia sortuta"
git log --oneline
```

📸 _Atera terminalaren argazkia eta ID-a gorde._

**6. GitHub-era igo (Push):**

- Joan GitHub.com webgunera, egin klik "New Repository" botoian. Jarri izen bat, baina **EZ gehitu README, ez .gitignore, ez license** (hutsa egon behar da).
- GitHub-ek bi komando emango dizkizu "…or push an existing repository from the command line" atalean. Kopiatu eta itsatsi Git Bash-en:

```bash
git remote add origin https://github.com/ZURE-ERABILTZAILEA/errepositorioaren-izena.git
git push -u origin garapena
```

📸 _Atera terminalaren argazkia._

**7. `.gitignore` sortu CSS fitxategiak ez igotzeko:**

- GitBash-en (edo VS Coden) sortu bi fitxategi hauek:

```bash
touch .gitignore
touch estiloak.css
```

- Ireki `.gitignore` fitxategia eta idatzi lerro hau bertan:

```text
*.css
```

- Aldatu zeozer HTML-an eta idatzi estilotan `h1` etiketari kolorea aldatzeko. Probatu nabigatzailean.
  📸 _Atera argazkia web orrialdeari nabigatzailean._
- Egin berriro commit:

```bash
git add .
git commit -m "gitignore fitxategia gehituta css-ak ezkutatzeko"
git log --oneline
```

_(Hemen ikusiko duzu git-ek ez duela CSS fitxategia detektatu)._
📸 _Atera terminalaren argazkia eta ID-a gorde._

---

## 📝 Git Komando Erabilgarrien Taula

| Komandoa                        | Deskribapena zertarako den                                                                                                  |
| :------------------------------ | :-------------------------------------------------------------------------------------------------------------------------- |
| `git init`                      | Karpeta arrunt bat Git errepositorio bihurtzen du (hutsetik hasterakoan).                                                   |
| `git clone <url>`               | GitHub-eko (urruneko) errepositorio bat deskargatzen du (kopiatzen du) zure ordenagailura.                                  |
| `git status`                    | Zure proiektuko fitxategien egoera erakusten du (aldatuta dauden, etab.).                                                   |
| `git branch`                    | Dauden adar (branch) guztiak erakusten ditu. Zurea berdez agertuko da.                                                      |
| `git checkout -b <izena>`       | Branch berri bat sortu eta bertara mugitzen zaitu automatikoki.                                                             |
| `git checkout <izena>`          | Lehendik sortuta dagoen branch batera mugitzeko balio du.                                                                   |
| `git add .`                     | Aldatutako edo sortutako fitxategi guztiak prestatzen ditu (staging area) commit egiteko.                                   |
| `git commit -m "mezua"`         | Aldaketak "argazki" gisa gordetzen ditu modu lokalean zure historian, mezu argigarri batekin.                               |
| `git log --oneline`             | Egindako commit-en historia erakusten du era laburrean, Commit ID-ak barne.                                                 |
| `git push -u origin <branch>`   | Zure lokalean egindako aldaketak eta commit-ak GitHub-era igotzen ditu.                                                     |
| `git fetch origin`              | GitHub-en dauden adar eta aldaketa berriak ekartzen ditu, baina ez ditu fitxategiekin bateratzen.                           |
| `git merge <branch>`            | Zehaztutako branch-aren aldaketak zure uneko branch-arekin bateratzen (fusionatzen) ditu.                                   |
| `git revert <commit-id>`        | Commit zehatz baten aldaketak desegiten ditu, horretarako desegite hori gordeko duen commit berri bat sortuz (oso segurua). |
| `git rebase -i HEAD~<zenbakia>` | Commit historia berridazteko edo aldatzeko (adibidez, historian tarteko commit bat betirako ezabatzeko edo `drop` egiteko). |
| `git remote add origin <url>`   | Zure errepositorio lokal berriari GitHub-eko lotura bat gehitzen dio nora igo jakiteko.                                     |
