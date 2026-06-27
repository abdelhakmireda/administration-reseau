

---

# 📦 Séance 07 — Analyse Interactive des Trames Réseau

## 🌐 Lien du projet en ligne

Le site interactif de la séance est disponible ici :

[https://interactive-trame-analyzer.vercel.app/](https://interactive-trame-analyzer.vercel.app/)

Ce site a été conçu pour aider les étudiants à comprendre comment analyser une trame réseau étape par étape, avant de passer à l’utilisation de Wireshark.

---

## 🎯 Objectif du projet

Ce projet permet d’apprendre l’analyse des trames réseau d’une manière simple, progressive et interactive.

L’étudiant commence par identifier la partie Ethernet, puis il analyse la valeur EtherType pour savoir si la trame contient IPv4, ARP ou IPv6.

Si la trame contient IPv4, l’étudiant continue l’analyse avec le champ Protocol pour déterminer si le paquet transporte TCP, UDP ou ICMP.

La logique générale suivie est la suivante :

```text
Ethernet → EtherType → IPv4 / ARP → TCP / UDP / ICMP → Analyse → Conclusion
```

---

## 🧠 Idée principale

Une trame réseau n’est pas une suite de valeurs hexadécimales au hasard.

Chaque partie possède une place précise et une signification particulière.

Le site aide l’étudiant à comprendre cette organisation en suivant une méthode claire :

```text
1. Lire Ethernet
2. Identifier EtherType
3. Déterminer IPv4 ou ARP
4. Si IPv4, lire le champ Protocol
5. Identifier TCP, UDP ou ICMP
6. Lire les ports, flags ou messages
7. Rédiger une conclusion
```

---

## 📚 Protocoles étudiés

Le projet permet d’étudier les principaux protocoles utilisés dans l’analyse des trames réseau :

### Ethernet

Ethernet est la première partie à analyser.

Il contient :

```text
MAC destination = 6 octets
MAC source      = 6 octets
EtherType       = 2 octets
```

Les valeurs importantes de EtherType sont :

```text
08 00 → IPv4
08 06 → ARP
86 DD → IPv6
```

---

### IPv4

IPv4 permet d’identifier :

```text
IP source
IP destination
Protocole transporté
```

Le champ Protocol permet de savoir ce que contient IPv4 :

```text
01 → ICMP
06 → TCP
11 → UDP
```

---

### TCP

TCP est utilisé pour les communications fiables.

Il utilise des ports et des flags.

Ports importants :

```text
22  → SSH
53  → DNS
80  → HTTP
443 → HTTPS
```

Flags importants :

```text
SYN      → début de connexion
SYN, ACK → réponse du serveur
ACK      → confirmation
FIN, ACK → fermeture normale
RST, ACK → connexion refusée ou réinitialisée
PSH, ACK → données envoyées
```

---

### UDP

UDP est un protocole plus simple que TCP.

Il est souvent utilisé pour les communications rapides comme DNS, DHCP ou NTP.

Structure UDP :

```text
Port source      = 2 octets
Port destination = 2 octets
Longueur         = 2 octets
Checksum         = 2 octets
```

Le port le plus important dans cette séance est :

```text
53 → DNS
```

---

### ICMP

ICMP est utilisé pour les messages de contrôle réseau.

Il est notamment utilisé avec la commande :

```text
ping
```

Messages importants :

```text
08 00 → Echo Request
00 00 → Echo Reply
03    → Destination Unreachable
11 00 → Time Exceeded
```

---

### ARP

ARP permet de trouver une adresse MAC à partir d’une adresse IP.

Il répond à une question de ce type :

```text
Qui possède l’adresse IP 192.168.1.1 ?
```

Valeurs importantes :

```text
00 01 → ARP Request
00 02 → ARP Reply
```

---

## 🧪 Partie pratique du site

Le site contient une partie pratique interactive.

L’étudiant peut :

```text
Générer une trame hexadécimale
Lire la trame
Choisir IPv4 ou ARP
Choisir TCP, UDP ou ICMP si la trame contient IPv4
Compléter uniquement les champs nécessaires
Écrire une conclusion
Recevoir une correction automatique
Voir son score
Lire l’explication de la bonne réponse
```

---

## 📝 Formulaire dynamique

Le formulaire change automatiquement selon les choix de l’étudiant.

Si l’étudiant choisit IPv4, le site affiche les champs IPv4 :

```text
Protocole
IP source
IP destination
```

Ensuite, si l’étudiant choisit TCP, le site affiche :

```text
Port TCP
Service TCP
Flag TCP
```

Si l’étudiant choisit UDP, le site affiche :

```text
Port UDP
Service UDP
```

Si l’étudiant choisit ICMP, le site affiche :

```text
Message ICMP
```

Si l’étudiant choisit ARP, le site affiche :

```text
Opcode ARP
IP émetteur
IP cible
```

---

## 🦈 Préparation à Wireshark

Ce projet prépare les étudiants à mieux comprendre Wireshark.

Avant d’utiliser Wireshark, l’étudiant apprend à comprendre ce que représente chaque information :

```text
Adresse MAC
Adresse IP
EtherType
Protocol
Port source
Port destination
Flag TCP
Message ICMP
Opcode ARP
```

Ainsi, lorsqu’il ouvrira Wireshark, il saura déjà interpréter les lignes affichées.

---

## 🔎 Filtres Wireshark utiles

Les filtres utiles pour la séance sont :

```text
icmp
dns
tcp
udp
http
arp
tcp.port == 80
tcp.port == 443
udp.port == 53
ip.addr == 192.168.1.10
tcp.flags.syn == 1
tcp.flags.reset == 1
```

---

## ✅ Compétences visées

À la fin de cette séance, l’étudiant doit être capable de :

```text
Identifier une trame Ethernet
Reconnaître IPv4 ou ARP
Lire le champ Protocol dans IPv4
Identifier TCP, UDP ou ICMP
Reconnaître les ports importants
Comprendre les flags TCP
Interpréter les messages ICMP
Analyser une requête ou une réponse ARP
Rédiger une conclusion technique simple
Faire le lien avec Wireshark
```

---

## 🧩 Exemple de conclusion attendue

```text
La trame montre que le poste 192.168.1.10 communique avec le serveur 8.8.8.8.
Le protocole utilisé est UDP.
Le port destination 53 indique le service DNS.
Conclusion : il s’agit d’une requête DNS.
```

---

## 🧠 Méthode à retenir

```text
Ethernet → EtherType → IPv4 ou ARP → Protocol → TCP / UDP / ICMP → Ports / Flags / Message → Conclusion
```

L’objectif n’est pas seulement de trouver des valeurs, mais de comprendre le sens de la communication réseau.

---

## 👨‍🏫 Réalisé par

**Professeur Abdelhakmi Reda**

