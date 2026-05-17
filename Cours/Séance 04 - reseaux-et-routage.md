# 🎓 Séance 04 — Le Routage Réseau (Version simplifiée et pédagogique)

# 🎬 Introduction

Dans les séances précédentes, nous avons appris :

✔ ce qu’est une adresse IP
✔ comment les machines communiquent
✔ le rôle du MAC
✔ les sous-réseaux
✔ ARP, DNS, DHCP et NAT

Mais maintenant une question très importante :

👉 *Comment un ordinateur peut parler avec un autre réseau ?*

Par exemple :

* votre PC à la maison 🏠
* un serveur Google 🌍
* un site web
* une autre entreprise

💡 Parce qu’ils ne sont pas dans le même réseau.

Alors :

👉 Qui transporte les données ?
👉 Qui choisit le chemin ?
👉 Comment Internet fonctionne réellement ?

🎯 Réponse :

# 👉 Grâce au ROUTAGE

---

# 🧠 1️⃣ Qu’est-ce que le routage ?

## 🎯 Définition simple

Le routage signifie :

👉 trouver le chemin pour envoyer les données vers la bonne destination.

---

# 📦 Exemple simple

Imaginez :

👉 vous voulez envoyer un colis 📦 à quelqu’un dans une autre ville.

Vous donnez le colis :

👉 au transporteur 🚚

Puis :

* dépôt
* autoroute
* centre de tri
* autre ville
* livraison finale

💡 En réseau :

👉 le routeur joue le rôle du transporteur.

---

# 🌐 Exemple réseau

PC1 :

```bash
192.168.1.10
```

veut joindre :

```bash
192.168.2.10
```

❌ Ce n’est pas le même réseau.

Alors :

👉 le PC envoie les données au routeur.

---

# 🧠 2️⃣ Le routeur

## 🎯 Définition

Le routeur est un équipement qui :

✔ relie plusieurs réseaux
✔ choisit le chemin des paquets
✔ permet l’accès Internet

---

# 📡 Analogie très simple

👉 Switch = distributeur dans une salle

👉 Routeur = GPS entre plusieurs villes 🚗

---

# 🌍 Exemple réel

Chez vous :

* téléphone 📱
* TV 📺
* PC 💻

Tous utilisent :

👉 votre box Internet

💡 Cette box est un routeur.

---

# 🧠 3️⃣ Gateway (Passerelle)

## 🎯 Définition simple

La gateway est :

👉 la porte de sortie du réseau.

---

# 📦 Exemple

Votre PC :

```bash
192.168.1.10
```

Gateway :

```bash
192.168.1.1
```

Quand votre PC veut parler avec :

```bash
8.8.8.8
```

👉 il envoie au routeur.

---

# 🔥 Important

Sans gateway :

❌ impossible de sortir du réseau local.

---

# 🧠 4️⃣ Comment le PC sait si la destination est locale ?

## 🎯 Le masque réseau

Le PC regarde :

* son IP
* le masque
* l’IP destination

---

# 📌 Exemple

PC :

```bash
192.168.1.10/24
```

Destination :

```bash
192.168.1.20
```

👉 même réseau ✔

Donc :

👉 communication directe.

---

# 📌 Autre exemple

Destination :

```bash
192.168.2.10
```

❌ réseau différent

Donc :

👉 envoyer au routeur.

---

# 🧠 5️⃣ Table de routage

## 🎯 Définition simple

Chaque machine possède :

👉 une liste de chemins réseau.

Cette liste s’appelle :

# 👉 table de routage

---

# 🔍 Voir la table sous Linux

```bash
ip route
```

---

# 📌 Exemple réel

```bash
192.168.1.0/24 dev eth0
default via 192.168.1.1
```

---

# 🧠 Explication facile

## Ligne 1

```bash
192.168.1.0/24 dev eth0
```

👉 “ce réseau est directement connecté”

---

## Ligne 2

```bash
default via 192.168.1.1
```

👉 “si je ne connais pas le chemin → envoyer au routeur”

---

# 🌐 6️⃣ Communication entre deux réseaux

