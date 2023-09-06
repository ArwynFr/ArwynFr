# Registre d'architecture

Ce document compile l'ensemble des décisions d'architecture applicables à mon compte GitHub.

## 2023-01 Créer un registre d'architecture
* Date : 06/09/2023
* Statut : Applicable

### Quoi

Je mets en place un registre d'architecture pour mon compte GitHub. Ce journal compile l'ensemble des décisions d'architecture applicables à ce compte GitHub. Il est constitué sous la forme d'un document Markdown qui sera abondé régulièrement au fil des décisions prises.

La modification d'une entrée approuvée n'est possible qu'en ajoutant des informations. En revanche des informations qui se sont révélées fausses peuvent être barrées, mais il est alors recommandé de justifier cette opération. Une entrée peut être modifiée librement tant qu'elle est en état brouillon. Elle peut également être dépréciée, soit pour la remplacer, soit pour en annuler les effets.

Le format des entrées est le suivant :
```md
## [Année]-[Chrono] [Titre de la décision]
* Date : [Date de mise à jour]
* Statut : [Statut de l'entrée]

### Quoi
[Description de la décision applicable]

### Pourquoi
[Justification de la décision]
```

Remarques:
* Le titre de la décision utilise un verbe à l'infitif.
* Le statut peut être : Brouillon, Applicable, Déprécié

### Pourquoi
Il arrive régulièrement que je m'interroge sur des décisions structurantes passées (comme par exemple monorepo vs multirepo). Je ne me rappelle pas toujours des décisions prises des mois précédents, surtout si je n'ai pas pratiqué les points associés régulièrement depuis. L'utilisation d'un registre d'architecture (Architecture Decision Log) permet de résoudre ce problème parce qu'il permet de journaliser les décisions architecturales, et donc de retrouver à la fois le *quoi* et le *pourquoi* de ces décisions, même longtemps après.

NOTE: Cela n'empêche pas d'interroger régulièrement la pertinence de la décision dans le temps.

## 2023-02 Utiliser une approche multirepo
* Date : 06/09/2023
* Statut : Applicable

### Quoi

Je mets en place une structure de repository de type multirepo, c'est à dire que les ressources d'orchestration (docker stack ou chart helms) sont versionnés avec les sources des applications.

### Pourquoi

Lors de l'utilisation d'un orchestrateur (K8S ou Docker Swarm), il est  possible de centraliser les ressources de déploiement dans un repository d'infrastructure (monorepo), ou de conserver ces ressources avec les sources applicatives (multirepo).

* L'utilisation d'un monorepo est plutôt pensée dans le contexte d'une organisation *dev versus ops*. Elle permet une ségrégation des droits et une gestion centralisée qui se focalise sur l'historisation et la cohérence technique. L'historique de chaque application est mélangé et le déploiement d'une mise à jour nécesssite souvent 2 PR.

* L'utilisation d'un multirepo est plutôt pensée dans le contexte d'une organisation *devops*. Elle permet une mise à jour de l'ensemble de l'application et son infrastructure en un seul geste et s'appuie sur une infrastructure "as-a-service". Il existe un risque d'incohérence technique entre plusieurs repository et il est plus compliqué d'avoir un historique des changements faits sur la plateforme au sens large.

S'agissant de dépôts personnels, il est plus cohérent de partir sur une approche multirepo. Pour maintenir la cohérence du SI, je peux utiliser des outils comme renovate et dependabot afin de maintenir l'ensemble des dépendances alignées sur la dernière version (edging).
