# 💰 Mini-projekt: Bank Simulator

Ett övningsprojekt för att träna JavaScript-grunder genom att bygga en enkel banksimulator i terminalen.

## 🎯 Projektbeskrivning

Du ska bygga en **Bank Simulator** där användaren kan hantera bankkonton med följande funktioner:
- Skapa nya bankkonton
- Visa alla konton med saldo
- Sätta in pengar på ett konto
- Ta ut pengar från ett konto
- Överföra pengar mellan konton
- Ta bort ett konto

Detta projekt tränar samma koncept som todo-appen och recept-hanteraren, men introducerar nya utmaningar som att hantera pengar och kontrollera saldo.

---

## 📋 Installation och Setup

### Steg 1: Skapa GitHub Repository

1. Skapa ett nytt repository på GitHub med namnet `bank-simulator`
2. Följ GitHubs instruktioner för att koppla samman det med din lokala mapp

### Steg 2: Skapa projektmappen

```bash
# Skapa och navigera till mappen
mkdir bank-simulator
cd bank-simulator
```

### Steg 3: Initiera Node.js-projektet

```bash
# Skapa package.json
npm init -y
```

### Steg 4: Konfigurera ES Modules

Öppna `package.json` och lägg till denna rad:

```json
"type": "module",
```

**Resultat:**
```json
{
  "name": "bank-simulator",
  "version": "1.0.0",
  "main": "index.js",
  "type": "module",
  ...
}
```

### Steg 5: Installera readline-sync

```bash
npm install readline-sync
```

### Steg 6: Skapa .gitignore

Skapa filen `.gitignore` med följande innehåll:

```
node_modules/
```

### Steg 7: Skapa huvudfilen

```bash
# Skapa main.mjs
touch main.mjs
```

**Windows:**
```bash
type nul > main.mjs
```

---

## 🎨 Krav på Bank Simulator

### Datastruktur

Varje bankkonto ska vara ett objekt med följande egenskaper:

```javascript
{
  accountNumber: "SE12345",    // Sträng (unikt kontonummer)
  owner: "Anna Andersson",     // Sträng (kontoinnehavarens namn)
  balance: 5000,               // Nummer (saldo i SEK)
  accountType: "Sparkonto"     // Sträng (typ av konto)
}
```

### Huvudmeny (7 alternativ)

```
Välkommen till Bank Simulator!
Du har dessa val tillgängliga:
1. Skapa nytt konto
2. Visa alla konton
3. Sätta in pengar
4. Ta ut pengar
5. Överföra pengar mellan konton
6. Ta bort konto
7. Avsluta applikationen
```

### Startar-array

Börja med 4-5 konton redan skapade med olika saldo och typer (Sparkonto, Lönekonto, Investeringskonto).

---

## 🧩 Funktioner att implementera

### 1. Skapa nytt konto (`createAccount()`)

Ska fråga efter:
- Kontoinnehavarens namn
- Kontonummer (t.ex. "SE12345")
- Initial insättning (startbelopp)
- Kontotyp

**Validering:**
- Kontonummer måste vara unikt (får inte finnas redan)
- Initial insättning måste vara minst 100 SEK
- Alla fält måste vara ifyllda

### 2. Visa alla konton (`listAccounts()`)

Ska visa:
```
 - (0) SE12345 - Anna Andersson
    Kontotyp: Sparkonto
    Saldo: 5000 SEK

 - (1) SE67890 - Erik Eriksson
    Kontotyp: Lönekonto
    Saldo: 12500 SEK
```

### 3. Sätta in pengar (`deposit()`)

Ska:
1. Visa alla konton
2. Fråga vilket konto (index)
3. Fråga hur mycket som ska sättas in
4. Lägga till beloppet till saldot
5. Visa det nya saldot

**Validering:**
- Index måste vara giltigt
- Belopp måste vara positivt

### 4. Ta ut pengar (`withdraw()`)

Ska:
1. Visa alla konton
2. Fråga vilket konto (index)
3. Fråga hur mycket som ska tas ut
4. Dra av beloppet från saldot
5. Visa det nya saldot

**Validering:**
- Index måste vara giltigt
- Belopp måste vara positivt
- **VIKTIGT:** Saldot får inte bli negativt! Kontrollera att `balance >= belopp` innan uttaget

### 5. Överföra pengar (`transfer()`)

Ska:
1. Visa alla konton
2. Fråga från vilket konto (från-index)
3. Fråga till vilket konto (till-index)
4. Fråga hur mycket som ska överföras
5. Dra av från första kontot
6. Lägg till på andra kontot
7. Visa bägge nya saldon

**Validering:**
- Båda index måste vara giltiga
- Från-index och till-index får INTE vara samma
- Belopp måste vara positivt
- Från-kontot måste ha tillräckligt med pengar

### 6. Ta bort konto (`deleteAccount()`)