## 🎬 Situation

PC1 :

```bash
192.168.1.10
```

PC2 :

```bash
192.168.2.10
```

---

# 📡 Étapes simples

## 1️⃣ PC1 détecte :

👉 destination différente.

## 2️⃣ Il envoie au routeur.

## 3️⃣ Le routeur regarde la destination.

## 4️⃣ Le routeur transmet vers le bon réseau.

## 5️⃣ PC2 reçoit les données.

---

# 🧠 Résumé simple

👉 Même réseau :

✔ communication directe

👉 Réseau différent :

✔ passage obligatoire par routeur

---

# 🔥 7️⃣ IP Forwarding

## 🎯 Définition

Le routeur Linux doit autoriser :

👉 le transfert des paquets.

---

# 📌 Activation

```bash
sysctl -w net.ipv4.ip_forward=1
```

---

# ⚠️ Important

Si ip_forward=0 :

👉 le routeur reçoit les paquets
❌ MAIS ne les transmet pas.

---

# 🧠 8️⃣ Route statique

## 🎯 Définition simple

Une route statique est :

👉 une route ajoutée manuellement.

---

# 📌 Exemple

```bash
ip route add 192.168.2.0/24 via 10.0.0.2
```

👉 signifie :

“pour atteindre ce réseau → utiliser ce routeur”

---

# 🌍 9️⃣ Routage Internet

## 🎯 Internet fonctionne comment ?

Internet est :

👉 un immense réseau de routeurs.

Chaque routeur :

✔ reçoit les données
✔ regarde l’adresse destination
✔ choisit le meilleur chemin

---

# 📦 Exemple réel

Votre PC → Google

Le paquet traverse :

1️⃣ box maison
2️⃣ fournisseur Internet
3️⃣ routeurs nationaux
4️⃣ routeurs internationaux
5️⃣ serveurs Google

---

# 🧠 🔟 Diagnostic réseau

# 🔍 Voir les interfaces

```bash
ip a
```

---

# 🔍 Voir les routes

```bash
ip route
```

---

# 🔍 Tester réseau

```bash
ping 8.8.8.8
```

---

# 🔍 Voir le chemin des paquets

```bash
traceroute google.com
```

---

# 🧠 1️⃣1️⃣ Switch vs Routeur

| Switch             | Routeur           |
| ------------------ | ----------------- |
| travaille avec MAC | travaille avec IP |
| même réseau        | plusieurs réseaux |
| couche 2           | couche 3          |
| local              | inter-réseaux     |

---

# 🌐 1️⃣2️⃣ Communication complète (vision globale)

## 🎬 Exemple

PC → google.com

---

# 🧩 Étapes

## 1️⃣ DNS

Trouver IP de Google.

---

## 2️⃣ Vérification réseau

Le PC voit :

👉 destination externe.

---

## 3️⃣ Envoi au routeur

Grâce à la gateway.

---

## 4️⃣ Routeurs Internet

Les paquets traversent Internet.

---

## 5️⃣ Réponse

Google répond au PC.

---

# 📌 Résumé global

| Élément        | Rôle             |
| -------------- | ---------------- |
| IP             | identifier       |
| MAC            | livraison locale |
| Gateway        | sortie réseau    |
| Routeur        | choisir chemin   |
| Table routage  | décisions        |
| IP Forwarding  | transférer       |
| Route statique | chemin manuel    |

---

# 🎯 Conclusion

👉 “Le routage est ce qui permet à Internet d’exister.”

Sans routage :

❌ pas de communication entre réseaux
❌ pas d’Internet
❌ pas de cloud
❌ pas de Google

💡 Les routeurs sont les “guides” des paquets réseau.

---

# ❓ Questions pédagogiques

1️⃣ Pourquoi a-t-on besoin d’une gateway ?
2️⃣ Quelle différence entre switch et routeur ?
3️⃣ Pourquoi le routage est-il essentiel ?
4️⃣ Que se passe-t-il si ip_forward=0 ?
5️⃣ Pourquoi un PC consulte sa table de routage ?
