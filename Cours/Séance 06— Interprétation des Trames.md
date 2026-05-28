# 🔍 6️⃣ Interprétation des Trames Hexadécimales

---

# 🎯 Objectifs

À la fin de cette partie, l’étudiant doit être capable de :

✔ lire une trame hexadécimale
✔ reconnaître Ethernet / IP / TCP / UDP
✔ identifier les champs importants
✔ reconnaître les services réseau
✔ comprendre le contenu transporté
✔ interpréter une communication réelle
✔ analyser une capture Wireshark simple

---

# 🎬 Introduction

Quand Wireshark capture le réseau, les données apparaissent souvent en :

# 📦 Hexadécimal

Exemple :

```text
45 00 00 34 40 06 C0 A8 01 0A
```

👉 Pour un débutant, cela semble incompréhensible 😵

Mais en réalité :

👉 chaque valeur possède une signification précise.

---

# 🧠 Très important

Une trame réseau est organisée comme :

```text
Ethernet
└── IP
    └── TCP/UDP
        └── Données
```

Chaque partie ajoute :

✔ ses champs
✔ ses informations
✔ ses règles

---

# 🌐 1️⃣ Rappel — Hexadécimal

Le réseau utilise souvent :

👉 l’hexadécimal (base 16)

---

# 📌 Valeurs hexadécimales

| Hexa | Décimal |
| ---- | ------- |
| 0A   | 10      |
| 40   | 64      |
| 80   | 128     |
| FF   | 255     |

---

# 🧠 Pourquoi l’hexadécimal ?

Parce qu’il est :

✔ compact
✔ facile pour les machines
✔ proche du binaire

---

# 📦 2️⃣ Exemple COMPLET de trame hexadécimale

```text
AA AA AA AA AA AA
BB BB BB BB BB BB
08 00
45 00 00 34 1C 46 40 00 40 06 B1 E6
C0 A8 01 0A
8E FA B4 0E
C9 3B 01 BB
00 00 00 01
00 00 00 00
50 02 20 00
91 7C 00 00
47 45 54 20 2F 20 48 54 54 50
```

---

# 🎯 Idée importante

Cette trame contient :

| Partie   | Rôle                |
| -------- | ------------------- |
| Ethernet | transport local     |
| IP       | routage             |
| TCP      | communication       |
| Data     | message utilisateur |

---

# 🌐 3️⃣ Interprétation Ethernet

---

# 📦 Partie Ethernet

```text
AA AA AA AA AA AA
BB BB BB BB BB BB
08 00
```

---

# 🔍 Découpage

| Champ           | Taille   |
| --------------- | -------- |
| MAC destination | 6 octets |
| MAC source      | 6 octets |
| EtherType       | 2 octets |

---

# 📌 MAC Destination

```text
AA:AA:AA:AA:AA:AA
```

👉 machine locale cible.

---

# 📌 MAC Source

```text
BB:BB:BB:BB:BB:BB
```

👉 machine qui envoie.

---

# 📌 EtherType

```text
08 00
```

👉 signifie :

# 🌍 IPv4

---

# 📚 EtherType importants

| Valeur | Signification |
| ------ | ------------- |
| 08 00  | IPv4          |
| 08 06  | ARP           |
| 86 DD  | IPv6          |

---

# 🎯 Interprétation rapide

| Valeur détectée | Signification |
| --------------- | ------------- |
| 08 00           | paquet IPv4   |
| 08 06           | requête ARP   |
| 86 DD           | IPv6          |

---

# 🌐 4️⃣ Interprétation IP

---

# 📦 Partie IP

```text
45 00 00 34 1C 46 40 00 40 06 B1 E6
C0 A8 01 0A
8E FA B4 0E
```

---

# 🔍 Champs IP importants

| Champ       | Valeur         |
| ----------- | -------------- |
| 45          | version IP     |
| 00 34       | taille paquet  |
| 40          | TTL            |
| 06          | protocole      |
| C0 A8 01 0A | IP source      |
| 8E FA B4 0E | IP destination |

---

# 📌 Le champ 45

```text
45
```

---

# 🎯 Interprétation

| Valeur | Signification    |
| ------ | ---------------- |
| 4      | IPv4             |
| 5      | taille header IP |

---

# 📌 Taille du paquet

```text
00 34
```

---

# 🔍 Conversion

```text
0x0034 = 52 octets
```

👉 taille du paquet IP.

---

# 📌 TTL

```text
40
```

---

# 🔍 Conversion

```text
0x40 = 64
```

👉 TTL = 64

---

# 🧠 Interprétation TTL

| TTL | Système probable   |
| --- | ------------------ |
| 64  | Linux              |
| 128 | Windows            |
| 255 | équipements réseau |

---

# 📌 Champ Protocol

```text
06
```

---

# 🎯 Signification

| Valeur | Protocole |
| ------ | --------- |
| 06     | TCP       |
| 11     | UDP       |
| 01     | ICMP      |

---

# 🧠 Très important

👉 Ce champ permet immédiatement de savoir :

✔ TCP
✔ UDP
✔ ICMP

---

# 📌 IP Source

```text
C0 A8 01 0A
```

---

# 🔍 Conversion

