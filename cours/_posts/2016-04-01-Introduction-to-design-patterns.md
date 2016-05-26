---
layout: post
title: An introduction to design patterns in Java
tags:
- java
- design pattern
description: An introduction to design patterns in Java
image:
  feature: knap.jpg
  credit: Wikipedia
  creditlink: https://commons.wikimedia.org/wiki/File:%D0%9A%D0%BE%D1%82%D0%B5%D0%BB%D1%8C%D0%BD%D0%B8%D0%BA%D0%BE%D0%B2._%D0%98%D1%81%D1%82%D0%BE%D1%80%D0%B8%D1%8F_%D0%BE%D0%B4%D0%BD%D0%BE%D0%B3%D0%BE_%D0%B8%D0%B7%D0%BE%D0%B1%D1%80%D0%B5%D1%82%D0%B5%D0%BD%D0%B8%D1%8F_(1938)._%D1%81%D1%82%D1%80._55.jpg
excerpt: Design patterns are solution proven to be effective for known problems.
---
{% include _toc.html %}

Les patrons de conceptions sont des solutions éfficaces à des problêmes connus. Dans ce cours, nous verrons un rappel sur les notions de programmation orientée objets, puis, nous étudierons les principaux patrons de conceptions.

# Rappel sur l'héritage

## Héritage

Le premier exercice de cette démonstration consiste à implémenter -- en utilisant l'héritage et le mot clef "extends" -- l'architecture suivante :  

![Héritage Java](/images/Heritage.png "Héritage Java")

Un animal dispose de la méthode manger(); qui ne prends pas d'arguments. Cette méthode est surchargée pour afficher :

{% highlight js %}
//Pour les Herbivores
Je suis un Herbivore; je mange des végétaux.
//Pour les Carnivores
Je suis un Carnivore; je mange de la viande.
//Pour les Omnivores
Je suis un Omnivore; je mange de tout.
{% endhighlight %}

## Classes Abstraites

