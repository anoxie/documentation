
# Zones et workflow de travail :

-   Working Directory : c’est là où les fichiers sont stockés et modifiés, concrètement c’est le dossier de travail.
-   Staging area : une mystérieuse zone spéciale que l’on appelle l’index, ou la zone de staging
-   Git repository : stock les données de l’arborescence tel qu’elles étaient lors du dernier commit
  

## Cloner et créer un repository git

```bash
git init
```

Créer un repository git.

```bash
git clone
```
Cloner un repository à partir d’une adresse de repository
  
## Qu’est-ce qu’un bon commit :
Il doit être atomique, il ne doit concerner qu’une seule chose, être le plus petit possible en restant cohérent. Il est possible d’atomiser les commits, même si l’un a effectué plusieurs modifications, pour faire un commit pour chaque modification, par exemple l’implémentation d’un feature sera un commit, la correction de fautes d’orthographe en sera un autre, il est même possible dans la zone de staging de choisir des parties de fichiers à joindre à un commit.

## Un commit étape par étape :

![](https://lh3.googleusercontent.com/dCBMYYifVd7GOI67ke4ssSvqYqAIohiSB2X6R0cFihbc6KkxvlrwhAQfhnnSjDrOz0rh1zupowzf2Ads0Il4VS8vZLjMaJ26CYB4Z64LTCiFxaCyOOmzo6t8eflZ52k7hGc-twbw)

```bash
git add <nom_de_fichier>
```
pour copier un fichier ou un répertoire dans la zone de staging.
```bash
git add .
```
permet d’ajouter à l’index de git tous les fichiers du répertoire courant
  
```bash
git commit -m “message”
```
pour sauvegarder la zone de staging dans le dépôt git et créer un nouveau commit
  
```bash
git commit -a -m “message”
```
permet de faire git add et git commit -m “message” en une seule fois, cette commande est possible du moment que les fichiers modifiés ont déjà été ajouté à l’index

```bash
git commit --amend -m “votre nouveau message”  
```
permet de modifier le message du dernier commit, ne fonctionne que si le commit n’a pas été push
  
```bash
git stash
```
permet de mettre en attente des modifications en cours sur une branche en particulier, à fin d’effectuer par exemple d’autres modifications plus urgentes, sans créer de commits superflus
  
```bash
git stash pop
```
permet de récupérer les changements précédemment mis en stash sur la branch /!\ pop vide le stash pour conserver les modifications dans le stach, il faut faire :
  
```bash
git stash apply
```
permet de récupérer ce qui est stocké dans le stash sans le supprimer.
  
```bash
git push origin master
```
pour envoyer les commits vers un dépôt centralisé
  
```bash
git pull origin master
```
pour récupérer les modifications apportées sur le dépôts centralisé
  
```bash
git blame <nom_du_fichier.extension>
```
liste toutes les modifications effectuées sur un fichier avec le début de la référence du commit correspondant, le nom et la date de la publication
  
```bash
git show <début_du_sha>
```
Permet de voir le message relatif à un commit
  
```bash
git revert <SHA1_commit>
```
va créer un commit qui fait l’inverse du commit en question, ce qui va créer un nouveau commit.
  
```bash
git reset
```
pour copier un fichier du dépôt git vers la zone de staging

```bash
git checkout
```
pour copier un fichier de la zone de staging vers la zone de workflow et donc supprimer les modifications en cours
```bash
git diff
```
pour visualiser les modifications entre les répertoires de travail et la zone de staging
  
```bash
git diff --cached ou git diff --staged
```
pour visualiser les modifications entre la zone de staging et le dernier commit
```bash
git status
```
pour visualiser dans quelle zone de git sont les fichiers
```bash
git log
```
pour visualiser l’historique du projet
# Qu’est-ce qu’une branch ?
Une branche n’est qu’une étiquette qui pointe vers un commit. Identifier par une référence sha1. La branch master étant par défaut la branche principale. Head est une référence spéciale qui pointe vers le commit qui sera le parent du prochain commit, typiquement indique la branch dans laquelle on souhaite travailler.

Chaque branche permet de créer un flow de développement parallèle
## Manipuler les branches :
```bash
git branch
```
permet de lister les branches
```bash
git branch <nom_de_branch>
```
permet de créer, lister et supprimer des branches
```bash
git branch <nom_de_branch> <réf_de_commit>
```
permet de créer une branche à partir de la référence d’un commit
```bash
git checkout <nom_de_branch>
```
permet de déplacer la référence HEAD, notamment vers une nouvelle branche et donc de changer de branch
```bash
git checkout -b <nom_de_branch>
```
permet de cumuler les deux git branch et git checkout
## Fusionner les branches :
Si les branches, permettent de travailler en parallèle sur différentes parties du projet, on finit bien par fusionner ces branches pour créer un seul projet. Lors d’une fusion ou merge, git va intégrer toutes les modifications contenues sur chaque branche dans une seule et même arborescence.
## Merge étape par étape :
-   on se place sur la branche qui va “recevoir” les modifications de l’autre branche avec ``` git checkout <nom_de_branch>```
-   on fusionne avec ```git merge <nom_de_branch_a_fusionner>```
-   une fois fusionné on supprime la branch devenue inutile avec ``` git branch -d test```    

## Résoudre les conflits de fusion :
Des conflits peuvent survenir durant la fusion obligeant à y intervenir manuellement, ce sera le cas par exemple si différentes branches apportent des modifications différentes au même endroit dans le même fichier.

En cas de conflit, git interrompt le merge et insère des marqueurs dans les fichiers conflictuels. Il faut éditer ces fichiers manuellement (ou à l’aide d’une interface spécifique), avant de poursuivre la fusion.

```bash
git help merge
```
Pour le protocole précis de résolution de conflits.  
  
Quand un conflit apparaît, git crée un fichier avec l’extension .md, qu’il convient d’éditer, pour choisir le code à conserver. Une fois sauvegardé il suffit de lancer un git commit, qui se chargera de détecter la résolution de conflit et générera un message automatique.

## L’état DETACHED HEAD
```bash
git reflog
```
permet de suivre les déplacements de la référence HEAD, et de retrouver les références de commit qui n’ont pas encore été intégré à une branch.

## Comprendre la commande checkout

Il y a deux façons d’utiliser la commande git checkout :

-   sans spécifier de fichier ou de répertoire, git va simplement déplacer la référence HEAD, et mettre à jour les deux arborescences de la zone de staging et du Working Directory, ce qui permet de revenir à une version antérieure. Si des modifications sont en cours, elles ne seront pas écrasées, et Git tentera de fusionner la version courante du fichier avec celle correspondant à la nouvelle position de HEAD.    
-   en spécifiant un dossier ou un répertoire, restaure les fichiers passé à la commande, en écrasant les versions du working directory par ceux en staging.

## Commandes checkout utiles :
```bash
git checkout .
```
Supprime toutes les modifications qui ne sont pas dans le staging

```bash
git checkout <nom_de_fichier/nom_de_repertoire>
```
Supprime toutes les modifications de fichiers contenues dans le fichier ou le répertoire
```bash
git checkout <branch> <nom_de_fichier/nom_de_repertoire>
```
Récupère dans le rép. de travail le fichier ou répertoire tel qu’il qu’il était dans la branch

## Comprendre la commande git reset

Reset à un fonctionnement similaire à checkout, sauf qu’il déplace la référence de la branch courante en plus de déplacer la référence HEAD.

On peut préciser la zone d’action de reset comme suit :
```bash
git reset <branch> --soft
```
Déplace HEAD
```bash
git reset <branch> --mixed
```
Déplace HEAD, et met à jour le staging, c’est le mode par défaut
```bash
git reset <branch> --hard
```
Déplace HEAD, met à jour le staging et le répertoire de travail

Avec l’option --hard, le répertoire de travail est écrasé, même s’il y a des modifications en cours.
```bash
git reset HEAD^
```
Permet de supprimer le dernier commit
```bash
git reset HEAD^^
```
permet de supprimer les 2 derniers commits
```bash
git reset HEAD~<number>
```
permet de revenir de <number> commit en arrière.

En précisant un chemin de fichier, la référence HEAD, n’est pas déplacé, les modifications seront limitées au chemin de fichier spécifié.

## Visualiser l’historique
```bash
git log -p
```
permet de voir le log avec les

## Ignorer des fichiers .gitignore

Pour des raisons de sécurité, il est primordiale d’éviter certain fichiers dans git, tels que :
-   tout les fichiers de configuration (config, database, env.,...)
-   les fichiers et dossiers temporaires (tmp, temps/…)
-   les fichiers inutiles comme ceux créés par votre IDE ou votre OS
    
NE JAMAIS VERSIONNER DE VARIABLE DE CONFIGURATIONS tel que mot de passes, clé secrètes,...

# Sources :

[https://www.miximum.fr/blog/enfin-comprendre-git/](https://www.miximum.fr/blog/enfin-comprendre-git/)

  

[https://openclassrooms.com/fr/courses/2342361-gerez-votre-code-avec-git-et-github](https://openclassrooms.com/fr/courses/2342361-gerez-votre-code-avec-git-et-github)

  

[https://openclassrooms.com/fr/courses/1233741-gerez-vos-codes-source-avec-git](https://openclassrooms.com/fr/courses/1233741-gerez-vos-codes-source-avec-git)

  

contribuer à des project openSource sur github

[https://openclassrooms.com/fr/courses/2342361-gerez-votre-code-avec-git-et-github/2433731-contribuez-a-des-projets-open-source](https://openclassrooms.com/fr/courses/2342361-gerez-votre-code-avec-git-et-github/2433731-contribuez-a-des-projets-open-source)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2OTgwODQ4MDAsMTkwODM2NjI5NSwtMz
g3NTc2OTg0XX0=
-->