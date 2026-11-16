# Architecture cible et contrats techniques

**Statut :** conception / décisions proposées. N'implique aucun test exécuté.

## Composants
```text
Browser (client isométrique)
       |
  HTTPS / reverse proxy
       |
  Game API stateless (quêtes, inventaire, progression)
       |              \
 PostgreSQL          /metrics + /healthz + /readyz
       |
 sauvegarde / restauration contrôlées
```

Le rendu, les déplacements locaux et l'UI sont exécutés dans le navigateur. **L'état durable est côté serveur** : missions terminées, objets, quantités, progression. Ne pas persister uniquement dans localStorage ni faire confiance aux valeurs envoyées par le navigateur.

## Contrats fonctionnels suggérés
| Verbe / chemin | Fonction | Résultat attendu |
|---|---|---|
| POST /api/players | Crée un joueur anonyme de laboratoire | player_id + jeton de test |
| GET /api/players/me | Profil et position de départ | joueur courant |
| GET /api/world | Village, PNJ, objets et quêtes | référentiel versionné |
| GET /api/quests | Missions et états de progression | vue serveur |
| POST /api/quests/{id}/accept | Accepte une mission | état idempotent |
| POST /api/interactions | Interaction PNJ/objet | résultat validé par règles |
| GET /api/inventory | Inventaire persistant | items/quantités |
| GET /healthz | Vie du processus | HTTP 200 si processus vivant |
| GET /readyz | Prêt à accepter des requêtes | 200/503 selon dépendances |
| GET /metrics | Compteurs/latences/erreurs | format documenté |
 
**Sémantique :** toute écriture sensible doit fournir une `Idempotency-Key` et respecter les transactions. Le modèle de jeton de laboratoire ne doit pas être présenté comme une authentification de production. Les API sont des propositions et peuvent être adaptées au moteur GuildOps réellement réutilisé.

## Modèle de données minimal
```text
player(id, created_at, display_name)
quest(id, title, definition_json, version)
player_quest(player_id, quest_id, status, progress, updated_at)
item(id, name, stackable)
inventory(player_id, item_id, quantity, updated_at)
interaction(idempotency_key, player_id, result_json, created_at)
```
Contraintes d'unicité sur `(player_id, quest_id)`, `(player_id, item_id)` et `(player_id, idempotency_key)`. Sauvegardes testées avec restauration **dans un environnement isolé**.

## Déploiement
- **Compose :** web, API, PostgreSQL et volume nommé persistant ; DB non exposée publiquement ; healthchecks.
- **Kubernetes :** front/API, Services, Deployment, ConfigMap/Secret ; persistance DB traitée explicitement (PVC ou DB externe). Un cluster mono-nœud ne valide pas la tolérance à la panne de nœud.
- **Cloud :** services équivalents, droits minimaux, suppression automatique après laboratoire ; ne pas promettre EKS/RDS si AWS Academy bloque les permissions.
- **Observabilité :** collecteur de métriques simple et client sonde HTTP, avec trace du timestamp, code et latence. Différencier indisponibilité de l'API, de la base et du client.

## Non-fonctionnel : hypothèses de jeu
2 000 joueurs inscrits, 20 req/s en régime courant, 200 req/s lors du tournoi, cible de disponibilité 99,9 %, RPO 15 min, RTO 2 h et budget fictif 1 500 €/mois. **Ce sont des exigences initiales à challenger**, pas une capacité démontrée. Mesurer avant toute conclusion.

## ADR à prendre
ADR-001 : réutiliser/adaptater le client GuildOps existant vs moteur indépendant.
ADR-002 : frontière client/serveur et persistance.
ADR-003 : DB locale/PVC/DB managée selon environnement.
ADR-004 : stratégie de test résilience, sauvegarde, reprise, migration.
ADR-005 : accès cloud/fallback et contrôle des coûts.

## Qualité et sécurité
Tests E2E navigateur (une quête complète), API (idempotence et invariants d'inventaire), déploiement Compose, persistance et restore, scripts charge reproductibles. Données fictives, aucun secret dans le dépôt, image épinglée et scans dès que possible, chaos limité aux namespaces de laboratoire.