| Hexa | Décimal |
| ---- | ------- |
| C0   | 192     |
| A8   | 168     |
| 01   | 1       |
| 0A   | 10      |

---

# 🌍 Résultat

```text
192.168.1.10
```

---

# 📌 IP Destination

```text
8E FA B4 0E
```

---

# 🌍 Résultat

```text
142.250.180.14
```

👉 serveur Google.

---

# 🌐 5️⃣ Interprétation TCP

---

# 📦 Partie TCP

```text
C9 3B 01 BB
50 02 20 00
```

---

# 🔍 Découpage

| Champ | Valeur           |
| ----- | ---------------- |
| C9 3B | Port source      |
| 01 BB | Port destination |
| 50 02 | Flags TCP        |

---

# 📌 Port Destination

```text
01 BB
```

---

# 🔍 Conversion

```text
443
```

---

# 🎯 Interprétation

👉 HTTPS

---

# 📚 Ports importants

| Port | Service |
| ---- | ------- |
| 80   | HTTP    |
| 443  | HTTPS   |
| 53   | DNS     |
| 22   | SSH     |
| 25   | SMTP    |

---

# 📌 Flags TCP

```text
50 02
```

---

# 🎯 Interprétation

| Flag | Signification    |
| ---- | ---------------- |
| SYN  | début connexion  |
| ACK  | accusé réception |
| FIN  | fermeture        |
| RST  | réinitialisation |

---

# 🧠 Très important

👉 SYN = début communication TCP.

---

# 🌐 6️⃣ Interprétation UDP

---

# 📦 Exemple UDP

```text
11
0035
```

---

# 🎯 Interprétation

| Valeur | Signification |
| ------ | ------------- |
| 11     | UDP           |
| 53     | DNS           |

---

# 🧠 Comment reconnaître UDP ?

| Élément       | UDP |
| ------------- | --- |
| pas flags TCP | ✔   |
| protocole 11  | ✔   |
| DNS fréquent  | ✔   |

---

# 🌐 7️⃣ Interprétation des données (Payload)

---

# 📦 Données

```text
47 45 54 20 2F
```

---

# 🔍 Conversion ASCII

| Hexa | ASCII |
| ---- | ----- |
| 47   | G     |
| 45   | E     |
| 54   | T     |

---

# 🌍 Résultat

```text
GET /
```

---

# 🎯 Interprétation

👉 requête HTTP vers serveur web.

---

# 📚 Messages fréquents

| Message      | Signification |
| ------------ | ------------- |
| GET          | requête web   |
| POST         | envoi données |
| DNS Query    | demande DNS   |
| SYN          | début TCP     |
| Echo Request | ping          |

---

# 🌐 8️⃣ Comment reconnaître rapidement une trame ?

---

# 🎯 Méthode professionnelle

---

# 📌 Étape 1

Lire :

```text
EtherType
```

---

# 🎯 Déduire

| Valeur | Type |
| ------ | ---- |
| 08 00  | IPv4 |
| 08 06  | ARP  |

---

# 📌 Étape 2

Lire :

```text
Protocol
```

---

# 🎯 Déduire

| Valeur | Type |
| ------ | ---- |
| 06     | TCP  |
| 11     | UDP  |
| 01     | ICMP |

---

# 📌 Étape 3

Lire :

```text
Ports
```

---

# 🎯 Déduire

| Port | Service |
| ---- | ------- |
| 80   | HTTP    |
| 443  | HTTPS   |
| 53   | DNS     |

---

# 📌 Étape 4

Lire :

```text
Flags
```

---

# 🎯 Déduire

| Flag | Signification |
| ---- | ------------- |
| SYN  | ouverture     |
| ACK  | confirmation  |
| FIN  | fermeture     |

---

# 📌 Étape 5

Lire :

```text
Payload
```

---

# 🎯 Déduire

| Payload | Signification |
| ------- | ------------- |
| GET     | HTTP          |
| Query   | DNS           |
| Echo    | Ping          |

---

# 🌐 9️⃣ Exemple COMPLET d’interprétation

| Élément   | Valeur          | Interprétation |
| --------- | --------------- | -------------- |
| EtherType | 08 00           | IPv4           |
| Protocol  | 06              | TCP            |
| Port 443  | HTTPS           | site sécurisé  |
| TTL 64    | Linux probable  | machine Linux  |
| SYN       | début connexion | ouverture TCP  |
| GET       | HTTP            | requête web    |

---

# 🎯 Résumé global

| Champ     | Permet de savoir  |
| --------- | ----------------- |
| EtherType | IPv4 / ARP / IPv6 |
| Protocol  | TCP / UDP / ICMP  |
| Ports     | service utilisé   |
| TTL       | système probable  |
| Flags     | état connexion    |
| Payload   | contenu réel      |

---

# 🎯 Conclusion

👉 Une trame hexadécimale contient énormément d’informations.

👉 En lisant correctement :

✔ EtherType
✔ IP
✔ Protocol
✔ Ports
✔ Flags
✔ Payload

👉 on peut comprendre :

✔ le type de communication
✔ le service utilisé
✔ le protocole
✔ le système probable
✔ le contenu échangé

👉 C’est exactement ce que fait un administrateur réseau ou un analyste Wireshark professionnel.
