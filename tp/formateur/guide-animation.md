# Guide d'animation formateur — éléments génériques

> **AVERTISSEMENT : dépôt public.** Aucun corrigé évaluatif confidentiel, jeton de classe, clé cloud, scénario secret de soutenance ou données personnelles ne doivent être committés ici. Ce document expose les *critères d'observation* publics. Les corrections détaillées seront conservées dans un espace privé avant publication éventuelle.

## Cadence
- Commencer chaque mission par une courte annonce du « studio ».
- Laisser les groupes formuler une hypothèse avant les manipulations.
- Exiger une preuve **et** une limite de cette preuve.
- Garder des prolongements pour les groupes rapides ; le bonus ne doit pas rendre le TP suivant inaccessible.
- Éviter de transformer le cours en débogage de frameworks GameDev.

## Points d'observation par TP
| TP | Critère à faire émerger | Contresens fréquent |
|---|---|---|
| 01 | Hypothèses, critères mesurables et arbitrages | 100 % disponible est une exigence univoque |
| 02 | Coûts, responsabilité, compétences, réversibilité | « Cloud = moins cher » toujours |
| 03 | Portail utilisable et données stockées serveur | Une page Web ouverte valide tout le système |
| 04 | Différence redémarrage, volume persistant, backup | Le volume est une sauvegarde |
| 05 | Dimensionnement et marge sur hypothèses | Une moyenne suffit pour absorber le pic |
| 06 | Comparaison quantitative sous panne contrôlée | Kubernetes = haute disponibilité automatique |
| 07 | Définition du SLI et de la fenêtre temporelle | 99,9 % signifie zéro erreur |
| 08 | Architecture et responsabilités de services réellement autorisés | Le fournisseur protège toutes les couches |
| 09 | Mitigations proportionnées aux risques | Une conformité déclarative suffit |
| 10 | TCO complet et sensibilité | Prix de VM = coût global |
| 11 | Cutover, intégrité, rollback | Exporter les données suffit à migrer |
| 12 | Décision défendable et limites | La somme pondérée est une vérité absolue |

## Soutenance
Rôles du Conseil :
- Trésorier : budget initial, coût variable, exploitation.
- Responsable sécurité : accès, résilience, données, conformité.
- Directrice du jeu : expérience utilisateur, lancement du tournoi, délais.

Une bonne réponse peut rejeter la demande initiale si l'équipe rend la contradiction explicite et propose des options.

## État de préparation avant diffusion
- [ ] Jeu jouable de bout en bout sur navigateur.
- [ ] Tests automatiques de quête, inventaire et reconnexion.
- [ ] Déploiement Compose testé réellement.
- [ ] Base et sauvegarde/restauration testées.
- [ ] Cluster local et expériences Litmus testés.
- [ ] Contournement validé si AWS Academy indisponible.
- [ ] Sources étudiants publiées séparément.
- [ ] Accès/quotas/destroy cloud contrôlés.
- [ ] Supports envoyés à CESI selon échéance locale.
