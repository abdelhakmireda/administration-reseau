# 🎓 Séance 05 — Les Trames Réseau, Encapsulation et Lecture des Communications

---

# 🎯 Objectifs de la séance

À la fin de cette séance, l’étudiant doit être capable de :

✔ comprendre ce qu’est une trame réseau
✔ comprendre l’encapsulation
✔ comprendre le rôle des couches TCP/IP et OSI
✔ identifier les champs importants d’une trame
✔ distinguer Ethernet / IP / TCP / UDP
✔ interpréter une trame réseau
✔ lire une capture Wireshark simple
✔ analyser une communication réseau réelle

---

# 🎬 Introduction

Dans les séances précédentes, nous avons appris :

✔ les adresses IP
✔ les adresses MAC
✔ le routage
✔ DNS / DHCP / NAT
✔ la communication entre réseaux

Mais maintenant une question très importante :

👉 Quand une machine envoie des données, que transporte réellement le réseau ?

Lorsque vous ouvrez un site web 🌐 :

* que contient réellement le message ?
* comment les équipements comprennent les données ?
* comment le réseau trouve la destination ?
* comment les routeurs prennent leurs décisions ?

💡 Pour comprendre cela, il faut comprendre :

# 📦 Les trames réseau

---

# 🌐 1️⃣ Qu’est-ce qu’une trame réseau ?

# 🎯 Définition

Une trame (Frame) est :

👉 une structure de données utilisée pour transporter les informations dans le réseau local.

Une trame contient :

✔ les données utilisateur
✔ les adresses MAC
✔ les adresses IP
✔ les informations de contrôle
✔ les informations de vérification

---

# 🧠 Idée importante

Quand un utilisateur envoie un message :

```text id="c1"
Bonjour
```

Le réseau n’envoie PAS simplement ce texte.

Les données sont progressivement transformées.

---

# 📦 Transformation des données

```text id="c2"
Message
↓
Segment TCP
↓
Paquet IP
↓
Trame Ethernet
↓
Bits électriques / WiFi
```

---

# 🎯 Définitions importantes

| Élément    | Niveau      |
| ---------- | ----------- |
| Données    | Application |
| Segment    | TCP         |
| Datagramme | UDP         |
| Paquet     | IP          |
| Trame      | Ethernet    |
| Bits       | Physique    |

---

# 🔄 2️⃣ L’encapsulation

# 🎯 Définition

L’encapsulation est le processus où chaque couche ajoute ses propres informations.

---

# 📦 Exemple simple

Message original :

```text id="c3"
Bonjour
```

---

# 📌 Étape 1 — TCP ajoute son en-tête

```text id="c4"
[TCP Header][Bonjour]
```

---

# 📌 Étape 2 — IP ajoute son en-tête

```text id="c5"
[IP Header][TCP Header][Bonjour]
```

---

# 📌 Étape 3 — Ethernet ajoute son en-tête

```text id="c6"
[ETH Header][IP Header][TCP Header][Bonjour][FCS]
```

---

# 🧠 Important

Chaque couche ajoute :

✔ ses informations
✔ ses règles
✔ son adressage

---

# 🌐 3️⃣ Modèle OSI et TCP/IP

# 📚 Modèle OSI

| Couche | Nom          | Fonction        |
| ------ | ------------ | --------------- |
| 7      | Application  | logiciels       |
| 6      | Présentation | format données  |
| 5      | Session      | gestion session |
| 4      | Transport    | TCP/UDP         |
| 3      | Réseau       | IP/routage      |
| 2      | Liaison      | Ethernet/MAC    |
| 1      | Physique     | câble/WiFi      |

---

# 🌐 Modèle TCP/IP

| TCP/IP       | Correspondance OSI |
| ------------ | ------------------ |
| Application  | 7-6-5              |
| Transport    | 4                  |
| Internet     | 3                  |
| Accès réseau | 2-1                |

---

# 🧠 Idée importante

👉 OSI = modèle pédagogique

👉 TCP/IP = modèle utilisé réellement sur Internet

---

# 🔄 4️⃣ Voyage complet d’une donnée

# 🎬 Situation réelle

Un PC :

```text id="c7"
192.168.1.10
```

veut accéder à :

```text id="c8"
google.com
```

---

# 🧩 Étape 1 — DNS

