# Ordre de mission — Lancement du Grand Tournoi

**Émetteur :** Castor & Chimères, studio indépendant. **Destinataires :** Guilde des Hébergeurs (votre équipe).

GuildOps est un jeu Web : les joueurs explorent un village isométrique, rencontrent des PNJ, réalisent des quêtes et conservent leur inventaire. Le Grand Tournoi approche. Le studio souhaite diffuser le jeu sans que les aventuriers perdent leurs récompenses au premier redémarrage.

### Extrait de la réunion client
> « On veut 100 % de disponibilité, sauf pendant la maintenance ; moins de 1 500 € par mois ; aucun verrouillage fournisseur ; et un retour en service avant la prochaine annonce du Grand Tournoi. Le cloud sera forcément plus économique, non ? »

Vous devez **qualifier** ces exigences. Ne supposez pas qu'elles sont toutes cohérentes. Les contraintes suivantes sont **hypothèses de travail à challenger** :
- 2 000 comptes de jeu fictifs, 20 req/s normalement, 200 req/s pendant le tournoi ;
- cible initiale 99,9 % mensuelle, RPO 15 min, RTO 2 h ;
- trois composants : interface Web, API de jeu, PostgreSQL ;
- données du laboratoire : pseudonymes et inventaires fictifs uniquement ;
- fonctionnement sur poste local, cluster Kubernetes de laboratoire et éventuellement cloud.

### Les quatre stratégies à étudier
1. **La cave du château :** serveurs gérés par le studio (on-premise).
2. **L'auberge des machines :** VPS / machines virtuelles hébergées.
3. **La Compagnie des Nuages :** IaaS public avec services managés.
4. **L'atelier des runes :** PaaS ou hébergement applicatif managé.

Ces noms sont narratifs. Dans les schémas et livrables, utilisez **aussi** la terminologie réelle.

### Règles de preuve
Chaque conclusion doit reposer sur des mesures, calculs ou hypothèses déclarées. Une capture d'écran d'un jeu qui fonctionne **n'est pas** une preuve de haute disponibilité. De même, le redémarrage d'un Pod ne prouve pas la préservation des données.

### Livraison finale
Dossier d'architecture, matrice pondérée, estimation TCO sur 36 mois, résultats de tests, risques résiduels, plan de migration/réversibilité et note de décision ADR présentée au Conseil de Castor & Chimères.
