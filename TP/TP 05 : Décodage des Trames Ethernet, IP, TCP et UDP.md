# 🧪 TP 05 : Interprétation des Trames Hexadécimales avec Wireshark

## 🎯 Objectifs

À la fin de ce TP, l'étudiant sera capable de :

✅ Lire une trame hexadécimale

✅ Identifier les couches Ethernet, IP, TCP et UDP

✅ Déterminer les adresses MAC et IP

✅ Identifier les protocoles utilisés

✅ Reconnaître les services réseau à partir des ports

✅ Interpréter les flags TCP

✅ Comprendre les données transportées

✅ Analyser une capture Wireshark simple

---

# 📖 Introduction

Lorsqu'une communication réseau circule sur Internet, elle est encapsulée dans plusieurs couches :

```text
Ethernet
└── IP
    └── TCP / UDP
        └── Données (Payload)
```

Chaque couche ajoute des informations permettant d'acheminer les données jusqu'à leur destination.

L'objectif de ce TP est d'apprendre à interpréter ces informations à partir d'une trame hexadécimale.

---

# 📚 Rappels utiles

## 📦 EtherType

| Valeur | Signification |
| ------ | ------------- |
| 08 00  | IPv4          |
| 08 06  | ARP           |
| 86 DD  | IPv6          |

---

## 🔗 Protocoles IP

| Valeur | Protocole |
| ------ | --------- |
| 01     | ICMP      |
| 06     | TCP       |
| 11     | UDP       |

---

## 🚪 Ports fréquents

| Port | Service |
| ---- | ------- |
| 22   | SSH     |
| 53   | DNS     |
| 80   | HTTP    |
| 443  | HTTPS   |

---

## 🚩 Flags TCP

| Flag | Signification    |
| ---- | ---------------- |
| SYN  | Début connexion  |
| ACK  | Confirmation     |
| FIN  | Fermeture        |
| RST  | Réinitialisation |

---

# 🌐 Cas d'étude complet

## Situation

Un utilisateur ouvre son navigateur Web et accède à un site sécurisé.

Wireshark capture la trame suivante :

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

