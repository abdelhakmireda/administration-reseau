
---

# 🎓 Séance 02 — Modèles Réseau (OSI & TCP/IP) et Adressage IP

---

## 🎬 Introduction

Dans la séance précédente, une question essentielle a été posée :

👉 **Comment les machines communiquent-elles ?**

On sait maintenant que les données sont envoyées sous forme de **paquets** 📦

Mais une autre question apparaît :

👉 **Qui décide comment envoyer ces paquets ?**
👉 **Comment deux machines peuvent-elles se comprendre ?**

---

💡 La réponse :
Les communications réseau suivent des **règles organisées en couches**

---

## 🧠 1️⃣ Pourquoi utiliser des modèles réseau ?

Si chaque machine communiquait à sa manière :

❌ chaos total
❌ incompatibilité
❌ aucune communication fiable

---

### 💡 Solution

Créer un modèle standard :

👉 qui organise la communication
👉 qui définit des règles
👉 qui sépare les responsabilités

---

## 🏗️ 2️⃣ Le modèle OSI

Le modèle **OSI (Open Systems Interconnection)** est un modèle théorique composé de **7 couches**.

---

### 🎯 Objectif

Diviser la communication réseau en plusieurs niveaux logiques.

---

## 📚 Les 7 couches OSI

| N° | Couche       | Rôle                           |
| -- | ------------ | ------------------------------ |
| 7  | Application  | Interaction avec l’utilisateur |
| 6  | Présentation | Format des données             |
| 5  | Session      | Gestion des sessions           |
| 4  | Transport    | Fiabilité (TCP/UDP)            |
| 3  | Réseau       | Routage (IP)                   |
| 2  | Liaison      | Communication locale (MAC)     |
| 1  | Physique     | Transmission (câble, signal)   |

---

## 🧠 Explication simplifiée (très importante)

👉 Chaque couche a un rôle précis.

👉 Les données descendent les couches à l’envoi, puis remontent à la réception.

---

## 🎯 Exemple concret : envoi d’un message

Un utilisateur envoie :

👉 "Bonjour"

---

### 📤 Côté envoi (descente)

1. Application → crée le message
2. Présentation → encode
3. Session → ouvre la communication
4. Transport → découpe en paquets
5. Réseau → ajoute l’adresse IP
6. Liaison → ajoute adresse MAC
7. Physique → envoie les bits

---

### 📥 Côté réception (montée)

Le processus inverse se produit :

👉 reconstruction complète du message

---

## 🧠 Analogie simple

Le modèle OSI fonctionne comme un système de livraison 📦 :

| Couche      | Rôle              |
| ----------- | ----------------- |
| Application | écrire le message |
| Transport   | emballer          |
| Réseau      | adresser          |
| Physique    | livrer            |

---

## ⚠️ Important

Le modèle OSI est :

👉 théorique
👉 pédagogique
👉 utilisé pour comprendre

---

## 🌐 3️⃣ Le modèle TCP/IP

Le modèle TCP/IP est le modèle **réel utilisé sur Internet**.

---

### 📚 Les couches TCP/IP

| Couche TCP/IP | Correspondance OSI |
| ------------- | ------------------ |
| Application   | OSI 7-6-5          |
| Transport     | OSI 4              |
| Internet      | OSI 3              |
| Accès réseau  | OSI 2-1            |

---

### 🧠 Idée clé

👉 TCP/IP est plus simple et plus pratique
👉 OSI est plus détaillé et pédagogique

---

## 🔄 Comparaison OSI vs TCP/IP

| OSI          | TCP/IP    |
| ------------ | --------- |
| 7 couches    | 4 couches |
| Théorique    | Pratique  |
| Détail élevé | Simplifié |

---

## 🌐 4️⃣ Introduction à l’adressage IP

Pour communiquer dans un réseau, chaque machine doit avoir une identité.

👉 Cette identité s’appelle :

👉 **Adresse IP**

---

### 📌 Exemple

```text
192.168.1.10
```

---

## 🧠 Structure d’une IP

Une adresse IP est composée de :

👉 une partie réseau
👉 une partie machine (hôte)

---

### 🎯 Exemple

```text
192.168.1.10
```

* 192.168.1 → réseau
* 10 → machine

---

## 🌍 Types d’adresses IP

---

### 🔹 IP privée

Utilisée dans les réseaux internes :

* 192.168.x.x
* 10.x.x.x
* 172.16.x.x

---

### 🔹 IP publique

Utilisée sur Internet :

👉 unique dans le monde

---

## ⚙️ 5️⃣ Notion de communication IP

Pour qu’une communication fonctionne :

👉 il faut :

* une adresse source
* une adresse destination

---

### 🎯 Exemple

Machine A → 192.168.1.10
Machine B → 192.168.1.20

👉 communication possible si réseau compatible

---

## 🧠 Vision globale

Une communication réseau repose sur :

* des couches (OSI / TCP-IP)
* des règles
* des adresses

---

### 📌 Résumé

* OSI = modèle pédagogique
* TCP/IP = modèle réel
* IP = identité réseau
* communication = échange structuré

---

## 🎯 Conclusion

Comprendre les modèles réseau permet de :

👉 analyser une communication
👉 comprendre les erreurs
👉 configurer correctement un réseau

---

## ❓ Questions de réflexion

1. Pourquoi le modèle OSI est-il important ?
2. Quelle est la différence entre OSI et TCP/IP ?
3. Quel est le rôle de la couche transport ?
4. Pourquoi une adresse IP est-elle nécessaire ?

---