Le PC cherche l’adresse IP :

```text id="c9"
google.com → 142.250.180.14
```

---

# 🧩 Étape 2 — TCP

TCP ajoute :

| Champ            | Exemple |
| ---------------- | ------- |
| Port source      | 51515   |
| Port destination | 443     |
| Flags            | SYN     |
| Sequence Number  | 100     |

---

# 🎯 Rôle des ports

Les ports identifient les applications.

---

# 📌 Exemples de ports

| Port | Service |
| ---- | ------- |
| 80   | HTTP    |
| 443  | HTTPS   |
| 53   | DNS     |
| 22   | SSH     |

---

# 🧩 Étape 3 — IP

IP ajoute :

| Champ          | Exemple        |
| -------------- | -------------- |
| IP source      | 192.168.1.10   |
| IP destination | 142.250.180.14 |
| TTL            | 64             |
| Protocol       | TCP            |

---

# 🔥 Le TTL

TTL = Time To Live

👉 limite le nombre de routeurs traversés.

---

# 📌 Exemple

```text id="c10"
TTL = 64
```

Chaque routeur :

```text id="c11"
TTL - 1
```

---

# ⚠️ Pourquoi TTL est important ?

Sans TTL :

❌ boucle infinie possible sur Internet

---

# 🧩 Étape 4 — Ethernet

Ethernet ajoute :

| Champ           | Exemple           |
| --------------- | ----------------- |
| MAC source      | 00:11:22:33:44:55 |
| MAC destination | AA:BB:CC:DD:EE:FF |
| Type            | IPv4              |

---

# 📦 Structure d’une trame Ethernet

```text id="c12"
| MAC Dest | MAC Src | Type | Data | FCS |
```

---

# 🧠 MAC vs IP

| Élément | Fonction         |
| ------- | ---------------- |
| MAC     | livraison locale |
| IP      | routage Internet |

---

# 🌍 Très important

👉 IP reste généralement identique.

👉 MAIS MAC change à chaque réseau local.

---

# 🧩 Étape 5 — Physique

Les données deviennent :

✔ signaux électriques
✔ lumière fibre
✔ ondes WiFi

---

# 📦 5️⃣ Exemple COMPLET d’une trame

# 🎯 Trame réseau simplifiée

```text id="c13"
Ethernet Header
--------------------------------
Dst MAC : AA:AA:AA:AA:AA:AA
Src MAC : BB:BB:BB:BB:BB:BB
Type : IPv4

IP Header
--------------------------------
Src IP : 192.168.1.10
Dst IP : 142.250.180.14
TTL : 64
Protocol : TCP

TCP Header
--------------------------------
Src Port : 51515
Dst Port : 443
Flags : SYN

Data
--------------------------------
GET / HTTP/1.1
```

---

# 🔍 6️⃣ Comment lire une trame ?

---

# 🧠 Étape 1 — Lire Ethernet

```text id="c14"
Dst MAC : AA:AA:AA:AA:AA:AA
Src MAC : BB:BB:BB:BB:BB:BB
```

---

# 🎯 Interprétation

| Champ   | Signification        |
| ------- | -------------------- |
| Src MAC | machine qui envoie   |
| Dst MAC | machine locale cible |

---

# 🧠 Étape 2 — Lire IP

```text id="c15"
Src IP : 192.168.1.10
Dst IP : 142.250.180.14
TTL : 64
```

---

# 🎯 Interprétation

| Champ  | Signification             |
| ------ | ------------------------- |
| Src IP | machine source            |
| Dst IP | serveur cible             |
| TTL    | nombre de sauts possibles |

---

# 🧠 Étape 3 — Lire TCP

```text id="c16"
Src Port : 51515
Dst Port : 443
Flags : SYN
```

---

# 🎯 Interprétation

| Champ            | Signification      |
| ---------------- | ------------------ |
| Port source      | application client |
| Port destination | service cible      |
| 443              | HTTPS              |
| SYN              | demande connexion  |

---

# 🧠 Étape 4 — Lire les données

```http id="c17"
GET / HTTP/1.1
```

---

# 🎯 Interprétation

👉 requête HTTP envoyée au serveur.

---

# 🌐 Vision complète

```text id="c18"
Ethernet
└── IP
    └── TCP
        └── HTTP
```

---

# 🧠 7️⃣ Différence TCP et UDP

