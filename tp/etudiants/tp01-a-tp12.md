# Cahier étudiant — Les douze missions de GuildOps

**Version de cadrage M0 :** les tâches reposant sur une application exécutable seront activées une fois la vertical slice et le laboratoire validés. Les durées sont indicatives, non garanties.

## TP01 — Le client impossible (30–45 min)
Le studio exige 100 % de disponibilité mais accepte les maintenances planifiées, refuse les coûts variables et souhaite changer de fournisseur à tout moment.
- **Socle :** classer les besoins en fonctionnels / non fonctionnels, impératifs / souhaitables, explicites / ambigus. Formuler au moins 8 questions au client.
- **Approfondissement :** préciser les unités/périodes de disponibilité, RPO, RTO, budget et tests d'acceptation.
- **Défi :** négocier une cible cohérente sous budget contraint.
- **Livrable :** `requirements.md` avec priorité, ambiguïtés, hypothèses et critères vérifiables.

## TP02 — Devine l'architecture (25–35 min)
Quatre propositions sont reçues : serveur local, VPS, cloud IaaS, PaaS.
- **Socle :** schématiser les composants et identifier les responsabilités de chaque option.
- **Approfondissement :** distinguer critères éliminatoires et critères pondérés.
- **Défi :** démontrer comment un changement de poids modifie la recommandation.
- **Livrable :** matrice comparative argumentée.

## TP03 — Ouverture du premier guichet (45–60 min)
Le studio livre GuildOps Web et la configuration Compose de départ.
- **Socle :** démarrer Web/API/PostgreSQL, créer un joueur et terminer une quête.
- **Approfondissement :** expliquer les ports exposés, isoler la base, vérifier health/readiness.
- **Défi :** proposer une procédure de retour à zéro déterministe.
- **Preuve :** parcours E2E horodaté, état Compose, schéma et logs significatifs.

## TP04 — Le gobelin a débranché l'API (40–60 min)
En pleine quête, l'API s'arrête ; le responsable produit exige que le joueur retrouve son inventaire.
- **Socle :** observer la panne, redémarrer et rejouer une action.
- **Approfondissement :** recréer **le conteneur** PostgreSQL sans supprimer son volume, vérifier un item avant/après ; distinguer panne du processus, crash du stockage et restauration.
- **Défi :** effectuer un dump/restauration **sur une instance de test isolée**, sans détruire l'environnement d'un autre groupe.
- **Preuve :** chronologie des symptômes, commandes, inventaire avant/après et limites.

## TP05 — 30 000 orcs devant le portail (30–45 min)
Le Grand Tournoi génère des rafales de requêtes de jeu.
- **Socle :** calculer pics de requêtes, charges de connexion et stockage à partir d'hypothèses fournies.
- **Approfondissement :** interpréter latence p95, cache, saturation et capacité des services.
- **Défi :** définir un benchmark juste et reproductible.
- **Preuve :** table de calcul + dimensionnement justifié.

## TP06 — Faille dimensionnelle (60–75 min)
Sur Kubernetes local, Litmus déclenche la suppression contrôlée d'un Pod de l'API.
- **Socle :** formuler l'hypothèse, lancer une sonde, injecter la panne sur une seule réplique et consigner les erreurs.
- **Approfondissement :** comparer avec 2 répliques et vérifier readiness / service routing.
- **Défi :** étudier un incident réseau **uniquement** dans l'environnement isolé autorisé.
- **Preuve :** résultats de mesures et conclusion limitée à la topologie testée. **Ne pas** prétendre avoir validé une panne de nœud.

## TP07 — Le budget d'erreur (30–45 min)
Les affiches du tournoi annoncent 99,9 % mensuel.
- **Socle :** calculer le budget mensuel d'indisponibilité en précisant le mois et la période.
- **Approfondissement :** relier échecs observés, taux de requêtes réussies, SLI et SLO.
- **Défi :** discuter quand le taux de succès ne suffit pas pour qualifier une expérience utilisateur.
- **Preuve :** calculs et définition explicite du SLI.

## TP08 — Départ pour la Compagnie des Nuages (60–75 min)
Le studio souhaite comparer le local à un environnement hébergé.
- **Socle :** déployer le front et/ou API dans l'environnement cloud autorisé **ou** suivre le fallback local prévu ; documenter la topologie.
- **Approfondissement :** responsabilités IAM, réseau, stockage, journalisation.
- **Défi :** comparer VM / service de conteneurs managé / PaaS.
- **Preuve :** capture technique, schéma, liste de ressources et procédure de suppression. **N'utiliser que les services autorisés par l'enseignant.**

## TP09 — Qui paie les dégâts du dragon ? (25–35 min)
Un incident révèle une base publique et un accès administrateur excessif.
- **Socle :** classer fournisseur/client/partagé pour 10 contrôles.
- **Approfondissement :** choisir les 5 corrections les plus utiles au regard des risques.
- **Défi :** faire varier les responsabilités pour PaaS et IaaS.
- **Preuve :** tableau risques et contrôles.

## TP10 — La facture du Grand Trésorier (60–75 min)
Le studio reçoit trois devis aux structures de coûts différentes.
- **Socle :** estimer un TCO de 36 mois incluant calcul, stockage, réseau, opérations et sauvegardes.
- **Approfondissement :** sensibilité au trafic sortant et au niveau de disponibilité.
- **Défi :** démontrer pourquoi le scénario apparemment moins cher peut devenir plus coûteux.
- **Preuve :** tableur et hypothèses versionnées ; aucun tarif public supposé intemporel.

## TP11 — La Compagnie des Nuages ferme boutique (45–60 min)
Il faut partir sans perdre les guildes ni les inventaires.
- **Socle :** définir export, transfert, cutover, validation et rollback ; identifier les dépendances.
- **Approfondissement :** restaurer une copie PostgreSQL dans un environnement isolé et comparer des totaux d'inventaire.
- **Défi :** proposer une stratégie réduisant l'interruption.
- **Preuve :** plan de réversibilité avec critères go/no-go.

## TP12 — Le Conseil de Castor & Chimères (75–90 min)
Chaque groupe défend sa stratégie devant trésorier, responsable de la sécurité et directeur du jeu.
- **Socle :** matrice pondérée, contraintes éliminatoires, ADR, schéma et démonstration d'une preuve.
- **Approfondissement :** carte événement inconnue (hausse de trafic, audit, fournisseur indisponible).
- **Défi :** recalculer la décision en temps limité et expliciter le risque résiduel.
- **Preuve :** soutenance et dossier final, avec désaccords possibles assumés.

## Barème de retour pédagogique indicatif (non noté automatiquement)
Pour chaque mission : preuve fonctionnelle et reproductible, interprétation correcte, choix justifié, limites explicites. Valoriser la conclusion honnête « notre architecture n'atteint pas la cible » lorsqu'elle est étayée.
