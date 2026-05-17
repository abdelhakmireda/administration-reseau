
---

# 🎓 Séance 03 — Adressage Réseau, MAC, Sous-réseaux & Protocoles essentiels

---

## 🎬 Introduction

Dans la séance précédente, nous avons vu :

👉 comment les machines communiquent
👉 comment les données circulent (paquets 📦)
👉 et les modèles OSI / TCP-IP

Mais aujourd’hui, une question très importante :

👉 **Comment une machine est-elle identifiée dans un réseau ?**
👉 **Et comment les données trouvent exactement leur destination ?**

💡 Parce que dans un réseau :

👉 il peut y avoir des dizaines… des centaines… voire des millions de machines 🌍

Alors :

👉 **Comment éviter le chaos ?**

---

# 🧠 1️⃣ Adresse IP et Adresse MAC

---

## 🌐 🔹 Adresse IP (logique)

👉 *“Imaginez que vous voulez envoyer un courrier à quelqu’un…”*

👉 Vous avez besoin de :

👉 **son adresse postale**

➡️ En réseau, cette adresse s’appelle :

👉 **Adresse IP**

---

📌 Exemple :

```
192.168.1.10
```

👉 Question aux étudiants :

❓ Est-ce que deux machines peuvent avoir la même IP ?

👉 Réponse :

❌ NON (sinon conflit réseau)

---

## 🔌 🔹 Adresse MAC (physique)

👉 Maintenant, imaginez :

👉 même si vous avez l’adresse d’une personne…
👉 il faut encore savoir **à qui remettre le courrier physiquement**

💡 Ici intervient :

👉 **l’adresse MAC**

---

📌 Exemple :

```
00:1A:2B:3C:4D:5E
```

👉 Elle est :

✔ unique
✔ liée à la carte réseau
✔ utilisée dans le réseau local

---

## 🎯 Explication simple

👉 IP = adresse de la maison 🏠
👉 MAC = identité de la personne 👤

---

## ⚠️ Très important

👉 Communication réelle :

👉 IP → pour trouver le réseau
👉 MAC → pour livrer localement

---

# 🌐 2️⃣ Types d’adresses IP

---

## 🔹 IP privée

👉 *“Quand vous êtes chez vous…”*

👉 votre réseau est interne :

```
192.168.x.x
10.x.x.x
172.16.x.x
```

👉 Ces IP :

✔ ne sortent pas sur Internet
✔ utilisées dans LAN

---

## 🔹 IP publique

👉 *“Quand vous allez sur Internet…”*

👉 vous êtes vu avec :

👉 une IP publique 🌍

---

## 🎯 Exemple concret

👉 Votre PC :

```
192.168.1.10
```

👉 Internet voit :

```
102.x.x.x
```

👉 Question :

❓ Pourquoi on n’utilise pas directement les IP privées sur Internet ?

👉 Réponse :

👉 Parce qu’elles ne sont pas uniques globalement

---

# 🔄 3️⃣ NAT (Network Address Translation)

---

## 🎯 Définition

👉 Le NAT permet :

👉 de transformer IP privée → IP publique

---

## 🧠 Explication prof

👉 *“Dans une maison, vous avez plusieurs appareils…”*

* téléphone 📱
* PC 💻
* TV 📺

👉 Mais sur Internet :

👉 **vous avez UNE seule IP**

---

## 🎯 Exemple

| Machine interne | IP publique |
| --------------- | ----------- |
| 192.168.1.10    | 102.x.x.x   |
| 192.168.1.20    | 102.x.x.x   |

---

👉 Question :

❓ Comment le routeur sait à qui renvoyer la réponse ?

👉 Réponse :

👉 Il garde une table NAT 📋

---

# 🌍 4️⃣ Sous-réseaux (Subnetting)

---

## 🎬 Introduction

👉 *“Imaginez une grande entreprise…”*

👉 Est-ce qu’on met tous les employés dans un seul réseau ?

❌ Non

👉 On organise :

