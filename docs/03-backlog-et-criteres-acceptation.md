# Backlog de réalisation et critères d'acceptation

**Priorité Nancy, 30 novembre 2026.** Ce document distingue *cadré* et *implémenté*. Aucune fonctionnalité n'est déclarée livrée sur la seule base d'un énoncé.

## P0 — sécuriser le cours
| ID | Travail | Définition de terminé |
|---|---|---|
| P0-01 | Auditer `GuildOps`, `GuildOps-etudiant`, `GuildOps-formateur` et identifier rendu/client réutilisable | ADR de réutilisation avec preuves de build, licences et compatibilité navigateur |
| P0-02 | Vertical slice jouable et persistance | Parcours création → quête → récompense → inventaire → reconnexion vérifié |
| P0-03 | Compose reproductible | `up`, `health`, `test`, `down` exécutés avec succès sur une machine témoin |
| P0-04 | Jeu de données déterministe + reset | Réinitialisation reproductible sans accès à données réelles |
| P0-05 | TP01–TP05 utilisables | Énoncés autonomes, fichiers de départ, preuves attendues, temps de résolution mesurés |
| P0-06 | Corrigés formateur sécurisés | Hors dépôt public ou politique d'accès explicitement acceptée |
| P0-07 | Soumission administrative CESI | Versions étudiant/formateur, fiche préparation et date validées |

## P1 — différencier les hébergements
| ID | Travail | Définition de terminé |
|---|---|---|
| P1-01 | Déploiement Kubernetes local | Le même parcours de quête est vérifié dans un namespace isolé |
| P1-02 | Sonde et métriques | Requêtes réussies/échouées, latence et timestamps exportables |
| P1-03 | Litmus `pod-delete` | Expérience répétée, mesures conservées, remise à zéro éprouvée |
| P1-04 | Cloud et fallback | Scénario autorisé sur classe AWS Academy ou alternative réellement testée |
| P1-05 | TCO 36 mois | Jeu d'hypothèses et tableau comparatif contrôlés par exemples |
| P1-06 | Réversibilité PostgreSQL | Export/import, vérification intégrité et plan rollback démontrés |

## P2 — qualité et extensions
- Fautes réseau et stockage isolées.
- Cartes événements multiples.
- Comparaison environnementale raisonnée.
- Tableau de bord de santé in-game et comparaison avant/après.
- Challenge expert benchmark.

## Risques / arbitrages
1. **Délai :** 2 semaines pour Nancy. Ne pas sacrifier les preuves à une vue 3D ambitieuse.
2. **Réutilisation GuildOps :** inconnu tant que les projets existants ne sont pas audités.
3. **Cloud :** permissions AWS Academy variables ; ne pas dépendre d'EKS ou de services coûteux.
4. **Données :** toutes fictives ; aucune destruction de volumes ou de namespaces non dédiés.
5. **Diffusion :** dépôt formateur actuellement public ; ne pas déposer de corrigés secrets.
6. **Référentiel :** divergence fiche Drive 2024 et fiche plus récente transmise par courriel ; reconfirmer version pour Nancy.
7. **Pédagogie :** 12 TP = catalogue ; ajuster nombre effectivement parcouru après répétition.

## Validation
Un *go* à la diffusion étudiant nécessite des preuves exécutées, pas uniquement code statiquement valide ni documents rédigés. Inscrire les résultats et les blocages dans un journal de validation daté.
