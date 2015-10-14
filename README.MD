# DeportedCommentary
Est un programme de commentaire centralis� d�centralis� :3

En gros c'est un programme un peu dans l'id�e de Isso (python), hashover (PHP), Juvia (Ruby?) et probablement d'autres.
Discourse et Vanilla Forum permettent d'�tre utilis� comme syst�me de commentaire par exemple.

Ces programmes existent pour faire concurrence � Disqus
afin de pouvoir avoir un syst�me de commentaire "simple" en rassemblant la gestions de ses commentaires venant de plusieurs sites sur un seul. �a permet d'avoir la main sur son propre service plut�t que de devoir faire une confiance aveugle en une entreprise qui est la pour ce faire des sous, et pour �a elle vends votre vie priv�.

Ce genre de syst�me permet par exemple d'avoir des commentaires sur des sites statique, ou sur des sites ou un syst�me de commentaire n'est pas pr�sent ou ne vous convenant pas.

# Pourquoi avoir fait ma propre alternative en Python sachant que Isso existe d�j� ?
J'aime coder, j'ai commenc� � apprendre le python assez r�cemment, et je rien n'est plus formateur pour apprendre un nouveau langage de ce lancer dans des choses un peu complexe des le d�but pour apprendre sur le tas.

De plus cr�er mon propre programme me permet d'en faire ce que je veux, et le rendre modulable plus facilement pour mes besoins (il est bien plus simple de comprendre un programme qu'on a fait sois m�me.

# Pr�requis
 - Python 3.5 >=
 - pip
 - avoir un site sur lequel int�grer le programme :3
 - le reste pip s'en occupera

# Installation
```
git clone 'adresse'
cd 'adresse'
pip -r requirements.txt
cp config.example.json config.json
```

# Configuration
 - �ditez le fichier config.json

## Explication du fichier de config
 - host : choisissez l'adresse ip ou DNS sur lequel est lanc� votre programme (default = "localhost")
 - port : le port sur lequel ce lance votre programme (default = 8080)
 - sitename : nom de votre site (utilis� pour la page d�accueil) assez optionnel
 - pageadmin : chemin d'acces � l'interface d'administration / elle n'est pas encore mise en place.
 - theme : nom de votre th�me (dans le dossier view) (default=default ; c'est un th�me material design, assez sobre)
 - Allow-Origin : tableau de valeur. s'ajoutera aux headers de vos pages
   - Access-Control-Allow-Origin: valeur une
   - Access-Control-Allow-Origin: valeur 2
   - �a permet d'autoriser les requ�tes ajax venant de toutes(*) adresses ext�rieurs, ou seulement quelques unes, vous pouvez vouloir que votre site ne soit accessible que de vos adresses et pas par tout le monde, c'est votre choix.
 - akismet-key : votre cl� akismet, sinon l'antispam ne fonctionnera pas
 
## Explication du theme
  - Copiez collez les dossier (theme) default des dossiers view et static
  - Choisissez un nom pour la copie, les noms doivent correspondre
  - /!\ le path dans l'url ferra correspondre '/static/votrefichier' au chemin 'static/votretheme/votrefichier'
  - personnalisez le
  - �ditez le fichier de config pour le faire correspondre � votre theme (juste le nom du dossier, pas de chemin.)
 
# Lancement
```python(3?) main.py```

## Int�gration
vous r�cupererez le code en vous connectant � la page d'acceuil de votre programme python via l'exterieur.

exemple : http(s)://votre.domaine:votreport/ cela ressemblera �    

	<div id="DPCommentary"></div>
	<script type="text/javascript" src="http://localhost:8080/integrate"></script>
	
Mais il ne faut pas que ce soit en localhost

# NotaBene
Une limitation du protocole XmlHttpRequest fait qu'il est impossible de r�cup�rer le contenue d'une adresse avec un protocole diff�rent

Si vous remarquez que le theme par d�faut fait des requetes vers l'exterieur de votre programme c'est que j'ai oubli� d'importer localement les assets, merci de me le signaler. apr�s si vous voulez utiliser votre propre th�me avec CDN c'est votre choix :3

# Librairie et ressources utilis�
 - [bottle](http://bottlepy.org/docs/dev/index.html) (c'est le serveur web)
 - [peewee](http://docs.peewee-orm.com/en/latest/index.html) ORM pour SQL
 - [SQLite](https://www.sqlite.org/) �a me semble suffisant pour gerer une base de commentaires
 - [validate_email](https://pypi.python.org/pypi/validate_email) pour valider les email fournie. Le champ est optionel donc pas de raison de mal le remplir
 - lib python standard (nottament urllib.parse et json)
 - [akismet python](https://pypi.python.org/pypi/akismet/0.2.0) pass� � la moulitte de 2to3 et quelques modification d'encodage, va faloir que je lui propose au mec qui a fait la lib
 - [Awesome Font](https://fortawesome.github.io/Font-Awesome/) pour mon th�me material, j'ai un peu honte, toute une police pour faire juste l'icone d'envois de commentaire :3
 - [Roboto Font](https://www.google.com/fonts/specimen/Roboto)
 - [Material Design](https://www.google.com/design/spec/material-design/introduction.html) de moi, librement inspir� des specifications de google

# Remerciements
 - [Geluchat](https://www.dailysecurity.fr/) pour m'avoir motiver � me lancer dans le python
 - [Sam et max](http://sametmax.com/) le 3/4 de ce que je connais en python c'est gr�ce � leur site, et j'ai choisi mes libs avec [cet article](http://sametmax.com/sept-petites-libs-qui-changent-la-vie-dun-dev-python/)
 
# Feature future
 - [ ] captcha (optionel)
 - [ ] panel admin (mdp hash� dans le fichier de config)
 - [ ] choix entre ReStructuredText et Markdown, par commentaire (BDD broken)
 - [ ] fil RSS
 - [ ] Authentification user optionelle (BDD broken)
 - [ ] Mail -> Admin (new commentaire), Mail -> user (dans son fil)