Ska:
1. Visa alla konton
2. Fråga vilket konto som ska tas bort
3. **Varning:** Om saldot är över 0, varna användaren och fråga om de är säkra
4. Ta bort kontot från arrayen

### 7. Avsluta applikationen

Sätt `keepRunning = false` för att avsluta while-loopen.

---

## 🎓 Kodningsutmaningar

### Enkla utmaningar
- Hur validerar du att ett kontonummer inte redan finns?
- Hur förhindrar du negativt saldo?
- Vilka funktioner behöver du?

### Medelsvåra utmaningar
- Skapa en hjälpfunktion `findAccountByNumber(accountNumber)` som hittar ett konto baserat på kontonummer istället för index
- Lägg till en funktion som visar **totalt saldo** över alla konton
- Formatera saldo med tusentalsavgränsare (5000 → 5 000 SEK)

### Avancerade utmaningar
- Spara transaktionshistorik (varje insättning/uttag/överföring)
- Lägg till ränteberäkning på sparkonton
- Sätt maxgräns för uttag per dag (t.ex. 10 000 SEK)

---

## 🧪 Testa din applikation

```bash
node main.mjs
```

### Testscenario att prova:

1. Skapa ett nytt konto med 1000 SEK
2. Sätt in 500 SEK på kontot
3. Försök ta ut 2000 SEK (ska misslyckas - inte tillräckligt saldo)
4. Ta ut 300 SEK (ska fungera)
5. Överför 400 SEK till ett annat konto
6. Visa alla konton och kontrollera att saldona stämmer
7. Försök ta bort ett konto med pengar (ska få varning)

---

## ✅ Checklista

Innan du är klar, kontrollera att din app kan:

- [ ] Visa en tydlig huvudmeny
- [ ] Skapa nya konton med validering
- [ ] Visa alla konton med index, namn och saldo
- [ ] Sätta in pengar på ett konto
- [ ] Ta ut pengar (med kontroll att saldo räcker)
- [ ] Överföra pengar mellan två konton
- [ ] Ta bort konton med varning om saldo > 0
- [ ] Validera alla inputs (giltiga index, positiva belopp)
- [ ] Hantera ogiltiga menyval
- [ ] Fortsätta köras tills användaren avslutar
- [ ] Ha separata funktioner för varje operation
- [ ] Ha tydliga kommentarer i koden

---

## 💡 Tips och tricks

### Hantera pengar

```javascript
// RÄTT sätt att kontrollera saldo innan uttag
if (accounts[index].balance >= amount) {
  accounts[index].balance -= amount;
  console.log("Uttag genomfört!");
} else {
  console.log("Otillräckligt saldo!");
  return; // Avbryt funktionen
}
```

### Kontrollera unika kontonummer

```javascript
// Loop genom alla konton och kolla om numret finns
function accountNumberExists(accountNumber) {
  for (let i = 0; i < accounts.length; i++) {
    if (accounts[i].accountNumber === accountNumber) {
      return true; // Hittade ett matchande nummer
    }
  }
  return false; // Inget matchande nummer hittades
}
```

### Formatera pengar (Medelsvår utmaning)

```javascript
function formatCurrency(amount) {
  return amount.toLocaleString('sv-SE') + ' SEK';
}

// Exempel:
console.log(formatCurrency(5000)); // "5 000 SEK"
```

---

## 🚀 Pusha till GitHub

```bash
# Initiera git (om inte redan gjort)
git init

# Lägg till alla filer
git add .

# Skapa commit
git commit -m "Lagt till bank simulator applikation"

# Koppla till GitHub repo
git remote add origin https://github.com/ditt-användarnamn/bank-simulator.git

# Pusha till GitHub
git push -u origin main
```

---

## 🎓 Vad du tränar på

- ✅ **Array-manipulation** (push, splice)
- ✅ **Objekt-hantering** (properties, värden)
- ✅ **Validering** (saldo, index, unika värden)
- ✅ **For-loopar** (söka genom arrays)
- ✅ **If-satser** (komplex logik med flera villkor)
- ✅ **Switch-satser** (menyhantering)
- ✅ **Funktioner** (parametrar, return)
- ✅ **Användarinput** (readline-sync)
- ✅ **Matematiska operationer** (+, -, jämförelser)
- ✅ **Best practices** (kodorganisation, kommentarer)

---

## 📚 Jämför med tidigare projekt

| Koncept | Todo-app | Recept-hanterare | Bank Simulator |
|---------|----------|------------------|----------------|
| **CRUD operationer** | ✅ | ✅ | ✅ |
| **Array-manipulation** | ✅ | ✅ | ✅ |
| **Validering** | Index | Index, Betyg 1-5 | Index, Saldo, Unika nummer |
| **Ny utmaning** | - | Nummer-validering | Pengar-transaktioner, Överföringar |

---

**Lycka till med projektet! 🚀**

**Om du kör fast:** Jämför med todo-appen och tänk på att varje funktion ska göra EN sak. Börja enkelt och bygg upp funktionaliteten steg för steg!