# SR Leova AI — Rezumat proiect

## Scop

Platformă AI internă pentru **Spitalul Raional Leova**: un singur punct de intrare (`ai.srleova.md`) de unde fiecare departament accesează un asistent AI dedicat, fără contact cu infrastructura de stocare.

---

## 1. Interfața utilizatorului — `ai.srleova.md`

**Landing page** minimalistă, găzduită pe serverul instituției (nu redirecționare oarbă).

| Element | Detalii |
|--------|---------|
| **Branding** | Logo SR Leova (placeholder), culori alb / albastru |
| **Navigare** | 4 butoane mari, câte unul per departament |

| Buton | Departament |
|-------|-------------|
| 🔵 Acces AI Medici | Medici |
| 🟢 Acces AI Contabilitate | Contabilitate |
| 🟡 Acces AI Resurse Umane | Resurse Umane |
| 🟣 Acces AI Administrație | Administrație |

**Experiența utilizatorului:** intră pe site → click pe buton → pune întrebarea în chat.

---

## 2. Flux tehnic (la click)

Fiecare buton deschide un **link securizat de partajare NotebookLM**, cu permisiuni stricte.

**Exemplu — Medici:**

1. Click pe **[ Acces AI Medici ]**
2. Browserul deschide NotebookLM (caiet dedicat medici)
3. Sesiunea folosește contul departamentului (ex. `medici.srleova@gmail.com`, plan gratuit)
4. Rol utilizator final: **Viewer** — doar chat + note de subsol; butonul +/- pentru fișiere este ascuns sau blocat

**Izolare:** fiecare departament are caiet și cont proprii; utilizatorii nu încarcă și nu șterg documente.

---

## 3. Panou de control — management date

| Aspect | Implementare |
|--------|--------------|
| **Stocare** | Google Drive pe cont central (abonament Pro ~$19.99/lună) |
| **Organizare** | 4 foldere separate (ex. `Drive_Medici`, `Drive_Contabilitate`, etc.) |
| **Actualizare** | Protocol nou → pus în folderul Drive → Sync/Refresh în NotebookLM (cont central) |
| **Efect** | Documentele apar imediat în chat-ul departamentului, fără acțiune din partea utilizatorilor |

**Responsabilitate:** doar administratorii IT / medicali centrali gestionează conținutul.

---

## 4. Avantaje

| Avantaj | Explicație |
|---------|------------|
| **Risc de eroare umană ≈ 0** | Utilizatorii finali nu ating Drive, NotebookLM admin sau încărcări |
| **Simplitate** | 3 pași: site → buton → întrebare |
| **Securitate** | Permisiuni Viewer, linkuri controlate, date centralizate |
| **Cost** | Un cont Pro central + conturi gratuite per departament |
| **Mentenanță** | Actualizare documente dintr-un singur loc (Drive + sync) |

---

## 5. Componente (stack simplificat)

```
┌─────────────────────────────────────────────────────────┐
│  ai.srleova.md (Landing Page — server SR Leova)         │
│  [Medici] [Contabilitate] [RH] [Administrație]          │
└────────────┬────────────┬────────────┬──────────────────┘
             │            │            │
             ▼            ▼            ▼
┌─────────────────────────────────────────────────────────┐
│  NotebookLM — 4 caiete (share links, rol Viewer)       │
│  conturi dept. gratuite + cont central Pro               │
└────────────────────────────┬────────────────────────────┘
                             │ sync
                             ▼
┌─────────────────────────────────────────────────────────┐
│  Google Drive — 4 foldere (cont central Pro)           │
│  Drive_Medici | Drive_Contabilitate | Drive_RH | ...   │
└─────────────────────────────────────────────────────────┘
```

---

## 6. Pași următori (propunere)

1. Înregistrare domeniu / subdomeniu `ai.srleova.md` și hosting landing page
2. Cont Google central Pro + 4 conturi departament (sau structură echivalentă)
3. Creare foldere Drive + caiete NotebookLM + linkuri share cu Viewer
4. Design landing page (logo SR Leova definitiv, 4 butoane, HTTPS)
5. Pilot cu un departament (ex. Medici), apoi extindere
6. Procedură internă: cine actualizează protocoalele și cum se face sync-ul

---

## 7. Conturi / resurse (din propunere)

| Resursă | Rol |
|---------|-----|
| Cont central Pro | Drive + administrare NotebookLM |
| `medici.srleova@gmail.com` (ex.) | Caiet AI Medici |
| Conturi similare | Contabilitate, RH, Administrație |
| Server instituție | Găzduire `ai.srleova.md` |
