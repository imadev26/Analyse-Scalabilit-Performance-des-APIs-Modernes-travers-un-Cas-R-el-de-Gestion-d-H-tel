# Instructions de Test - APIs Hôtel

## 🎯 Vue d'ensemble

Ce guide détaille comment exécuter les tests de performance pour comparer REST, SOAP, GraphQL et gRPC.

---

## 📋 Préparation

### 1. Vérifier les prérequis

```bash
# Docker
docker --version

# Java
java -version

# Maven
mvn -version

# Node.js (pour GraphQL)
node --version
npm --version
```

### 2. Cloner et démarrer les services

```bash
# REST Service (Spring Boot)
cd rest-api
mvn spring-boot:run

# SOAP Service (Spring Boot)
cd soap-api
mvn spring-boot:run

# GraphQL Service (Apollo Server)
cd graphql-api
npm install
npm start

# gRPC Service (Java)
cd grpc-api
mvn spring-boot:run
```

### 3. Vérifier que tous les services répondent

```bash
# REST
curl http://localhost:8080/api/reservations

# SOAP
curl http://localhost:8081/soap/reservation?wsdl

# GraphQL
curl http://localhost:4000/graphql

# gRPC
# Utiliser BloomRPC sur localhost:9090
```

---

## 🧪 Tests avec JMeter

### Installation JMeter

```bash
# Télécharger
wget https://downloads.apache.org/jmeter/binaries/apache-jmeter-5.5.zip
unzip apache-jmeter-5.5.zip
cd apache-jmeter-5.5/bin
```

### Exécuter les tests

```bash
# REST
./jmeter -n -t ../test-plans/REST_Load_Test.jmx -l results/rest-results.jtl

# SOAP
./jmeter -n -t ../test-plans/SOAP_Load_Test.jmx -l results/soap-results.jtl

# GraphQL
./jmeter -n -t ../test-plans/GraphQL_Load_Test.jmx -l results/graphql-results.jtl

# gRPC
./jmeter -n -t ../test-plans/gRPC_Load_Test.jmx -l results/grpc-results.jtl
```

### Générer les rapports

```bash
./jmeter -g results/rest-results.jtl -o reports/rest-report
./jmeter -g results/soap-results.jtl -o reports/soap-report
./jmeter -g results/graphql-results.jtl -o reports/graphql-report
./jmeter -g results/grpc-results.jtl -o reports/grpc-report
```

---

## 🔥 Tests avec k6

### Installation k6

```bash
# Windows
choco install k6

# Linux
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys C5AD17C747E3415A3642D57D77C6C491D6AC1D69
echo "deb https://dl.k6.io/deb stable main" | sudo tee /etc/apt/sources.list.d/k6.list
sudo apt-get update
sudo apt-get install k6

# Mac
brew install k6
```

### Exécuter les tests

```bash
# REST
k6 run scripts/k6-rest-test.js

# GraphQL
k6 run scripts/k6-graphql-test.js

# Avec options
k6 run --vus 100 --duration 30s scripts/k6-rest-test.js
```

---

## 🐝 Tests avec Locust

### Installation Locust

```bash
pip install locust
```

### Exécuter les tests

```bash
# Mode interface
locust -f scripts/locust-rest.py --host=http://localhost:8080

# Mode headless
locust -f scripts/locust-rest.py --host=http://localhost:8080 \
  --users 100 --spawn-rate 10 --run-time 5m --headless
```

---

## ⚡ Tests avec Gatling

### Installation Gatling

```bash
# Télécharger
wget https://repo1.maven.org/maven2/io/gatling/highcharts/gatling-charts-highcharts-bundle/3.9.0/gatling-charts-highcharts-bundle-3.9.0-bundle.zip
unzip gatling-charts-highcharts-bundle-3.9.0-bundle.zip
```

### Exécuter les tests

```bash
cd gatling-charts-highcharts-bundle-3.9.0
./bin/gatling.sh
# Sélectionner le scénario REST/SOAP/GraphQL/gRPC
```

---

## 📊 Monitoring avec Prometheus + Grafana

### Démarrer stack monitoring

```bash
docker-compose -f docker-compose-monitoring.yml up -d
```

### Accéder aux interfaces

- **Prometheus:** http://localhost:9090
- **Grafana:** http://localhost:3000 (admin/admin)

### Importer dashboards

1. Aller dans Grafana
2. Import → Upload JSON
3. Sélectionner les dashboards dans `dashboards/`

---

## 📈 Collecter les Métriques

### Métriques Système

```bash
# CPU
docker stats --no-stream

# Mémoire
free -m

# Network
iftop
```

### Métriques Application

```bash
# Spring Boot Actuator (REST/SOAP)
curl http://localhost:8080/actuator/metrics

# GraphQL métriques
curl http://localhost:4000/metrics

# gRPC métriques
curl http://localhost:9090/metrics
```

---

## 🎯 Scénarios de Test Standard

### Scénario 1: Montée en charge progressive

```
10 users → 5 min
100 users → 5 min
500 users → 5 min
1000 users → 5 min
```

### Scénario 2: Spike test

```
0 → 1000 users en 1 min
Maintenir 5 min
1000 → 0 users en 1 min
```

### Scénario 3: Endurance

```
100 users constants
Durée: 1 heure
```

### Scénario 4: Stress test

```
Augmentation continue jusqu'à échec
Identifier le point de rupture
```

---

## 📝 Remplir les Tableaux

Après chaque test:

1. Ouvrir `docs/tableaux/RESULTATS.md`
2. Remplir:
   - Latence moyenne (ms)
   - Débit (req/s)
   - CPU (%)
   - Mémoire (MB)
3. Prendre des screenshots des dashboards
4. Noter les observations

---

## 🐛 Dépannage

### Service ne démarre pas

```bash
# Vérifier les ports
netstat -an | grep "8080\|8081\|4000\|9090"

# Voir les logs
docker logs <container-name>
```

### Métriques manquantes

```bash
# Vérifier Prometheus targets
curl http://localhost:9090/api/v1/targets

# Redémarrer Prometheus
docker restart prometheus
```

### Tests trop lents

```bash
# Réduire le nombre d'utilisateurs
# Augmenter la durée de ramp-up
# Vérifier les ressources système
```

---

**Bon tests !** 🚀