([rappel](http://perso.telecom-paristech.fr/~hudry/coursJava/abstraction/))

Une méthode abstraite est signalée par le modificateur abstract placé au début de son en-tête. Une telle méthode n'a alors que son prototype, c'est-à-dire son type de retour suivi, de son nom, suivi de la liste de ses paramètres entre des parenthèses, suivi d'un point-virgule. Une méthode abstraite ne peut pas être déclarée static ou private ou final. Dès qu'une classe contient une méthode abstraite, elle doit elle aussi être déclarée abstraite, avec le modificateur abstract placé au début de son en-tête . Une classe abstraite ne peut pas être instanciée. Il faudra l'étendre et définir toutes les méthodes abstraites qu'elle contient pour pouvoir l'utiliser. Une sous-classe d'une classe abstraite sera encore abstraite si elle ne définit pas toutes les méthodes abstraites dont elle hérite.

Quel est l'intérêt d'avoir une classe animal qui dispose d'une méthode manger(); vide ? En effet, nous n'avons pas défini de comportement spécifique pour animal. De plus nous n'allons probablement jamais instancier d'animaux générique. Nous allons toujours avoir besoin d'un animal d'une catégorie spécifique. Pourquoi ne pas transformer la classe Animal en une classe abstraite ?

### Exercice 1

Implémeter cette architecture avec une classe Animal abstraite; puis lancer le programme.

## Interfaces

([rappel](http://imss-www.upmf-grenoble.fr/prevert/Prog/Java/CoursJava/interface.html))

Une interface définit un comportement (d’une classe) qui doit être implémenté par une classe, sans implémenter ce comportement. C’est un ensemble de méthodes abstraites, et de constantes. Certaines interfaces ( Cloneable, Serializable, …) sont dites interfaces de «balisage» : elle n’imposent pas la définition d’une méthode, mais indiquent que les objets qui les implémentent ont certaines propriétés. Les différences entre les interfaces et les classes abstraites :

*   Une interface n’implémente aucune méthode.
*   Une classe, ou une classe abstraite peut implémenter plusieurs interfaces, mais n’a qu’une super classe, alors qu’une interface peut dériver de plusieurs autres interfaces.
*   Des classes non liées hiérarchiquement peuvent implémenter la même interface

Notre classe abstraite animal avait manger(); définie en tant qu'abstract; cependant elle n'implémente aucune autre fonctions. Il sera alors peut être plus pertinent de modifier animal en Interface.

### Exercice 2

Modifier l'architecture afin qu’Animal soit une Interface; puis relancer le programme. Vous devez obtenir les mêmes résultats que lors de l'exercice 1.

### Exercice 3

Proposer et coder une architecture cohérente et pertinente pour représenter le schéma suivant :

![Modélisation Java](http://static.commentcamarche.net/www.commentcamarche.net/pictures/java-images-arbo.gif "Modélisation Java")

Les flèches pleines sont à titre d'indications. Pour rappel une flèche pleine en UML représente une relation d'héritage.

Votre implémentation devra aussi disposer d'énumérateur(s) permettant d'instancier facilement les différents animaux et d'interagir (les faire manger) avec eux.

# Patrons de conception

Les patrons de conceptions sont des solutions éfficaces à des problêmes connues.

#### Open Close principle

Les entités d'un logiciel tel que les classes ou les modules devraient être OUVERT extension mais FERMÉ pour modification

![](http://www.oodesign.com/images/stories/ocp.bad.gif) ![](http://www.oodesign.com/images/stories/ocp.good.gif)

#### Inversion du contrôle de dépendance

Les modules de haut niveau de doivent pas dépendre des modules de bas niveaux. Ils devraient dépendre d'abstraction des modules de bas niveaux. De plus les abstractions ne devraient pas reposer sur des détails, ce sont les détails qui dépendent des abstractions.

#### Segrégation des interfaces

Les clients ne devraient pas avoir à dépendre des interfaces qu'ils n'utilisent pas

#### Responsabilité UNIQUE

Une classe ne doit avoir qu'une seule responsabilité

#### Principes de Liskov

Les types dérivés doivent pouvoir substituer les types de bases en tout temps

## Patrons les + importants.

*   Observateur
*   Fabrique
*   Singleton
*   Decorateur
*   Adapteur
*   Itérateur
*   Strategie
*   Proxy
*   Builder

## Observateur

Il est difficile de parler de prog orientée objets sans considérer leur états. La programmation orientée n'objet n'a pour seul but les objets et leurs interactions et donc leurs états. De ce fait, il existe une infinité de raison pour des objets d'avoir besoin de connaitre l'état d'un autre objet du système. Dans le but de découpler au maximum cet échange d'information, nous avons besoin d'un DP adatpé. Ce design pattern est l'Observeur. C'est un patron comportemental.

![](http://www.oodesign.com/images/design_patterns/behavioral/observer_implementation_-_uml_class_diagram.gif)

Un exemple du monde réel

![](http://www.oodesign.com/images/design_patterns/behavioral/observer_example_newspublisher_-_uml_class_diagram.gif)

L'observeur est en général utilisé dans un environement MVC où la gestion d'évènement est au coeur du système.

Quelques Warnings à retenir :

*   Many to Many relationships

Cela n'arrive pas souvent mais dans certains cas, nous avons besoin d'observer plus d'un objet et cet objet doit informer plusieurs observeur. Dans ce cas, l'implémentation classique de l'observeur doit être modifiée car il doit être informé du changement d'état et aussi de quel objet a changé d'état !

*   Renversement de responsabilité

Dans le cas où un objet change très fréquement d'état (pls fois par seconde), il n'est pas forcement opportun que ce soit l'objet observé qui soit en charge de transmettre son état. En effet, dans ce cas, l'observateur peut venir chercher l'état. Nous avons donc un renversement de responsabilités.

*   Mon objet observé est-il consitent ?

Dans des systèmes transactionelles, il est important de s'assurer que l'état interne d'un objet est cohérent avant de déclancher la notification...

## Fabrique

La fabrique, plus connue sous le nom de Factory est l'un des DP les plus utilisé dans les languages modernes tel que Java ou C#. Il y différentes implémentations, mais l'esprit reste gobalement le même. Pour le GoF, ce DP peut être nommé Factory Method ou Abstract Factory. Son atout principal est de créer des objets sans exposer la logique au client puis de faire référence à ses nouveaux objets via une interface communes.

![](http://www.oodesign.com/images/stories/factory%20noob%20implementation.gif)

Une version plus complexe et aussi plus utile de la Factory classique est l'abstract Factoty. Grace à elle nous pouvons offir une interface pour créer des objets d'une même famille sans spécifier explicitement leurs classes d'implémentation.

![](http://www.oodesign.com/images/creational/abstract-factory-pattern.png)

Et un exemple de monde réel

![](http://www.oodesign.com/images/creational/abstract-factory-pattern-example.png)

## Singleton

Il peut être important dans une application d'avoir une et une seule instance d'une classe. Par exemple, dans un système, il n'y a qu'un seul géstionnaire de fenêtres, qu'un seul gestionnaire d'impression ect. Le singleton est un pattern de la famille des creations. Il est l'un des patrons de conceptions les plus simples car il n'implique d'une seule classe et il est très facile à implémenter / prendre en main. Pour résumer, ses responsabilités sont d'assurer qu'un et un seul objet d'un certain type a été créé et fournir un accès glabal à cet objet

![](http://www.oodesign.com/images/design_patterns/creational/singleton_implementation_-_uml_class_diagram.gif)

Les cas d'utilisations sont nombreux pour le Singleton

*   Logging
*   Classes de configuration
*   Accès à des ressources partagées
*   Les factories vues précedement sont souvent des singletons.

Bien que sa compréhension et son implémentation naïve soient relativement simples, le singleton pousse à la réflection lorsque l'on veut être absolument sûr qu'un seul objet est créé dans un environnement concurrent.

#### Lazy instantiation

{% highlight java %}//Lazy instantiation using double locking mechanism.
class Singleton
{
	private static Singleton instance;

	private Singleton()
	{
	System.out.println("Singleton(): Initializing Instance");
	}

	public static Singleton getInstance()
	{
		if (instance == null)
		{
			synchronized(Singleton.class)
			{
				if (instance == null)
				{
					System.out.println("getInstance(): First time getInstance was invoked!");
					instance = new Singleton();
				}
			}            
		}

		return instance;
	}

	public void doSomething()
	{
		System.out.println("doSomething(): Singleton does something!");
	}
}
{% endhighlight %}

#### Early instantiation

{% highlight java %}//Early instantiation using implementation with static field.
class Singleton
{
	private static Singleton instance = new Singleton();

	private Singleton()
	{
		System.out.println("Singleton(): Initializing Instance");
	}

	public static Singleton getInstance()
	{    
		return instance;
	}

	public void doSomething()
	{
		System.out.println("doSomething(): Singleton does something!");
	}
}
{% endhighlight %}

#### Constructeur private ou protected

#### ClassLoaders

Si votre application utilise plusieurs classes loader, par exemple pour faire de la génération automatique de classes, vous devez créer votre classe loader. Dans ce cas là, l'unicité n'est plus garantie ! En effet, une même classe chargée par deux classes loader différents sera vue comme deux classes différentes dans la JVM et donc vous pourriez avoir N instance du Singleton :x

#### Sérialization

Si un singleton est sérializable et qu'il sérializer puis désérialisé plus d'une fois alors il y aura pls instances du Singleton dans le système :'(

{% highlight java %}public class Singleton implements Serializable {
		...

		// This method is called immediately after an object of this class is deserialized.
		// This method returns the singleton instance.
		protected Object readResolve() {
			return getInstance();
		}
	}
{% endhighlight %}

Pour résumer, le singleton est une arme facile à utiliser. Cependant, vous devez faire attention au retour de flamme si vous êtes dans des environnements multithreadés, sérializable, avec de multiples classes loader...

## Decorateur

Afin d'étendre les fonctionnalités d'un objet nous avons deux choix. La méthode statique via l'héritage par exemple ou la méthode dynamique, at runtime. Le décarateur est un patrons structurel qui permet d'ajouter des fonctionnalités dynamiquement -- lors de l'exécution à un objet

![](http://www.oodesign.com/images/design_patterns/structural/decorator-design-pattern-implementation-uml-class-diagram.png)

L'exemple le plus classique étant celui de l'extention des possibilités d'une fenêtre at runtime

![](http://www.oodesign.com/images/design_patterns/structural/decorator-design-pattern-example-uml-class-diagram.png)

Le décorateur est souvent utilisé en complément des patrons adaptor et composite. Un des autres avantages de la décoration par rapport à l'héritage est que nous pouvons aussi retiré des fonctionnalités at runtime.

## Adapteur

L'adapteur, comme son nom l'indique, a pour vocation d'adapter certaines classes d'objets entre elle. Comme els adapteurs du monde réel, le patrons adapteur est conçu pour être un adapteur entre deux objets, pour servir de pont de communication / traduction entre eux. De manière générale, l'adapteur convertira des interface de classe en d'autre inteerface afin de pouvoir utiliser les premières. De plus, l'adapteur permet la collaboration entre des classes qui ne le pourraient pas autrement. Une exemple du monde réel ? Les adapteur de prises de courant US/EU...

![](http://www.oodesign.com/images/structural/adapter-pattern.png)

Nous pouvons aussi créer des adapteurs à double sens. Dans ce cas l'adapteur implémente les deux interfaces. Celle de la cible et de l'adapté. Ainsi, l'adapté peut être utilisé à la fois comme la cible et comme l'adapté. Les deux systèmes peuvent donc collaborer de manière transparante ! De plus, l'adapteur collabore souvent avec le pattern startegy.

## Itérateur

L'itérateur est à la base d'une des structures de données les plus utilisées dans le dév de logiciel moderne. L'itérateur fournir un moyen d'accéder aux éléments d'une collections d'objet d'une même famille sans exposer la représentation sous-jacente. L'abstraction fournie par l'itérateur nous permet de modifier l'implémenation d'une collection sans provoquer de changement sur le code qui utilise cette collection.

![](http://www.oodesign.com/images/design_patterns/behavioral/iterator_implementation_-_uml_class_diagram.gif)

De manière général l'itétateur souffre des même maux que le singleton lorsque l'on utilise ce dernier dans des environnements concurrents. Une question à poser lors de l'implémentation d'un itérateur est celle-ci. Est-ce que l'itérateur doit être interne à la collection via une méthode ou alors externe via une autre classe ? La réponse est , comme souvent, ça dépend :).

## Strategie

Le but premier du patrons stratégie est de pouvoir donner des comportement différent à la même classes. En effet, pourquoi créer autant de classes que de comportements cible souhaités si les classes ont les même proprités. Par exemple, un robot avec trois attitude, neutre, aggrésif, défensif. Il est plus opportun de modifier le comportement de mon robot en fonction de paramètre extérieur plutôt que de créer 3 robot. De plus, mon robot pourra changer de comportement at runtime. Le stratégie nous permet donc de définir une famille d'algos qui sont interchangeable et qui seront plus ou moin adapté en fonction d'une situation donnée

![](http://www.oodesign.com/images/design_patterns/behavioral/strategy_implementation_-_uml_class_diagram.gif)

Et l'exemple avec le robot

![](http://www.oodesign.com/images/design_patterns/behavioral/strategy_example_robot_-_uml_class_diagram.gif)

Nous avons vu les avantages du stratégie. Cependant, l'un de ses principal défaut est que le client DOIT comprendre pourquoi et comment les stratégies diffère pour pouvoir choisir la plus adaptée.

## Proxy

Dans certains cas, nous avons besoin de contrôler l'accès à un objet. La manière et le moment où il est fait. Notamment dans le cas d'accès à des méthodes couteuses, tel que le chargement en mémoire d'un fichier très lourd. Le but principal du Proxy est de fournir un PlaceHolder pour un objet dans le but d'en controler la référence réel. La définition est un peu compliquée, mais l'implémentation assez simple.

![](http://www.oodesign.com/images/design_patterns/structural/proxy-design-pattern-implementation-uml-class-diagram.png)

Il y a plusieurs sortes de proxy.

*   Le Proxy Virtuel: Retarde la création et / ou l'instantiation et / ou l'initialisation d'un objet couteux, tel qu'une image. Lorsque l'utilisateur a réelement besoin de l'image alors elle est chargée

*   Les proxy de protection: qui protègent l'accès à certaines méthodes d'objets en fonction de l'autorisation d'un client

Un example de proxy virtuel pour le chargement d'images![](http://www.oodesign.com/images/design_patterns/structural/proxy-design-pattern-image-example-uml-class-diagram.png)

## Builder

Plus la compléxité des applications augmente, plus celles des collaborations entre les classes et les objets augmente. Les objets complexes sont créés par des parties d'autre objets et leurs créations dépend du context d'exécution et de l'environnement extérieur. Ainsi, le builder permet de définir une instance pour créer un objet mais laisse les sous-classes décider quelle classe elles souhaitent implémenter. De plus, les références à ces objets sont fait grace à une interface communes

![](http://www.oodesign.com/images/creational/builder-pattern.png)

Un exemple de builder pour un convertisseur de texte

![](http://www.oodesign.com/images/creational/builder-pattern-example.png)

## Etude de cas : Paint.GoF - Partie I.

Paint.Gof est un logiciel de dessin assisté par ordinateur qui a les caractéristiques suivantes :

*   Dessin de formes : Ligne, Rond, ...
*   Dessin de formes complexes : Composition d'une forme a partir de forme simple (ex: un rond dans un Rectange)
*   Décomposition des formes complexes : Liste des formes simples composant une forme complexe
*   La comportement de la fonction de décomposition dépends de l'OS de l'utilisateur (Mac -> FIFO; Windows -> LIFO; Linux -> non supportée)
*   Gestion d'un pool d'imprimante (A4, A3 et A2)

### Résultats attendus

{% highlight java %}Que voulez-vous faire ? (Dessiner; imprimer)
	>Dessiner
	Quel type de forme voulez-vous dessiner ? (Simple, Complexe)
	>Simple
	Quelle forme voulez-vous dessiner ? (Ligne, Rond)
	>Ligne 5 5 10 10
	Vous avez dessiné un ligne passant par Y(5,5) et Z(10,10)
	Que voulez-vous faire ? (Dessiner; imprimer)
	>Dessiner
	Quel type de forme voulez-vous dessiner ? (Simple, Complexe)
	>Complexe
	Votre forme se compose de ? (LigneS, RondS)
	>Ligne 5 5 5 10 Ligne 0 5 0 10 Ligne 0 5 0 10 Ligne 0 10 5 10
	Votre forme se compose de 4 ligne(s)
		// Affichage des lignes en fonction de l'OS
	Que voulez-vous faire ? (Dessiner; imprimer)
	>imprimer
	Choisir votre imprimante (A4, A3, A2)
	>A3
	Vous avez imprimé en A2.
{% endhighlight %}

### Design patterns à utiliser (au minimum)

*   Strategy
*   Factory
*   Decorateur

## Etude de cas : Paint.GoF - Partie II.

Aggrémentez votre architecture pour que celle-ci supporte les--nouvelles--fonctionalités suivante :

*   Export PDF; via une imprimante PDF.
*   Gestions d'images de haute qualitée

*   Il est possible d'ajouter des images à une listes d'images sur lesquelles ont souhaite travailler.
*   Cependant; une image n'est réelement chargée que lorsque l'on commence à travailler dessus.

###  Résultats attendus

{% highlight java %}Que voulez-vous faire ? (Dessiner; Ajouter Image; Travailler sur Image; Imprimer)
>Ajouter Image c:\mon-image.png // L'image n'est pas chargée dans la mémoire
Que voulez-vous faire ? (Dessiner; Ajouter Image; Travailler sur Image; Imprimer)
>Ajouter Image c:\mon-image-2.png // L'image n'est pas chargée dans la mémoire
Que voulez-vous faire ? (Dessiner; Ajouter Image; Travailler sur Image; Imprimer)
>Travailler sur Image c:\mon-image.png // L'image est chargée.
Que voulez-vous faire ? (Dessiner; Ajouter Image; Travailler sur Image; Imprimer)
>Imprimer
Quels type d'impression ? (Papier (A4,A3,A2) ou PDF(A4,A3,A2))
>PDF A2
// L'export PDF lance aussi la décomposition
{% endhighlight %}

### Design patterns à utiliser (au minimum)

*   Proxy
*   Abstract Factory

# Design Patterns Abuse

<iframe src="https://docs.google.com/gview?url=https://math.co.de/media/DesignPatternsAbuse.pdf&embedded=true" style="width:718px; height:700px;" frameborder="0"></iframe>

* Voir aussi [Smells & Antipatterns](https://math.co.de/cours/Introduction-to-smells/)

# Design Patterns For The Real World

<iframe src="https://docs.google.com/presentation/d/18XVrS3XccMcqUgd6z6A5SLcCPhRx268BEHm2-oj7ltA/embed?start=false&loop=false&delayms=3000" frameborder="0" width="960" height="569" allowfullscreen="true" mozallowfullscreen="true" webkitallowfullscreen="true"></iframe>
