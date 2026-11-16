# MMO GuildOps — laboratoire formateur INFAL105

**Castor & Chimères · CESI MAALSI · Stratégie d'hébergement applicatif**

Ce dépôt héberge le cadrage et, à terme, les corrigés et infrastructures du **laboratoire GuildOps Web** dédié à INFAL105. L'objectif est d'héberger un **jeu navigateur réellement jouable** (village isométrique, missions, inventaire, progression persistante) sur plusieurs architectures, puis de mesurer leur comportement sous charge et sous incidents.

> État initial : dépôt de cadrage. Aucun jeu complet, déploiement cloud ou laboratoire Litmus n'est encore déclaré fonctionnel.

Les propositions détaillées seront soumises par pull request. Les supports et secrets exclusivement formateur doivent rester hors du dépôt public tant que leur mode de diffusion n'est pas défini.

## Contraintes structurantes

- Trois journées, Nancy : **30 novembre au 2 décembre 2026**.
- Priorité pédagogique : **choix argumenté d'hébergement**, pas apprentissage exhaustif du développement de jeux ni de Kubernetes.
- **12 TP principaux + défis de prolongement**, avec preuve observable et critères de réussite.
- Expériences de chaos **Litmus** sur Kubernetes, et pannes contrôlées Docker Compose au préalable.
- Déploiement cloud seulement après validation des accès ; alternative locale obligatoire.
- Séparer **sources étudiantes** et **corrections/consignes privées formateur**.

Voir la PR de cadrage pour les documents proposés.
