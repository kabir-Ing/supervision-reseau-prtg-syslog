# Supervision d'un parc informatique avec PRTG et Visual Syslog

![Supervision](https://img.shields.io/badge/Supervision-PRTG-0078D4?style=flat-square) ![Journalisation](https://img.shields.io/badge/Logs-Syslog-0891B2?style=flat-square) ![OS](https://img.shields.io/badge/Syst%C3%A8mes-Windows_Server-23395B?style=flat-square)


## 1. Résumé du projet

Ce projet porte sur le déploiement, dans un environnement de machines Windows virtualisées, d'une solution de **supervision de postes et de services** avec **PRTG Network Monitor** et d'une solution de **centralisation/consultation des événements Windows** utilisant **EVTSYS** et **Visual Syslog**.

L'objectif est  d'obtenir une meilleure visibilité sur l'état des équipements (disponibilité, interfaces, charge processeur) et de consulter des journaux système depuis un outil centralisé.

## 2. Problématique

La maintenance d'un parc informatique nécessite de détecter les indisponibilités et de disposer d'informations techniques pour analyser les dysfonctionnements. Une surveillance dispersée et l'absence de consultation centralisée des événements compliquent ces opérations.

## 3. Environnement et technologies documentés

| Élément | Utilisation dans le projet |
|---|---|
| **PRTG Network Monitor** | Supervision des équipements, capteurs et tickets |
| **SNMP** | Remontée d'informations des machines supervisées |
| **Windows Server** | Machine virtuelle utilisée pour héberger PRTG |
| **Machine cliente Windows** | Équipement supervisé et source d'événements |
| **Visual Syslog** | Réception et consultation des messages Syslog |
| **EVTSYS** | Transmission d'événements Windows au collecteur Syslog |
| **Syslog** | Transport/centralisation des événements |

**Architecture logique  :**

```text
[Machine cliente Windows] -- SNMP --> [PRTG sur Windows Server]
          |
          +-- EVTSYS / Syslog --> [Visual Syslog]
```


## 4. Démarche de réalisation

### Étape 1 — Préparation de l'environnement
- Utilisation de machines Windows virtualisées : une machine cliente et une machine Windows Server pour PRTG.
- Préparation de la supervision SNMP sur le poste cible.

### Étape 2 — Installation et configuration de PRTG
- Installation de PRTG sur l'environnement serveur.
- Accès à l'interface d'administration web.
- Création d'utilisateurs et de groupes.
- Ajout d'un équipement à superviser et renseignement des paramètres SNMP.

### Étape 3 — Mise en place des capteurs et tickets
- Ajout de capteurs pour observer la disponibilité, les interfaces réseau et la charge processeur.
- Consultation des valeurs remontées dans l'interface PRTG.
- Création d'un ticket dans l'outil.

### Étape 4 — Centralisation des journaux
- Installation de Visual Syslog.
- Installation/configuration d'EVTSYS sur Windows et démarrage de son service.
- Consultation dans Visual Syslog des messages reçus.

## 5. Résultats observables dans le manuel

- **PRTG :** des captures montrent l'équipement supervisé, plusieurs capteurs et une vue détaillée de disponibilité système.
- **Tickets :** le processus de création et un ticket enregistré sont illustrés.
- **EVTSYS :** une capture de terminal montre le démarrage du service.
- **Visual Syslog :** une capture présente une liste de messages d'événements reçus.

Ces éléments démontrent une mise en place fonctionnelle illustrée. **Le rapport ne contient pas de mesures avant/après, de taux de disponibilité mesurés dans la durée, ni de validation formelle du déclenchement des alertes : aucun de ces résultats n'est revendiqué ici.**

## 6. Compétences mises en pratique

- Mise en place d'un environnement Windows virtualisé.
- Configuration élémentaire de la supervision réseau avec **PRTG** et **SNMP**.
- Gestion d'équipements, de capteurs, d'utilisateurs et de tickets PRTG.
- Installation d'une chaîne de journalisation **EVTSYS → Visual Syslog**.
- Lecture de tableaux de bord et de journaux techniques.
- Documentation d'un déploiement informatique.

## 7. Limites et pistes d'amélioration

- Préciser les versions logicielles, la topologie et les flux réseau utilisés.
- Vérifier les paramètres de sécurité SNMP/Syslog avant toute reproduction.
- Ajouter, si un nouveau laboratoire est réalisé, des tests documentés d'alertes, une chronologie et des critères d'acceptation.
- Distinguer supervision de disponibilité et détection d'incidents de cybersécurité : **PRTG + Visual Syslog ne constituent pas à eux seuls un SOC ou un SIEM complet**.

## 8. Documentation et preuves

Le manuel d'origine comprend des captures d'installation, de configuration des comptes et capteurs, de création de tickets et de consultation des logs.

**Avant publication :** placer les captures sélectionnées et anonymisées dans `captures/`, le PDF original relu dans `documentation/`, puis remplacer les références ci-dessous par de vrais liens :

- [ ] Vue d'ensemble PRTG et capteurs
- [ ] Détail de disponibilité système
- [ ] Configuration et état du service EVTSYS
- [ ] Journaux reçus dans Visual Syslog
- [ ] Rapport PDF expurgé des informations sensibles

## 9. Ce que j'en retiens

Ce projet m'a permis de pratiquer deux approches complémentaires : **surveiller le fonctionnement d'équipements** avec des capteurs et **centraliser des événements système** pour faciliter leur consultation. La prochaine amélioration consiste à rendre les tests et résultats plus systématiques et reproductibles.

---

*Projet restructuré à partir de mon manuel de déploiement antérieur. Le dépôt décrit les éléments documentés, sans inventer de métriques ou de tests supplémentaires.*
