# Campagne Litmus — « La faille dimensionnelle »

**Objectif :** distinguer disponibilité observée, redémarrage automatisé, persistance et reprise après désastre. **Statut : protocole à implémenter et tester** ; ne garantit aucune compatibilité/version Litmus avant validation.

## Séquence proposée
0. **Prérequis :** cluster local Kind/Minikube dédié ou partagé avec namespaces isolés, installation Litmus validée par le formateur, API GuildOps en état connu, données fictives, permission réduite.
1. **État initial :** API à 1 réplica, sonde HTTP testant une vraie action de lecture du jeu (éviter un unique healthcheck).
2. **Hypothèse :** « La suppression du Pod ne provoque aucune erreur visible. » Définir durée de mesure, fréquence de sonde, critère de réussite.
3. **Injection :** expérience Litmus de type `pod-delete` ciblée explicitement sur le deployment API et dans le namespace du groupe.
4. **Observations :** nombre de requêtes, codes 2xx/5xx, latence p95, durée sans réponse, temps de retour au service ; comparer prédiction/résultat.
5. **Itération :** 2 réplicas, readiness probe, nouvelle injection et nouvelle mesure à conditions comparables.
6. **Débrief :** démontrer pourquoi 2 réplicas ne protègent ni une DB mono-instance ni un cluster mono-nœud contre toutes les pannes.

## Expériences complémentaires facultatives
- **container-kill :** comportement du redémarrage d'un conteneur.
- **pod-network-loss :** rupture réseau entre API et base si permissions et fault image compatibles.
- **disk-fill :** stockage **éphémère et uniquement isolé**, quota strict ; ne pas viser les volumes hébergeant la base persistante.

Les noms exacts, APIs et ressources des expériences doivent être confirmés contre la version de Litmus retenue. Ne jamais lancer de chaos cluster-wide, ne pas injecter d'incident sur le poste de l'enseignant ou un système non dédié.

## Mesure minimale
```csv
timestamp_utc,scenario,replicas,status_code,latency_ms,success
2026-11-30T10:00:00Z,baseline,1,200,45,true
```
Ligne illustrative **fictive**, pas un résultat d'essai. L'outil de sonde doit écrire une ligne par requête, y compris les échecs de connexion (status_code vide, success=false).

## Préparation formateur
- Tester le chart `vendored-litmus` dans un namespace dédié et épingler les images.
- Vérifier l'accès aux registry et la résolution du problème antérieur de `ImagePullBackOff`.
- Fournir une commande **start**, **probe**, **fault**, **stop**, **reset** vérifiée.
- Vérifier service account/RBAC et empêcher le ciblage d'autres namespaces.
- Disposer d'une alternative manuelle Kubernetes (`kubectl delete pod`) si Litmus échoue ; expliquer alors que le TP n'a pas démontré le fonctionnement de Litmus.
- En cas d'échec de la plateforme, fournir des séries de mesures d'exemple **clairement étiquetées synthétiques** pour l'analyse.

## Questions de restitution
- Votre SLI décrit-il une action réellement utile au joueur ?
- Quel nombre de requêtes a échoué ? Quelle période ?
- Le service a-t-il continué à répondre pendant la panne ? Quelles limites ?
- Les objets de l'inventaire ont-ils été préservés ? Qu'avez-vous effectivement testé ?
- Le RTO/RPO est-il vérifié ? (Réponse attendue : non, pas par un simple pod-delete.)

## Critères d'acceptation du laboratoire
1. Le ciblage d'une autre application est refusé par construction et RBAC.
2. L'expérience s'exécute puis s'arrête de manière prévisible.
3. Les métriques couvrent le baseline et la faute.
4. Une procédure de remise à zéro rétablit le jeu.
5. Aucune faute destructive sur données persistantes ou système hôte.
