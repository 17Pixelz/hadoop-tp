# Madoop et MapReduce TP

Dans ce TP on va utiliser Hadoop à partir d’une image Docker, l’image qu’on va utiliser est préconfigurée par [Kai LIU](https://github.com/kiwenlau), selon l’architecture suivante :

![Architecture](https://i.ibb.co/Y8y3BSx/hadoop-cluster-docker.png)

> Remarque : vous devez avoir docker installer chez vous.

## Instalation
### Téléchargement de l'images docker:
Commençant par exécuter la commande suivante dans le terminal :
```
docker pull kiwenlau/hadoop:1.0
```
### Création des contenaires
Maintenant l'image est bien téléchargée, on doit créer les trois contenaires (le master et les deux slaves).
D'abord on crée un réseau où les contenaires se relie:
```
docker network create --driver=bridge hadoop
```

Ensuite on crée et lance les trois contenaires:
```
docker run -itd --net=hadoop -p 50070:50070 -p 8088:8088 --name hadoop-master --hostname hadoop-master kiwenlau/hadoop:1.0
docker run -itd --net=hadoop --name hadoop-slave1 --hostname hadoop-slave1 kiwenlau/hadoop:1.0
docker run -itd --net=hadoop --name hadoop-slave2 --hostname hadoop-slave2 kiwenlau/hadoop:1.0
```

Et on accède au master:
```
docker exec -it hadoop-master bash
```

Enfin on execute le script `start-hadoop.sh` pour lancer hadoop et yarn
```
./start-hadoop.sh
```

## Exemple d'utilisation
Comme exemple on veut utiliser WordCount qui permet de calculer le nombre d'occurences de chaque mot dans des fichiers précis.

Un script existe déja dans la machine `run-wordcount.sh`, il crée deux fichier avec un contenu tres simple, et il execute un programe en java qui utilise hadoop et mapreduce pour calculer le nombre d'occurences de chaque mot dans les deux fichiers créés.

On peut l'executer par:
```
./run-wordcount.sh
```

Et le resultat doit être :
```
input file1.txt:
Hello Hadoop

input file2.txt:
Hello Docker

wordcount output:
Docker    1
Hadoop    1
Hello    2
```


### Devoir
Votre part de ce TP après l'installation bien sur, et de créer un projet utilisant votre langauge préférée qui permer de calculer le nombre d'occurences d'un mot précis en donnant un fichier texte comme entrer.







