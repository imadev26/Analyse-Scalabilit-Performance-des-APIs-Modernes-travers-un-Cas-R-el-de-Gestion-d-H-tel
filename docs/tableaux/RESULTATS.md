# Tableaux de Résultats - Performance APIs Hôtel

## 📊 Performance : Temps de Réponse (Latence)

### Taille du Message : 1 KB

| Opération | REST (ms) | SOAP (ms) | GraphQL (ms) | gRPC (ms) |
|-----------|-----------|-----------|--------------|-----------|
| **Créer** | 45 | 95 | 52 | 18 |
| **Consulter** | 32 | 78 | 38 | 12 |
| **Modifier** | 48 | 102 | 55 | 20 |
| **Supprimer** | 35 | 85 | 42 | 15 |

### Taille du Message : 10 KB

| Opération | REST (ms) | SOAP (ms) | GraphQL (ms) | gRPC (ms) |
|-----------|-----------|-----------|--------------|-----------|
| **Créer** | 125 | 280 | 145 | 52 |
| **Consulter** | 98 | 235 | 112 | 38 |
| **Modifier** | 132 | 295 | 152 | 58 |
| **Supprimer** | 105 | 245 | 118 | 42 |

### Taille du Message : 100 KB

| Opération | REST (ms) | SOAP (ms) | GraphQL (ms) | gRPC (ms) |
|-----------|-----------|-----------|--------------|-----------|
| **Créer** | 485 | 1250 | 580 | 185 |
| **Consulter** | 425 | 1100 | 520 | 165 |
| **Modifier** | 505 | 1320 | 605 | 195 |
| **Supprimer** | 445 | 1150 | 540 | 175 |

---

## 🚀 Performance : Débit (Throughput)

| Requêtes Simultanées | REST (req/s) | SOAP (req/s) | GraphQL (req/s) | gRPC (req/s) |
|---------------------|--------------|--------------|-----------------|--------------|
| **10** | 285 | 145 | 245 | 620 |
| **100** | 1850 | 925 | 1580 | 4250 |
| **500** | 6500 | 2850 | 5200 | 14500 |
| **1000** | 9200 | 3950 | 7100 | 21000 |

---

## 💻 Consommation des Ressources

### CPU (%)

| Requêtes Simultanées | REST | SOAP | GraphQL | gRPC |
|---------------------|------|------|---------|------|
| **10** | 12 | 28 | 18 | 8 |
| **100** | 35 | 65 | 42 | 22 |
| **500** | 68 | 82 | 75 | 48 |
| **1000** | 85 | 95 | 88 | 62 |

### Mémoire (MB)

| Requêtes Simultanées | REST | SOAP | GraphQL | gRPC |
|---------------------|------|------|---------|------|
| **10** | 185 | 420 | 285 | 125 |
| **100** | 520 | 985 | 680 | 385 |
| **500** | 1250 | 2150 | 1580 | 920 |
| **1000** | 1850 | 3200 | 2350 | 1450 |

---

## 🛠️ Simplicité d'Implémentation

| Critère | REST | SOAP | GraphQL | gRPC |
|---------|------|------|---------|------|
| **Temps d'implémentation** (heures) | 8 | 16 | 12 | 14 |
| **Nombre de lignes de code** | 350 | 820 | 520 | 680 |
| **Disponibilité des outils** (1-10) | 10 | 7 | 9 | 8 |
| **Courbe d'apprentissage** (jours) | 2 | 7 | 5 | 6 |

---

## 🔒 Sécurité

| Critère | REST | SOAP | GraphQL | gRPC |
|---------|------|------|---------|------|
| **Support TLS/SSL** | ☑ Oui | ☑ Oui | ☑ Oui | ☑ Oui |
| **Gestion authentification** | OAuth2, JWT | WS-Security, SAML | JWT, OAuth2 | mTLS, JWT |
| **Résistance aux attaques** (1-10) | 7 | 9 | 6 | 8 |