47 45 54 20 2F
```

---

# 🔍 1. Analyse Ethernet

## Partie Ethernet

```text
AA AA AA AA AA AA
BB BB BB BB BB BB
08 00
```

### Résultat

| Champ           | Valeur            |
| --------------- | ----------------- |
| MAC Destination | AA:AA:AA:AA:AA:AA |
| MAC Source      | BB:BB:BB:BB:BB:BB |
| EtherType       | 08 00             |
| Protocole       | IPv4              |

---

## 📖 Explication des champs

### 📌 MAC Destination

Adresse physique du destinataire sur le réseau local.

Exemple :

```text
AA:AA:AA:AA:AA:AA
```

---

### 📌 MAC Source

Adresse physique de l'émetteur.

Exemple :

```text
BB:BB:BB:BB:BB:BB
```

---

### 📌 EtherType

Permet d'identifier le protocole transporté.

| Valeur | Signification |
| ------ | ------------- |
| 08 00  | IPv4          |
| 08 06  | ARP           |
| 86 DD  | IPv6          |

Exemple :

```text
08 00
```

👉 La couche suivante est IPv4.

---

# 🔍 2. Analyse IP

## Partie IP

```text
45 00 00 34 1C 46 40 00 40 06 B1 E6
C0 A8 01 0A
8E FA B4 0E
```

### Résultat

| Champ           | Valeur Hexa | Conversion | Interprétation          |
| --------------- | ----------- | ---------- | ----------------------- |
| Version + IHL   | 45          | 4 et 5     | IPv4 + Header 20 octets |
| Type de Service | 00          | 0          | Service normal          |
| Longueur Totale | 00 34       | 52         | Taille du paquet        |
| Identifiant     | 1C 46       | 7238       | ID du paquet            |
| Flags           | 40 00       | DF=1       | Pas de fragmentation    |
| TTL             | 40          | 64         | Durée de vie            |
| Protocol        | 06          | 6          | TCP                     |
| Checksum        | B1 E6       | 45542      | Contrôle d'erreur       |

---

## 📖 Explication des champs

### 📌 Version

| Valeur | Signification |
| ------ | ------------- |
| 4      | IPv4          |
| 6      | IPv6          |

---

### 📌 IHL

Taille de l'en-tête IP.

| Valeur | Taille    |
| ------ | --------- |
| 5      | 20 octets |
| 6      | 24 octets |
| 7      | 28 octets |

Calcul :

```text
IHL × 4
```

Exemple :

```text
5 × 4 = 20 octets
```

---

### 📌 Longueur Totale

```text
00 34
```

Conversion :

```text
0x0034 = 52
```

👉 Le paquet mesure 52 octets.

---

### 📌 TTL

```text
40
```

Conversion :

```text
0x40 = 64
```

| TTL | Système probable |
| --- | ---------------- |
| 64  | Linux            |
| 128 | Windows          |
| 255 | Routeur          |

---

### 📌 Protocol

| Valeur | Protocole |
| ------ | --------- |
| 01     | ICMP      |
| 06     | TCP       |
| 11     | UDP       |

Exemple :

```text
06
```

👉 TCP

---

### 📌 Adresse IP Source

```text
C0 A8 01 0A
```

| Hexa | Décimal |
| ---- | ------- |
| C0   | 192     |
| A8   | 168     |
| 01   | 1       |
| 0A   | 10      |

Résultat :

```text
192.168.1.10
```

---

### 📌 Adresse IP Destination

```text
8E FA B4 0E
```

Résultat :

```text
142.250.180.14
```

---

# 🔍 3. Analyse TCP

## Partie TCP

```text
C9 3B 01 BB
50 02 20 00
```

### Résultat

| Champ            | Valeur |
| ---------------- | ------ |
| Port Source      | 51515  |
| Port Destination | 443    |
| Service          | HTTPS  |
| Flags            | SYN    |

---

## 📖 Explication des champs

### 📌 Port Source

Port temporaire choisi par le client.

Exemples :

| Port  |
| ----- |
| 50000 |
| 51515 |
| 55000 |

---

### 📌 Port Destination

| Port | Service |
| ---- | ------- |
| 22   | SSH     |
| 53   | DNS     |
| 80   | HTTP    |
| 443  | HTTPS   |

Exemple :

```text
01 BB
```

Conversion :

```text
443
```

👉 HTTPS

---

### 📌 Flags TCP

| Flag | Signification    |
| ---- | ---------------- |
| SYN  | Début connexion  |
| ACK  | Confirmation     |
| FIN  | Fermeture        |
| RST  | Réinitialisation |
| PSH  | Envoi immédiat   |

---

### 📌 SYN

```text
50 02
```

👉 Début de connexion TCP.

---

### 📌 SYN + ACK

```text
50 12
```

👉 Réponse du serveur.

---

### 📌 ACK

```text
50 10
```

👉 Connexion établie.

---

### 📌 FIN

```text
50 11
```

👉 Fermeture normale.

---

### 📌 RST

```text
50 14
```

👉 Réinitialisation brutale.

---

## 🔄 Three-Way Handshake TCP

```text
Client                     Serveur

SYN      ------------------>

          <---------------- SYN + ACK

ACK      ------------------>
```

---

# 🔍 4. Analyse du Payload

## Partie Données

```text
47 45 54 20 2F
```

### Conversion ASCII

| Hexa | ASCII  |
| ---- | ------ |
| 47   | G      |
| 45   | E      |
| 54   | T      |
| 20   | espace |
| 2F   | /      |

Résultat :

```text
GET /
```

---

## 📖 Explication

| Message      | Signification       |
| ------------ | ------------------- |
| GET          | Demande de page Web |
| POST         | Envoi de données    |
| HTTP         | Réponse Web         |
| DNS Query    | Requête DNS         |
| Echo Request | Ping                |

---

# 🎯 Conclusion du cas étudié

| Élément          | Interprétation |
| ---------------- | -------------- |
| EtherType        | IPv4           |
| Protocol         | TCP            |
| Port Destination | 443            |
| Service          | HTTPS          |
| TTL              | 64             |
| IP Source        | 192.168.1.10   |
| IP Destination   | 142.250.180.14 |
| Flag             | SYN            |
| Payload          | GET /          |

👉 Un poste client ouvre une connexion HTTPS vers un serveur Web.

---

# ✏️ Exercice 1 : Analyse Ethernet

```text
11 11 11 11 11 11
22 22 22 22 22 22
08 06
```

Questions :

1. Quelle est la MAC destination ?
2. Quelle est la MAC source ?
3. Quelle est la valeur EtherType ?
4. Quel protocole est transporté ?

---

# ✏️ Exercice 2 : Analyse IP

```text
45 00 00 28
40 01
C0 A8 01 05
08 08 08 08
```

Questions :

1. Quelle est la version IP ?
2. Quelle est la taille du paquet ?
3. Quelle est la valeur TTL ?
4. Quel protocole est utilisé ?
5. Quelle est l'adresse IP source ?
6. Quelle est l'adresse IP destination ?

---

# ✏️ Exercice 3 : Analyse TCP

```text
C3 50 00 50
50 12
```

Questions :

1. Quel est le port source ?
2. Quel est le port destination ?
3. Quel service est utilisé ?
4. Quels flags sont actifs ?
5. À quelle étape de la connexion correspond cette trame ?

---

# ✏️ Exercice 4 : Analyse UDP

```text
11
00 35
```

Questions :

1. Quel protocole est utilisé ?
2. TCP ou UDP ?
3. Quel est le port destination ?
4. Quel service correspond à ce port ?

---

# ✏️ Exercice 5 : Conversion IP

Convertir :

```text
C0 A8 01 01
```

```text
08 08 08 08
```

```text
AC 10 00 01
```

---

# ✏️ Exercice 6 : Analyse Complète

```text
AA AA AA AA AA AA
BB BB BB BB BB BB
08 00

