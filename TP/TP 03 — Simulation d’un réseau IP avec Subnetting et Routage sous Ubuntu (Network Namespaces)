
---
# 🧠 🎯 Objectifs pédagogiques

À la fin de ce TP, l’étudiant sera capable de :

✔ Comprendre la communication entre sous-réseaux
✔ Configurer des adresses IP sous Linux
✔ Comprendre la notion de gateway
✔ Activer le routage IP
✔ Tester et diagnostiquer un réseau

---

# 🧱 🏗️ Architecture technique

👉 1 seule VM Ubuntu (2GB RAM / 10GB disque)

👉 Simulation de :

| Machine | Type    | Réseau         |
| ------- | ------- | -------------- |
| pc1     | client  | 192.168.1.0/26 |
| pc2     | client  | 192.168.2.0/26 |
| router  | routeur | 2 interfaces   |

---

# 🌐 📡 Plan d’adressage

| Machine | IP                        | Masque | Gateway     |
| ------- | ------------------------- | ------ | ----------- |
| pc1     | 192.168.1.10              | /26    | 192.168.1.1 |
| pc2     | 192.168.2.10              | /26    | 192.168.2.1 |
| router  | 192.168.1.1 / 192.168.2.1 |        |             |

---

# ⚙️ 🔧 PARTIE 1 — Préparation

```bash
sudo apt update
sudo apt install iproute2 -y
```

---

# 🏗️ PARTIE 2 — Création des machines (namespaces)

```bash
sudo ip netns add pc1
sudo ip netns add pc2
sudo ip netns add router
```

---

# 🔌 PARTIE 3 — Création des connexions réseau

```bash
sudo ip link add veth-pc1 type veth peer name veth-r1
sudo ip link add veth-pc2 type veth peer name veth-r2
```

---

# 📦 PARTIE 4 — Affectation

```bash
sudo ip link set veth-pc1 netns pc1
sudo ip link set veth-pc2 netns pc2
sudo ip link set veth-r1 netns router
sudo ip link set veth-r2 netns router
```

---

# 🌐 PARTIE 5 — Configuration IP

---

## 💻 PC1

```bash
sudo ip netns exec pc1 ip addr add 192.168.1.10/26 dev veth-pc1
sudo ip netns exec pc1 ip link set veth-pc1 up
sudo ip netns exec pc1 ip route add default via 192.168.1.1
```

---

## 💻 PC2

```bash
sudo ip netns exec pc2 ip addr add 192.168.2.10/26 dev veth-pc2
sudo ip netns exec pc2 ip link set veth-pc2 up
sudo ip netns exec pc2 ip route add default via 192.168.2.1
```

---

## 🧠 ROUTER

```bash
sudo ip netns exec router ip addr add 192.168.1.1/26 dev veth-r1
sudo ip netns exec router ip addr add 192.168.2.1/26 dev veth-r2

sudo ip netns exec router ip link set veth-r1 up
sudo ip netns exec router ip link set veth-r2 up
```

---

# 🔥 PARTIE 6 — Activation du routage

```bash
sudo ip netns exec router sysctl -w net.ipv4.ip_forward=1
```

---

# 📡 🔍 PARTIE 7 — Tests

---

## ✅ Test 1

```bash
sudo ip netns exec pc1 ping 192.168.1.1
```

---

## ✅ Test 2

```bash
sudo ip netns exec pc2 ping 192.168.2.1
```

---

## 🚀 Test final

```bash
sudo ip netns exec pc1 ping 192.168.2.10
```

---

# 💥 PARTIE 8 — Debug (TRÈS IMPORTANT)

---

## 🔍 Vérifier IP

```bash
sudo ip netns exec pc1 ip a
```

---

## 🔍 Vérifier routes

```bash
sudo ip netns exec pc1 ip route
```

---

## 🔍 Vérifier routage

```bash
sudo ip netns exec router cat /proc/sys/net/ipv4/ip_forward
```

---

# 🧹 PARTIE 9 — Reset

```bash
sudo ip netns delete pc1
sudo ip netns delete pc2
sudo ip netns delete router
```

---

# 🏆 🎯 Résultat attendu

✔ Communication intra-réseau
✔ Communication inter-réseaux
✔ Routage fonctionnel

---

# 🧠 💬 Questions pédagogiques

👉 Pourquoi pc1 ne peut pas communiquer sans routeur ?
👉 Quel est le rôle de la gateway ?
👉 Que se passe-t-il si on désactive ip_forward ?

---

# 🚀 BONUS — Script automatique

👉 (à mettre dans `/scripts/setup.sh`)

```bash
#!/bin/bash

ip netns add pc1
ip netns add pc2
ip netns add router

ip link add veth-pc1 type veth peer name veth-r1
ip link add veth-pc2 type veth peer name veth-r2

ip link set veth-pc1 netns pc1
ip link set veth-pc2 netns pc2
ip link set veth-r1 netns router
ip link set veth-r2 netns router

ip netns exec pc1 ip addr add 192.168.1.10/26 dev veth-pc1
ip netns exec pc1 ip link set veth-pc1 up
ip netns exec pc1 ip route add default via 192.168.1.1

ip netns exec pc2 ip addr add 192.168.2.10/26 dev veth-pc2
ip netns exec pc2 ip link set veth-pc2 up
ip netns exec pc2 ip route add default via 192.168.2.1

ip netns exec router ip addr add 192.168.1.1/26 dev veth-r1
ip netns exec router ip addr add 192.168.2.1/26 dev veth-r2

ip netns exec router ip link set veth-r1 up
ip netns exec router ip link set veth-r2 up

ip netns exec router sysctl -w net.ipv4.ip_forward=1
```

---

# 🎯 Conclusion

👉 Ce TP est :

✔ réel
✔ léger (1 seule VM)
✔ pédagogique
✔ niveau entreprise

---

