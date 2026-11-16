# GuildOps Web — cadrage produit et pédagogique (M0)

**Commanditaire fictionnel :** Castor & Chimères, studio indépendant. **Client pédagogique :** CESI / INFAL105, MAALSI Nancy (30/11–02/12/2026). **Statut :** spécification, non implémentée.

## Pitch
Pour inaugurer le Grand Tournoi des Guildes, Castor & Chimères ouvre GuildOps Web. Les visiteurs créent un personnage, parcourent un village isométrique, parlent aux PNJ, réalisent de petites quêtes, récupèrent des objets et retrouvent leur progression après reconnexion. L'équipe d'hébergement doit préparer le lancement, absorber un afflux de joueurs, restaurer les données après incident et défendre sa stratégie devant le comité du studio.

La narration est ludique ; la technique ne l'est pas : disponibilité, coûts, sécurité, RPO/RTO et réversibilité doivent rester vérifiables.

## Périmètre jouable minimum (vertical slice)
1. **Navigateur Web**, sans installation client : village isométrique (2D isométrique ou 3D légère selon audit des dépôts existants ; ne pas rendre le moteur 3D bloquant).
2. **Déplacement** du personnage avec collisions simples et caméra adaptée.
3. **Trois PNJ** avec dialogues ; un PNJ offre une quête, un autre échange un objet, le troisième valide une étape.
4. **Trois missions courtes** : parler à un PNJ, collecter 3 ressources, livrer un objet. Début, progression et fin visibles.
5. **Inventaire** : acquisition/retrait/quantité ; une opération idempotente côté API pour éviter les doublons après retry.
6. **Progression persistante** : création d'un joueur de test, sauvegarde en PostgreSQL, déconnexion/reconnexion, reprise après redémarrage des conteneurs.
7. **Événement « Grand Tournoi »** déclenchant des requêtes de jeu reproductibles ; charge synthétique par scripts (pas besoin de centaines de vrais joueurs).
8. **Télémétrie** : health, readiness, métriques HTTP/latence/erreurs, identifiant de corrélation, traces applicatives utiles.
9. **États dégradés visibles** : service indisponible, action en attente, erreur explicite ; pas de succès fictif côté client.

## Hors périmètre avant Nancy
MMORPG complet, PvP, temps réel multi-joueurs sophistiqué, paiement, marketplace, monde ouvert, chat public, génération procédurale, mobile natif, orchestration avancée et sécurité de production complète. **Démo pédagogique, jamais données personnelles réelles.**

## Objectifs de réussite
- Parcours « nouveau joueur → mission → récompense → inventaire → reconnexion » automatisable de bout en bout.
- Une panne d'API entraîne un symptôme visible ; une réparation rétablit le parcours.
- Perte/recréation d'un conteneur **sans effacement du volume** conserve l'inventaire.
- Une expérience Litmus sur le service stateless permet de comparer mono-réplique/multi-répliques ; résultat mesuré, pas présumé.
- La restauration d'une sauvegarde teste effectivement RPO/RTO ; aucune promesse fondée sur un simple restart.
- Le même contrat applicatif reste utilisable avec Compose, Kubernetes local et un scénario cloud documenté.

## Organisation des versions
- **M0 :** documentation + contrats + énoncés.
- **M1 :** vertical slice jouable validée localement + persistance.
- **M2 :** déploiement Compose + observabilité + vérifications E2E.
- **M3 :** Kubernetes local + Litmus + campagne de chaos répétable.
- **M4 :** parcours cloud, FinOps, migration/réversibilité, supports de classe.

Chaque jalon doit être accepté par preuves : logs/commandes, tests exécutés, captures pertinentes, pas seulement des fichiers rédigés.

## Réutilisation
Auditer d'abord les dépôts GuildOps existants avant de réécrire un jeu. Ne pas modifier les dépôts d'origine sans cadrage spécifique. Conserver des interfaces d'adaptation pour ne pas coupler le gameplay aux environnements de TP.

## Références pédagogiques
- Fiche INFAL105 transmise pour Dijon, version récente évoquant 3 jours et 70 % d'exercices (à archiver et vérifier formellement avec Nancy).
- Ancienne fiche accessible sur Drive : version 25/10/2024, 50/50. **Ne pas présenter les deux versions comme identiques.**
- Support Google Slides historique et sauvegarde pré-refonte du 16/11/2026.
