# TP5 — Traitement de Flux avec Kafka Streams
Ce projet regroupe 3 exercices pratiques de traitement de données en temps réel avec Apache Kafka Streams (Java 17, Spring Boot 3.2, Kafka 3.9).

🚀 Démarrage rapide (Infrastructure)
Le projet utilise un broker Kafka unique configuré en mode KRaft via Docker.

# Lancer Kafka et Zookeeper
>docker-compose up -d

# 🛠️ Aperçu des Exercices
## Exercice 1 — Text Cleaner
Une application Kafka Streams pure qui nettoie et trie des messages texte bruts.

Pipeline : text-input ➡️ Nettoyage (trim, toUpperCase) ➡️ Filtrage (isValid)

Routage : Les messages valides vont vers text-clean, les messages invalides (mots interdits comme SPAM, HACK, XXX ou texte > 100 caractères) sont rejetés dans text-dead-letter.

## Exercice 2 — Weather Analyzer
Analyse de données météo au format CSV avec agrégation et exposition de métriques.

Pipeline : Reçoit le flux weather-data (Format: station,temp,humidité) ➡️ Filtre les températures > 30°C ➡️ Convertit les °C en °F ➡️ Calcule les moyennes en temps réel par station (via un State Store RocksDB) ➡️ Envoie le résultat dans station-averages.

Bonus : Les moyennes calculées sont exposées en temps réel pour Prometheus sur http://localhost:1234/metrics.

## Exercice 3 — Click Stream Analytics
Une architecture complète en 3 micro-services Spring Boot pour compter les clics des utilisateurs :

Producer App (:8082) : Une interface web Thymeleaf avec un bouton qui envoie un événement "click" à chaque interaction dans le topic clicks.

Streams App : Regroupe les clics par utilisateur, incrémente le compteur via RocksDB et publie les résultats mis à jour toutes les secondes dans click-counts.

Consumer App (:8083) : Écoute click-counts via un @KafkaListener et expose le score final via une API REST (GET /clicks/count).

## Flux de l'exercice 3 :

[Navigateur / Bouton] ➡️ [Producer :8082] ➡️ Topic 'clicks' ➡️ [Streams App] ➡️ Topic 'click-counts' ➡️ [Consumer :8083] ➡️ API REST
## 🗂️ Structure du Projet
exercice1/TextCleanerApp.java : Application de nettoyage de texte autonome.

exercice2/WeatherAnalyzerApp.java : Application d'analyse météo + Prometheus.

exercice3/ :

producer/ : Application Spring Boot Web (Interface de clic).

streams/ : Traitement et calcul des scores Kafka Streams.

consumer/ : API REST de restitution des résultats.

/screenshots : Captures d'écran de validation des tests.