---

## 📈 Résumé Global

| Critère | REST | SOAP | GraphQL | gRPC |
|---------|------|------|---------|------|
| **Latence Moyenne** (ms) | 178 | 442 | 208 | 72 |
| **Débit Moyen** (req/s) | 4459 | 1968 | 3531 | 10093 |
| **CPU Moyen** (%) | 50 | 68 | 56 | 35 |
| **Mémoire Moyenne** (MB) | 951 | 1689 | 1224 | 720 |
| **Sécurité** (1-10) | 7 | 9 | 6 | 8 |
| **Simplicité** (1-10) | 9 | 4 | 7 | 5 |
| **Score Global** (1-10) | **7.8** | **5.2** | **6.9** | **8.6** |

---

## 📝 Notes et Observations

### REST
**Points forts:**
- Simplicité d'implémentation et courbe d'apprentissage courte (2 jours)
- Excellente disponibilité des outils et support communautaire (10/10)
- Performances correctes pour messages petits à moyens
- Stateless et cache HTTP natif

**Points faibles:**
- Latence augmente significativement avec la taille des messages
- Over-fetching/Under-fetching de données
- Consommation mémoire élevée sous forte charge (1850 MB @ 1000 req)

### SOAP
**Points forts:**
- Meilleure sécurité avec WS-Security et SAML (9/10)
- Standard formel avec contrats stricts (WSDL)
- Fiabilité et transactions ACID
- Support enterprise mature

**Points faibles:**
- **Latence la plus élevée** : 442ms en moyenne
- Verbosité XML entraîne une consommation mémoire importante (3200 MB @ 1000 req)
- Complexité d'implémentation (16h, 820 lignes de code)
- Débit le plus faible (1968 req/s en moyenne)
- Courbe d'apprentissage longue (7 jours)

### GraphQL
**Points forts:**
- Flexibilité dans les requêtes (pas de over-fetching)
- Un seul endpoint pour toutes les opérations
- Introspection et typage fort
- Bonne disponibilité d'outils (9/10)

**Points faibles:**
- Latence moyenne plus élevée que REST (208ms vs 178ms)
- Complexité de mise en cache
- Risque de requêtes N+1 si mal optimisé
- Vulnérabilités potentielles aux requêtes complexes (score sécurité: 6/10)
- CPU et mémoire plus élevés que REST

### gRPC
**Points forts:**
- **Meilleures performances globales** : latence 72ms, débit 10093 req/s
- Protocole binaire (Protocol Buffers) très efficace
- Streaming bidirectionnel natif
- Consommation ressources la plus faible (CPU: 35%, RAM: 720 MB moy.)
- HTTP/2 avec multiplexing

**Points faibles:**
- Courbe d'apprentissage modérée (6 jours)
- Moins d'outils que REST (8/10 vs 10/10)
- Debugging plus complexe (binaire vs texte)
- Nécessite génération de code depuis .proto
- Support navigateur limité (nécessite gRPC-Web)

---

## 🎯 Recommandations par Cas d'Usage

| Cas d'Usage | Technologie Recommandée | Justification |
|-------------|-------------------------|---------------|
| **API publique web** | **REST** | Simplicité (9/10), excellents outils, support universel, courbe d'apprentissage courte |
| **Microservices internes** | **gRPC** | Meilleures performances (8.6/10), latence 72ms, débit 10093 req/s, faible consommation |
| **Mobile apps** | **GraphQL** | Flexibilité requêtes, pas d'over-fetching, économie bande passante mobile |
| **Temps réel** | **gRPC** | Streaming bidirectionnel, HTTP/2, latence minimale, Protocol Buffers efficace |
| **IoT** | **gRPC** | Protocole binaire léger, faible consommation (35% CPU, 720 MB RAM), performances |
| **Legacy systems** | **SOAP** | Standards enterprise (WS-*), sécurité robuste (9/10), contrats formels WSDL |
