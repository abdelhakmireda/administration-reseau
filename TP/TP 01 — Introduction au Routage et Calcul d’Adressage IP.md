
---

# 🎓 Adressage IP & Calcul Réseau (Approche Professionnelle)

---

## 🎬 Introduction (prise de parole prof)

👉 *“Aujourd’hui, vous allez apprendre une compétence clé…”*

👉 *Pas juste comprendre les réseaux…*

👉 mais **les concevoir comme en entreprise** 🏢

---

# 🌐 1️⃣ Comprendre une adresse IP

---

## 🎯 Exemple

```
192.168.1.10/24
```

---

## 🧠 Explication

👉 Une IP = 32 bits (IPv4)

👉 divisée en 2 parties :

| Partie  | Rôle                 |
| ------- | -------------------- |
| Réseau  | identifier le réseau |
| Machine | identifier l’hôte    |

---

👉 Le `/24` signifie :

👉 24 bits pour réseau
👉 8 bits pour machines

---

# 📏 2️⃣ Calcul du nombre de machines

---

## 🎯 Formule

👉 Nombre de machines =

👉 **2^n - 2**

---

## 🧠 Explication prof

👉 *“Pourquoi -2 ?”*

👉 Parce que :

❌ 1 adresse réseau
❌ 1 adresse broadcast

---

## 🎯 Exemple

### 🔹 /24

👉 bits machines = 8

```
2^8 - 2 = 254 machines
```

---

### 🔹 /26

👉 bits machines = 6

```
2^6 - 2 = 62 machines
```

---

### 🔹 /30

👉 bits machines = 2

```
2^2 - 2 = 2 machines
```

👉 utilisé pour liaison routeur ↔ routeur

---

# 📡 3️⃣ Adresse réseau & broadcast

---

## 🎯 Exemple

```
192.168.1.0/24
```

---

| Type      | Adresse                     |
| --------- | --------------------------- |
| Réseau    | 192.168.1.0                 |
| Broadcast | 192.168.1.255               |
| Machines  | 192.168.1.1 → 192.168.1.254 |

---

## 🧠 Astuce prof

👉 réseau = tout à 0
👉 broadcast = tout à 1

---

# 🔪 4️⃣ Introduction au Subnetting

---

## 🎬 Situation

👉 *“Une entreprise grandit…”*

👉 1 seul réseau = problème ❌

---

## 🎯 Solution

👉 découper en sous-réseaux

---

## 🧠 Exemple

```
192.168.1.0/24
```

👉 on peut faire :

```
/25 → 2 sous-réseaux
/26 → 4 sous-réseaux
```

---

# 🏢 5️⃣ Simulation Entreprise (TRÈS IMPORTANT)

---

## 🎯 Scénario

👉 Une entreprise possède :

👉 **4 départements :**

* Informatique 💻 → 60 machines
* RH 👥 → 30 machines
* Finance 💰 → 20 machines
* Direction 🧠 → 10 machines

---

## 🧠 Question aux étudiants

👉 Comment organiser le réseau ?

👉 Est-ce qu’on donne le même réseau à tout le monde ?

❌ NON

---

# ✍️ Étape 1 — Choisir réseau global

```
192.168.1.0/24
```

👉 total : 254 machines

---

# ✍️ Étape 2 — Calcul des besoins

| Département | Machines |
| ----------- | -------- |
| IT          | 60       |
| RH          | 30       |
| Finance     | 20       |
| Direction   | 10       |

---

# ✍️ Étape 3 — Choix des masques

---

## 🔹 IT → 60 machines

👉 besoin : 62 →

👉 masque :

```
/26 (62 machines)
```

---

## 🔹 RH → 30 machines

👉 besoin : 30 →

👉 masque :

```
/27 (30 machines)
```

---

## 🔹 Finance → 20 machines

👉 besoin : 20 →

👉 masque :

```
/27
```

---

## 🔹 Direction → 10 machines

👉 besoin : 10 →

👉 masque :

```
/28 (14 machines)
```

---

# ✍️ Étape 4 — Attribution des sous-réseaux

---

## 🔹 IT

```
192.168.1.0/26
→ 192.168.1.1 → 62
```

---

## 🔹 RH

```
192.168.1.64/27
→ 192.168.1.65 → 94
```

---

## 🔹 Finance

```
192.168.1.96/27
```

---

## 🔹 Direction

```
192.168.1.128/28
```

---

# 🧠 Résultat final

👉 réseau structuré
👉 pas de gaspillage
👉 optimisé

---

# 📚 6️⃣ TD — Exercices (niveau entreprise)

---

## ✍️ Exercice 1

👉 Réseau :

```
192.168.10.0/24
```

👉 Questions :

1. Nombre de machines ?
2. Broadcast ?
3. Plage IP ?

---

## ✍️ Exercice 2

👉 Une entreprise a :

* 100 machines
* 50 machines
* 20 machines

👉 Questions :

1. Quel masque pour chaque ?
2. Proposer un plan d’adressage

---

## ✍️ Exercice 3 (important)

👉 Réseau :

```
192.168.1.0/24
```

👉 On veut :

👉 4 sous-réseaux égaux

Questions :

1. Quel masque ?
2. Combien de machines ?
3. Donner les réseaux

---

## ✍️ Exercice 4 (expert)

👉 Une entreprise possède :

* 120 machines
* 60 machines
* 30 machines
* 10 machines

👉 Réseau disponible :

```
192.168.0.0/23
```

👉 Questions :

1. Proposer un plan complet
2. Minimiser le gaspillage
3. Donner tous les sous-réseaux

---

# 🎯 Conclusion

👉 *“L’adressage IP n’est pas juste théorique…”*

👉 *C’est une compétence clé pour :*

✔ concevoir un réseau
✔ optimiser les ressources
✔ éviter les erreurs

---

