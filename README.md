L'objectif de ce dépôt est de contenir un certain nombre de recette `ansible` qui me sont nécessaires, d'une manière ou d'une autre dans ma vie.

# Exécution d'une recette
**Se fait obligatoirement en tant que `root`.**

## Optionnel
```
export http_proxy=8<...>8
export https_proxy=${http_proxy}
```

## Obligatoire
  * Déployer la recette sur la machine concernée par le déploiement (`recipe.yml`) dans la suite du document.
  * Déployer les éventuelles autorités de certification internes sur la machine concernée par le déploiement. Le dossier sera référencé dans la suite par `ac_path`.
  * Installer les paquets nécessaires : 
    * `ansible`
    * `python2-passlib` (ne vient pas avec sous ArchLinux).
  * Aller à l'endroit où la recette a été copiée et lancer le déploiement.
```
ansible-playbook recipe.yml
```

### Matrice des variables
Variable | Utilité
---------|---------
`user` | Nom du compte utilisateur à créer / modifier pour pouvoir développer correctement.
`password` | Mot de passe du compte.
`vb_version` | Version de l'hyperviseur VirtualBox. Utilisé pour installer les VirtualBoxAdditions.
`ac_path` | Emplacement sur la machine virtuelle dans lequel on a copié les autorités de certification internes.


# Présentation des recettes
## `archlinux_srv.yml`
Contient la recette de l'installation de mon p'tit serveur à moi. :-)

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
  * Il est possible que certains modules PHP ne soient pas installés. Pour ce faire, me fournir la liste.