45 00 00 34
40 11

C0 A8 01 20
08 08 08 08

C3 50 00 35

44 4E 53
```

Compléter :

| Élément               | Valeur |
| --------------------- | ------ |
| EtherType             |        |
| Version IP            |        |
| TTL                   |        |
| Protocole             |        |
| IP Source             |        |
| IP Destination        |        |
| Port Destination      |        |
| Service               |        |
| Type de communication |        |

---

# 🏆 Travail à rendre

✅ Calculs détaillés

✅ Conversions Hexadécimal → Décimal

✅ Réponses aux questions

✅ Conclusion pour chaque exercice

---

# 🎓 Bilan

À la fin de ce TP, vous devez être capable de déterminer :

✔ Qui envoie ?

✔ Qui reçoit ?

✔ Quel protocole est utilisé ?

✔ Quel service est utilisé ?

✔ Quel est le contenu transporté ?

✔ S'agit-il de TCP, UDP ou ICMP ?

✔ La connexion est-elle en ouverture, en cours ou en fermeture ?

✔ Quelle est la nature de la communication observée ?

---

# ✏️ ✏️ Exercice 7 : Analyse complète (HTTPS SYN-ACK)

```text
AA AA AA AA AA AA
CC CC CC CC CC CC
08 00

45 00 00 3C
1A 2B 40 00
40 06 A1 B2

C0 A8 01 64
8E FA B4 0E

D4 31 01 BB

00 00 00 00
00 00 00 00

50 12 72 10
A1 B2 00 00

```

---

## 📌 Questions

1. Quelle est la MAC destination ?
2. Quelle est la MAC source ?
3. Quelle est la valeur EtherType ?
4. Quelle est la version IP ?
5. Quelle est la taille du paquet ?
6. Quelle est la valeur TTL ?
7. Quel protocole est utilisé ?
8. Quelle est l’IP source ?
9. Quelle est l’IP destination ?
10. Quel est le port source ?
11. Quel est le port destination ?
12. Quel service est utilisé ?
13. Quels flags sont actifs ?
14. À quelle étape de la connexion correspond cette trame ?

---

## 🧠 Indice étudiant

* Port 443 = HTTPS 🔐
* Flags `50 12` = SYN + ACK 🔁
* TTL 64 = Linux 🐧

---

# ✏️ ✏️ Exercice 8 : Analyse complète (DNS UDP)

```text
11 11 11 11 11 11
22 22 22 22 22 22
08 00

45 00 00 2C
B4 12 00 00
40 11 7C D3

C0 A8 01 0A
08 08 08 08

E1 23 00 35
00 18

44 4E 53 01 00
```

---

## 📌 Questions

1. Quelle est la MAC destination ?
2. Quelle est la MAC source ?
3. Quelle est la valeur EtherType ?
4. Quelle est la version IP ?
5. Quelle est la taille du paquet ?
6. Quelle est la valeur TTL ?
7. Quel protocole est utilisé ?
8. Quelle est l’IP source ?
9. Quelle est l’IP destination ?
10. TCP ou UDP ?
11. Quel est le port destination ?
12. Quel service est utilisé ?
13. Que signifie le payload ?

---

## 🧠 Indice étudiant

* `11` = UDP 🚀
* Port 53 = DNS 🔎
* Payload “DNS” = requête de résolution de nom

---

# 🎯 Remarque pédagogique (important)

Ces deux exercices couvrent :

✔ Exercice 7 → TCP (HTTPS + SYN/ACK)
✔ Exercice 8 → UDP (DNS request)

👉 Donc tu as maintenant :

* Ethernet
* IP
* TCP
* UDP
* Flags
* Ports
* Payload

💡 Ce sont exactement les 2 cas les plus importants en examen Wireshark.


