# Parcours pédagogique — INFAL105 / GuildOps

**3 jours de 7 h effectives** ; les temps indiqués sont des objectifs prudents et révisables après répétition. Viser au moins 70 % d'activités incluant résolution, restitution et analyse, conformément à la fiche la plus récente évoquée ; reconfirmer la version référentiel de Nancy.

## Jour 1 — Le studio doit ouvrir son jeu
| TP | Mission | Socle | Approfondissement | Livrable |
|---|---|---|---|---|
| TP01 | Cadrer les besoins contradictoires du studio | Identifier contraintes, ambiguïtés, priorités | Négocier 99,9 %, RPO/RTO et budget | Tableau exigences + questions |
| TP02 | Comparer cave du château / VPS / cloud / PaaS | 4 architectures et responsabilités | Critères éliminatoires et sensibilité | Tableau comparatif |
| TP03 | Déployer GuildOps sous Compose | Jouer une quête en local | Exposition réseau, secrets, healthcheck | Application + preuve E2E |
| TP04 | « Le gobelin a débranché l'API » | Panne API et restart | Persistance inventaire et sauvegarde de DB | Journal d'incident |
| TP05 | Dimensionner le Grand Tournoi | Estimer req/s, stockage, bande passante | Identifier goulots, burst, marges | Hypothèses + calculs |

## Jour 2 — Les promesses se mesurent
| TP | Mission | Socle | Approfondissement | Livrable |
|---|---|---|---|---|
| TP06 | Litmus : une faille dévore un Pod | `pod-delete`, sonde et relevés | Comparer 1 et 2+ répliques ; réseau/disque en bonus | Graphique ou journal d'erreurs |
| TP07 | « Vous aviez promis 99,9 % » | Budget d'erreur et SLO | RPO/RTO vs mesures observées | Rapport de disponibilité |
| TP08 | Externaliser vers un hébergeur | Déployer parcours minimal en cloud ou fallback | IAM, stockage, coût et architecture | Déploiement + schéma |
| TP09 | « Qui paie les dégâts du dragon ? » | Matrice responsabilité partagée | Prioriser 5 risques à budget constant | Matrice RACI/risques |

## Jour 3 — Le Grand Conseil tranche
| TP | Mission | Socle | Approfondissement | Livrable |
|---|---|---|---|---|
| TP10 | Facture du Grand Trésorier | TCO 36 mois sur 3 options | Trafic sortant, sauvegardes et sensibilité | Tableur + hypothèses |
| TP11 | Quitter la Compagnie des Nuages | Plan de migration, cutover et rollback | Test réel export/import PostgreSQL | Plan réversibilité + preuve |
| TP12 | Conseil de Castor & Chimères | ADR + matrice pondérée | Cartes événements et objections | Soutenance et décision |

## Défis de réserve
A. Benchmark trompeur (cache, percentiles, protocole) ; B. Audit sécurité surprise ; C. Hébergement et impact environnemental ; D. Changement de tarification ou de clauses contractuelles.

## Règle commune à tous les TP
**Trois niveaux :** socle vérifiable en 20–40 min ; approfondissement raisonné ; défi expert non bloquant. Un script ne doit pas faire l'essentiel du raisonnement à la place des étudiants. Les expériences manipulant les données opèrent sur des données de démo réinitialisables.

## Matrice de compétences synthétique
| Objectif INFAL105 | Preuves |
|---|---|
| Qualifier un besoin d'hébergement | TP01, TP05 |
| Connaître les modèles / IaaS/PaaS/SaaS / responsabilité | TP02, TP08, TP09 |
| Construire une matrice pondérée | TP02, TP10, TP12 |
| Dimensionnement et sûreté | TP04, TP05, TP06, TP07 |
| Mettre en place une infrastructure | TP03, TP06, TP08 |
| Pratiquer des solutions cloud | TP08 et démonstrations |
| Coût, conformité, environnement | TP09, TP10, défis |
| Migration et réversibilité | TP11, TP12 |
| Défendre une décision | TP12 |

## Organisation
Groupes de 2 ou 3 ; une même identité fictive par groupe ; remise sous forme d'un dossier Git contenant `architecture.md`, `decision.md`, `measurements.csv`, `costs.csv`, `rollback.md` et captures/logs minimaux. Ne pas exiger de données ou identifiants personnels.