* service RH
* service IT
* service finance

---

## 🎯 Définition

👉 Sous-réseau = division d’un réseau

---

## 📌 Exemple

```
192.168.1.0/24
```

👉 contient :

👉 254 machines

---

## 🔪 Découpage

👉 On peut faire :

```
192.168.1.0/25
192.168.1.128/25
```

---

## 💡 Pourquoi ?

✔ sécurité 🔐
✔ performance ⚡
✔ organisation 🧠

---

👉 Question :

❓ Est-ce que deux machines de sous-réseaux différents peuvent communiquer ?

👉 Réponse :

👉 Oui, mais via un routeur

---

# 🔗 5️⃣ ARP (Address Resolution Protocol)

---

## 🎬 Situation réelle

👉 Machine A veut envoyer à :

```
192.168.1.20
```

👉 Elle connaît l’IP…

👉 MAIS PAS le MAC ❌

---

## 🎯 Rôle ARP

👉 Trouver MAC à partir IP

---

## 📡 Processus

👉 Machine envoie :

👉 “Qui a 192.168.1.20 ?”

👉 Réponse :

👉 “C’est moi → voici mon MAC”

---

## 🧠 Important

👉 ARP fonctionne uniquement en réseau local

---

# 🌐 6️⃣ DNS

---

## 🎬 Question prof

👉 *“Vous tapez google.com…”*

👉 Est-ce que le réseau comprend ce nom ?

❌ NON

---

## 🎯 Rôle DNS

👉 Traduire :

```
google.com → 8.8.8.8
```

---

## ⚠️ Cas réel

👉 DNS HS :

❌ internet marche pas par nom
✅ IP fonctionne

---

👉 (comme ton problème Docker 😄)

---

# ⚙️ 7️⃣ DHCP

---

## 🎬 Question

👉 *“Quand vous connectez au WiFi…”*

👉 Est-ce que vous configurez l’IP manuellement ?

❌ NON

---

## 🎯 Rôle DHCP

👉 Donne automatiquement :

✔ IP
✔ masque
✔ gateway
✔ DNS

---

## 🧠 Exemple

👉 PC connecté :

👉 reçoit automatiquement :

```
192.168.1.50
```

---

# 🔀 8️⃣ Communication complète

---

## 🎯 Exemple réel

👉 PC → google.com

---

## 🧩 Étapes

1️⃣ DNS → obtenir IP
2️⃣ ARP → obtenir MAC
3️⃣ envoi au routeur
4️⃣ NAT → traduction
5️⃣ routage Internet

---

👉 *“Vous voyez ? Ce n’est pas juste envoyer un message…”*

👉 c’est toute une chaîne intelligente 🔗

---

# 🌐 9️⃣ Rôle du routeur

---

## 🎯 Fonction

👉 décider où envoyer les paquets

---

## 🧠 Explication

👉 Il regarde :

👉 adresse destination

👉 choisit le meilleur chemin

---

## 📦 Analogie

👉 routeur = GPS 🚗

---

# 🧠 🔟 Vision globale

---

👉 Un réseau fonctionne grâce à :

✔ IP → identifier
✔ MAC → localiser
✔ ARP → connecter
✔ DNS → traduire
✔ DHCP → configurer
✔ NAT → sortir Internet
✔ routeur → diriger

---

# 📌 Résumé

👉 IP = identité logique
👉 MAC = identité physique
👉 ARP = lien IP/MAC
👉 DNS = nom → IP
👉 DHCP = automatique
👉 NAT = privé → public
👉 routeur = intelligence du réseau

---

# 🎯 Conclusion

👉 *“Un réseau, ce n’est pas juste des machines connectées…”*

👉 *C’est un système organisé où chaque élément a un rôle précis.”*

---

# ❓ Questions de réflexion

* Pourquoi a-t-on besoin de MAC et IP ?
* Quel est le rôle du NAT ?
* Pourquoi DHCP est essentiel ?
* Que se passe-t-il si DNS ne fonctionne pas ?

---

