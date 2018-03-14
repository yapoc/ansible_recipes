L'objectif de ce dépôt est de contenir un certain nombre de recette `ansible` qui me sont nécessaires, d'une manière ou d'une autre dans ma vie.

# Exécution d'une recette
```
ansible-playbook <RECETTE>.yml
```

# Présentation des recettes
## `centos_dev.yml`
Installation d'un socle qui permet de développer sur une VM `CentOS` toute fraîchement installée.
### Problèmes & améliorations possibles
  * Récupération du RPM `elasticsearch` : Je devrais normalement faire comme suit, mais ça pose des problèmes de prise en compte de la variable d'environnement `${http_proxy}`.

```
  - name: Récupération du RPM elasticsearch
    get_url:
      url: https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-6.2.2.rpm
      dest: /tmp/elasticsearch.rpm
      mode: 0644
```

  * J'ai l'impression d'avoir un vague problème lors de l'acceptation de la licence et de la création de l'utilisateur. Je comprends pas pourquoi `CentOS` est aussi névrosé mais on va dire que c'est trop spécifique à la distribution pour que je me prenne la tête dessus pour le moment.