| TCP      | UDP            |
| -------- | -------------- |
| fiable   | fiable! rapide         |
| connecté | sans connexion |
| ACK      | pas ACK        |
| web      | DNS/streaming  |

---

# 🎯 Comment reconnaître TCP ?

| Élément       | Indication |
| ------------- | ---------- |
| Flags SYN/ACK | TCP        |
| connexion     | TCP        |

---

# 🎯 Comment reconnaître UDP ?

| Élément     | Indication |
| ----------- | ---------- |
| pas flags   | UDP        |
| DNS souvent | UDP        |

---

# 📦 Exemple UDP

```text id="c19"
Protocol : UDP
Dst Port : 53
```

---

# 🎯 Interprétation

👉 requête DNS.

---

# 📏 8️⃣ Taille des trames

# 🎯 Taille Ethernet

| Taille  | Valeur      |
| ------- | ----------- |
| Minimum | 64 octets   |
| Maximum | 1518 octets |

---

# 🧠 MTU

MTU = Maximum Transmission Unit

souvent :

```text id="c20"
1500 octets
```

---

# ⚠️ Si données trop grandes ?

👉 fragmentation possible.

---

# 🧪 9️⃣ Cas pratiques d’interprétation

---

# 🧪 Cas 1 — Ping

```bash id="c21"
ping 8.8.8.8
```

---

# 🎯 Dans la trame

| Champ       | Valeur       |
| ----------- | ------------ |
| Protocol    | ICMP         |
| Type        | Echo Request |
| Destination | 8.8.8.8      |

---

# 🧠 Interprétation

👉 un ping est envoyé.

---

# 🧪 Cas 2 — DNS

```text id="c22"
Protocol : UDP
Dst Port : 53
```

---

# 🧠 Interprétation

👉 communication DNS.

---

# 🧪 Cas 3 — HTTP

```text id="c23"
Dst Port : 80
```

👉 HTTP.

---

# 🧪 Cas 4 — HTTPS

```text id="c24"
Dst Port : 443
```

👉 HTTPS sécurisé.

---

# 🧪 Cas 5 — TCP SYN

```text id="c25"
Flags : SYN
```

---

# 🧠 Interprétation

👉 début d’une connexion TCP.

---

# 🧪 Cas 6 — TTL

```text id="c26"
TTL : 128
```

👉 souvent machine Windows.

---

# 🧠 1️⃣0️⃣ Méthode simple pour lire une trame

# 🎯 Ordre recommandé

---

# 📌 Étape 1

Identifier :

```text id="c27"
TCP ? UDP ? ICMP ?
```

---

# 📌 Étape 2

Lire :

```text id="c28"
IP source
IP destination
```

---

# 📌 Étape 3

Lire :

```text id="c29"
Ports
```

---

# 📌 Étape 4

Lire :

```text id="c30"
Flags TCP
```

---

# 📌 Étape 5

Lire :

```text id="c31"
Data
```

---

# 📌 Étape 6

Lire :

```text id="c32"
TTL
Taille
MAC
```

---

# 🎯 Résumé global

| Élément  | Rôle             |
| -------- | ---------------- |
| Ethernet | transport local  |
| MAC      | livraison locale |
| IP       | routage          |
| TTL      | éviter boucles   |
| TCP      | fiabilité        |
| UDP      | rapidité         |
| Ports    | applications     |

---

# 🎯 Conclusion

👉 Une trame réseau est une structure complète contenant plusieurs couches imbriquées.

👉 Chaque couche ajoute des informations précises :

✔ MAC
✔ IP
✔ ports
✔ TTL
✔ données

👉 Lire une trame permet de comprendre :

* le fonctionnement réel du réseau
* les communications
* les erreurs
* les échanges Internet

👉 Cette compétence est essentielle pour :

✔ administration réseau
✔ diagnostic
✔ cybersécurité
✔ analyse Wireshark

---

# ❓ Questions pédagogiques

1️⃣ Quelle différence entre IP et MAC ?
2️⃣ Pourquoi utilise-t-on l’encapsulation ?
3️⃣ Pourquoi le TTL diminue-t-il ?
4️⃣ Comment reconnaître TCP ou UDP ?
5️⃣ Quel est le rôle des ports ?
6️⃣ Pourquoi les adresses MAC changent-elles ?
