<style>
em {
    float: left;
    text-align: right;
    width: 100%;
}

img {
    width: 100%;
}

p {
    text-align: justify;
}
</style>

*Matthieu GUILLEMIN*

# Rapport de stage : <br/> Développement d’une plateforme web de gestion du risque naturel

![Logo IUT2 Grenoble](/images/logos.png)

> [Introduction](#introduction) <br/>
> [Présentation de l’entreprise et du stage](#présentation-de-lentreprise-et-du-stage) <br/>
> [Présentation de la réalisation](#présentation-de-la-réalisation) <br/>
> [Conclusion](#conclusion) <br/>
> [Bibliographie](#bibliographie) <br/>
> [Webographie](#webographie) <br/>
> [Glossaire](#glossaire) <br/>
> [Annexes](#annexes) <br/>

# Introduction

Pour valider son Diplôme Universitaire Technologique, chaque étudiant de deuxième année du département informatique doit effectuer un stage en entreprise d’une durée minimale de 10 semaines. Cela lui permet de prendre contact avec le monde professionnel et de valider les connaissances acquises lors de ses deux années d’études. C’est dans cette perspective que j’ai intégré HALIAS Technologies, situé à Meylan.

Le rapport que vous êtes en train de lire présente un échantillon du travail que j’ai pu effectuer pendant 10 semaines, mes recherches, mes réalisations, aboutis ou non, ainsi qu’une présentation succincte de l’entreprise et des technologies utilisées.

# Présentation de l’entreprise et du stage

## La présentation de l’entreprise
HALIAS Technologies a été fondée en 2006 par Laurent TESTARD et Jérôme MARTIN, experts en développement logiciel. Dès le départ, les deux hommes ont voulu mettre leurs compétences au service du secteur énergétique.

En 2020, ils décident d’élargir leur activité aux domaines de l’environnement et des géosciences. Leur objectif est de proposer des solutions informatiques efficientes permettant à leurs clients de gérer l’impact environnemental de leurs activités et de délivrer des indicateurs clés de performance écologique.

Aujourd’hui, l’entreprise compte 15 employés allant du profil de commercial à celui de développeur informatique et ingénieur.

Ce dévouement passionné à la cause environnementale et cette envie de proposer des solutions adaptées à la situation climatique actuelle et future m’ont donné envie d’effectuer mon stage chez HALIAS Technologies.

## La présentation du stage
J’ai intégré l’équipe informatique de HALIAS Technologies afin d’aider au développement d’un de leur projet. Celui-ci porte le nom OCIRN et se veut devenir une plateforme web de gestion du risque naturel. Il s’agit d’un projet de R&D (Recherche et Développement), il n’est donc pas réalisé à la demande d’un client et présente moins de contraintes de rendu qu’un projet classique. C’est l’entreprise elle-même qui fixe ses objectifs et les deadlines pour les atteindre.

OCIRN propose une solution à un problème courant, et encore non résolu, dans le monde de la géoscience : L’incompatibilité des différents logiciels de mesure géologique. L’idée derrière le projet est de proposer un langage universel permettant à ces outils de communiquer entre eux (cf. annexe 1). Ils peuvent être amenés à s’échanger des informations, comme des valeurs d’entrées et/ou des résultats de calcul. HALIAS, par le biais de OCIRN, veut proposer un moyen simple, rapide et efficace pour eux de le faire.

## Environnement de travail
Le stage se déroule en semi-présentiel. Je collabore sur OCIRN avec deux alternants en master MIAGE et Génie Informatique qui travaillent une grande partie du temps de chez eux car pas toujours disponibles pour venir sur place entre leurs périodes de cours à l’université. Ce contexte nous oblige à communiquer régulièrement par mail, pour les échanges formels, et sur Discord, pour ceux qui le sont moins. On organise des réunions Google Meet quand le besoin d’aborder un point plus en détails se fait sentir ou pour se fixer de nouveaux objectifs.

La suite Atlassian est utilisée par l’entreprise, j’ai donc dû me familiariser avec Jira, outil de suivi de projet, Confluence, logiciel de wiki, et Bitbucket qui est un outil de gestion de version au même titre que GitHub et/ou GitLab.

Les machines de chez Halias étant des PC Windows, utiliser WSL (Windows Subsystem for Linux), qui est une couche de compatibilité permettant d'exécuter des commandes Linux de manière native sur Windows, était donc quasiment indispensable pour travailler dans de bonnes conditions avec le PowerShell de Microsoft.

Enfin, pour ce qui est de l’éditeur de texte, j’utilise Visual Studio Code qui est très complet et qui simplifie la gestion de version en créant un pont vers BitBucket.

# Présentation de la réalisation

## Choix techniques
La partie frontend de OCIRN est entièrement développée en Vue.js, tandis que la partie backend est développée à l’aide de Python et son mini framework Flask.

Vue.js est un framework qui permet de construire des interfaces utilisateur. Il est lui-même bâti sur la base des standards HTML, CSS et JavaScript. Chaque fichier portant l’extension .vue est, dans la plupart des cas, composé de trois parties distinctes qui constituent le squelette d’un projet Vue : une partie HTML pour définir le contenu de la page, une partie JavaScript pour gérer les données affichées sur la page en question, et une partie CSS pour le style. Dans le cas de Vue, ces trois aspects sont réunis en un seul fichier. Cette façon peu courante de faire permet de compartimenter facilement l’application et ainsi de la rendre évolutive.

Halias utilise Node.js comme outil pour faire tourner le pan frontend de OCIRN. Il est soutenu par une communauté importante donc bien documenté et accessible.

Flask est un micro framework open-source de développement web en Python. Il est classé comme microframework car il est très léger. Effectivement, son noyau est simple mais extensible grâce à un grand nombre de classes et méthodes développées par ses utilisateurs. Il propose un serveur de développement qui, en mode debug,  se relance automatiquement lorsque des modifications sont apportées au code. C’est un atout de taille qui permet de développer de nouvelles fonctionnalités efficacement et qui rend la tâche des codeurs beaucoup plus agréable.

## Détail des tâches
Sur le modèle d’une API, chaque appel au service de OCIRN coûte un certain nombre de crédits à l’utilisateur. Mon rôle sur le projet est, dans un premier temps, de développer la partie gestion des crédits. Ce pan de la plateforme doit permettre, entre autres, à l’utilisateur de consulter l’évolution de ses comptes et l’historique de ses transactions (paiement et rechargement).

OCIRN est une plateforme de mise en relation de services, elle ne permet pas, à elle seule, d’effectuer le moindre calcul. Tout son fonctionnement repose alors sur les logiciels de calculs géologiques qui lui seront rattachés. Il est donc primordial que tous les utilisateurs soient en mesure d’ajouter et de supprimer des outils dans leurs listes d’OSP (OCIRN Service Providers), à la manière de plugins, afin de créer un écosystème d’outils qui corresponde le mieux à leurs besoins. Dans un second temps, je suis chargé de développer cette partie gestion des OSP . Je m’occuperai aussi bien du front-end que du backend.

## Description et explication du travail réalisé

### Maquettage
Le travail sur les pages de gestion des crédits et de gestion des OSP a commencé par une phase de maquettage. J’ai réalisé deux maquettes, une pour chaque page, en respectant la charte graphique de la plateforme et en adoptant un style épuré, étant donné qu’il s’agit d’une application à usage technique. Les deux maquettes ont été réalisées avec Figma (cf. annexe).

### Historique des transactions
Comme dit précédemment, la page de gestion des crédits est une page sur laquelle l’utilisateur doit pouvoir retrouver un historique des transactions qu’il a effectué jusqu’à présent sur la plateforme. Dès le début du développement, il a été jugé intéressant que la liste des transactions soit présentée sous deux formes différentes : dans un tableau et dans un graphique. Cela permet à l’utilisateur de se faire une idée précise de son activité sur OCIRN, avec une approche plus visuelle d’un côté (le graphique) et plus détaillée de l’autre (le tableau). 

 Avant de passer à l’implémentation de la page, il a fallu définir les attributs d’un objet de type Transaction pour pouvoir les stocker dans une relation SQL (cf. annexe). Cette relation, appelée history, représente la liste de toutes les transactions effectuées sur OCIRN, par tous les utilisateurs confondus.

Au niveau de la page, c’est à dire du fichier TokenConsumption.vue, les seules transactions qui doivent être récupérées sont celles de l’utilisateur connecté.  Ainsi, la requête de type GET qui remplit le tableau transactions au chargement de la page prend le nom de ce dernier en paramètre (username). Elle prend aussi l’année sélectionnée en paramètre (year) car il a été choisi de filtrer l’historique des transactions par année pour des raisons de lisibilité.

L’appel à la base de données est constitué de plusieurs couches : 
La requête depuis le frontend est faite sur le port 5010 où est en train de tourner le webservice de l’application. Dans ce webservice, le endpoint /history fait lui-même une requête de type GET vers l’orchestrateur (http://flask-orch:5000/history). Dans l’orchestrateur, la demande se précise en fonction des paramètres username et year, et les transactions de {username} faites en  {year} sont retournées sous forme de tableau. Cette liste d’objets de type Transaction est bien tirée de la relation history présente dans la base de données grâce au SELECT de la fonction get_history(mail, year) dans orch_utils.py. La liste transite ensuite d’un service à l’autre sous le format JSON jusqu’à arriver à son destinataire, la page TokenConsumption.vue. Une fois que la page a reçu les transactions, elle transmet la variable transactions, qui est un tableau, à ses deux vues components, transactionsDatatable et transactionsXYChart, ce qui va permettre de générer le tableau et le graphique. Ce processus de requête est réitéré à chaque fois que l’année sélectionnée est modifiée par l’utilisateur pour rendre la page dynamique. Cela est possible grâce à la propriété watch qui veille sur la valeur de yearSelected et relance une requête axios.get à chaque fois que celle-ci est modifiée.

#### Le tableau
L’historique des transactions sous forme de tableau est généré dans le fichier transactionsDatatable.vue. Vuetify, une bibliothèque d'interface utilisateur Vue qui propose des composants prêts à être utilisés, a considérablement simplifié l’implémentation de cet élément. Elle propose un composant nommé v-data-table qui permet  de créer un tableau de données de manière automatique en ne prenant que deux attributs : headers et items. Ces deux derniers attendent un Array pour valeur, sachant que l’attribut headers définit le nom des colonnes du tableau qui va être créé et que l’attribut items définit les données qui vont être rangées dans le tableau (ici des objets de type Transaction). Chaque ligne du tableau représente une transaction et les attributs de chaque transaction sont rangés dans la colonne correspondante grâce au headers, définit plus tôt, qui associe chaque colonne a un attribut donné. L’Array qui est passé comme valeur à l’attribut items est le tableau de transactions résultant de la requête backend faite par le composant vue père TokenCosumption.vue, filtré par ID. En effet, nous avons pris la décision d’ajouter un composant Vuetify v-text-field pour permettre aux utilisateurs de rechercher une transaction particulière en tapant son ID/numéro. Cette fonctionnalité prend tout son sens aux yeux de l’utilisateur quand celui-ci a accès au graphique d’évolution de son porte-monnaie virtuel.

#### Le graphique
Le graphique généré dans le fichier transactionsXYChart.vue représente exactement les mêmes données que le tableau du fichier transactionsDatatable.vue, à savoir les transactions de l’utilisateur connecté, mais sous une forme différente. Il met en lumière l’évolution du contenu du porte-monnaie au fil du temps en se basant sur le nombre de crédits qu’il restait à l’utilisateur en question après chaque transaction. Cette valeur est connue grâce à l’attribut nb_credits_after de l’objet Transaction. Le graphique présente moins d’informations, ce qui facilite la lecture de l’utilisateur, même s'il peut faire apparaître les détails d’une transaction en survolant le nœud du graphique qui la représente. On retrouve les mêmes détails dans le tableau, auquel on peut se référer facilement en regardant l’ID d’une transaction dans la toolbox qui apparaît lorsqu'on la survole dans le graphique. Le graphique a été généré avec la librairie amCharts.

# Conclusion
# Bibliographie
# Webographie
# Glossaire
# Annexes