# 🧪 TP 04 — Routage simple entre deux réseaux Linux

# 🎓 Module : Administration Réseau

---

# 🧠 🎯 Objectifs

À la fin de ce TP, l’étudiant sera capable de :

✔ Comprendre le rôle du routeur
✔ Configurer des adresses IP
✔ Ajouter une gateway
✔ Activer le routage IP
✔ Tester la communication entre deux réseaux

---

# 🌐 Architecture réseau

```text
PC1 ---- ROUTER ---- PC2
```

---

# 📡 Plan d’adressage

| Machine | Adresse IP      |
| ------- | --------------- |
| pc1     | 192.168.1.10/24 |
| router  | 192.168.1.1/24  |
| router  | 192.168.2.1/24  |
| pc2     | 192.168.2.10/24 |

---

# ⚙️ PARTIE 1 — Création des namespaces

```bash
sudo ip netns add pc1
sudo ip netns add pc2
sudo ip netns add router
```

---

# 🔌 PARTIE 2 — Création des connexions

```bash
sudo ip link add veth-pc1 type veth peer name veth-r1

sudo ip link add veth-pc2 type veth peer name veth-r2
```

---

# 📦 PARTIE 3 — Affectation des interfaces

```bash
sudo ip link set veth-pc1 netns pc1
sudo ip link set veth-r1 netns router

sudo ip link set veth-pc2 netns pc2
sudo ip link set veth-r2 netns router
```

---

# 🌐 PARTIE 4 — Configuration IP

# 💻 PC1

```bash
sudo ip netns exec pc1 ip addr add 192.168.1.10/24 dev veth-pc1

sudo ip netns exec pc1 ip link set veth-pc1 up

sudo ip netns exec pc1 ip route add default via 192.168.1.1
```

---

# 💻 PC2

```bash
sudo ip netns exec pc2 ip addr add 192.168.2.10/24 dev veth-pc2

sudo ip netns exec pc2 ip link set veth-pc2 up

sudo ip netns exec pc2 ip route add default via 192.168.2.1
```

---

# 🧠 ROUTER

```bash
sudo ip netns exec router ip addr add 192.168.1.1/24 dev veth-r1

sudo ip netns exec router ip addr add 192.168.2.1/24 dev veth-r2

sudo ip netns exec router ip link set veth-r1 up

sudo ip netns exec router ip link set veth-r2 up
```

---

# 🔥 PARTIE 5 — Activation du routage

```bash
sudo ip netns exec router sysctl -w net.ipv4.ip_forward=1
```

---

# 📡 PARTIE 6 — Tests

# ✅ Test 1

```bash
sudo ip netns exec pc1 ping 192.168.1.1
```

---

# ✅ Test 2

```bash
sudo ip netns exec pc2 ping 192.168.2.1
```

---

# 🚀 Test final

```bash
sudo ip netns exec pc1 ping 192.168.2.10
```

---

# 🔍 PARTIE 7 — Vérification

## Voir les IP

```bash
sudo ip netns exec pc1 ip a
```

---

## Voir les routes

```bash
sudo ip netns exec pc1 ip route
```

---

# 🧹 PARTIE 8 — Nettoyage

```bash
sudo ip netns delete pc1

sudo ip netns delete pc2

sudo ip netns delete router
```

---

# 🧠 Questions pédagogiques

1️⃣ Pourquoi PC1 a besoin d’une gateway ?
2️⃣ Quel est le rôle du routeur ?
3️⃣ Pourquoi active-t-on ip_forward ?
4️⃣ Pourquoi PC1 et PC2 ne communiquent pas directement ?

---

# 🎯 Résultat attendu

✔ Communication entre deux réseaux
✔ Compréhension du routage
✔ Compréhension de la gateway
✔ Compréhension du forwarding IP
