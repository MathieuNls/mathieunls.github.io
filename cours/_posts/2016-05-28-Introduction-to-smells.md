---
layout: post
title: An introduction to smell
tags:
- smell
- anti-patterns
description: An introduction to smell
image:
  feature: https://mwidlake.files.wordpress.com/2011/08/silver-bullet.jpg
  credit: Orcale
  creditlink: https://mwidlake.wordpress.com/2011/08/05/friday-philosophy-oracle-performance-silver-bullet/
excerpt: Smells and anti-patterns are bad solutions to knwon problems
---
{% include _toc.html %}

## Smell

Les codes smells sont souvent méconnus des programmeurs qui ne conaissent que la partie visible. C a d, l'accumulation de smells qui forment un anti-patron. Au stade de l'anti-patron, il est déjà trop tard. Le refactoring sera de grande ampleur... Ainsi, les ingénieurs logiciel et parmis eux Fowler, ont inventé la notion de code smell. Les code smell sont n'importe quel symptôme d'un source code qui pourrait indiquer la présence d'un problème plus profond. En règles général, un code smell ne signifie pas un bug, ils n'empèchent pas le programme de bien fonctionner. Par contre, ce qu'ils indiquent, c'est une faiblaisse du design du programme qui peut elle même se traduire en des lenteurs dans les évolutions ou dans l'exécution.  
Souvent, les problèmes profond liés au code smell ne sont pas révélés lors d'analyses rapides et peu profonde du code--lorsque le refactoring de faible ampleur entre les releases. Lorsqu'un programmeur est en charge du refactoring, les code smells sont des indicateurs cruciaux de la qualité sous-jacente de l'architecture, ils agissent comme des heuristiques permettant de jauger la qualité du code. Ainsi, les codes smells _doivent_ être éliminés lors du refactoring

Une liste non exhaustive decodes smells, ceux identifiés par Fowler sont en gris.

![](/images/eXia1.png)

## Anti-Patterns

Les patrons de sont de bonnes pratique pour résoudre des problèmes récurrent. A l'inverse les anti-patrons sont de mauvaises pratiques courrament utilisées pour résoudre, eux aussi, des problèmes courant ! Comme les smells, les anti-patrons peuvent être transparent en terme de fonctionnalités pour l'utilisateur mais auront un impact beaucoup plus important que les smells sur le programme. Que ce soit au niveau de son évolution ou de son exécution. Il existe des AP pour tout les pans d'une organisation. La liste [wikipedia](http://en.wikipedia.org/wiki/Anti-pattern) est plutôt impréssionante surtout en y rajoutant 2/3 des ceux spécifiés par le LATECE :).

#### Organisationel

*   Analysis paralysis: Devoting disproportionate high effort to the analysis phase of a project
*   Cash cow: A profitable legacy product that often leads to complacency about new products
*   Design by committee: The result of having many contributors to a design, but no unifying vision
*   Escalation of commitment: Failing to revoke a decision when it proves wrong
*   Management by perkele: Authoritarian style of management with no tolerance of dissent
*   Management by objectives: Management by numbers, focus exclusively on quantitative management criteria, when these are non-essential or cost too much to acquire
*   Moral hazard: Insulating a decision-maker from the consequences of his or her decision
*   Mushroom management: Keeping employees uninformed and misinformed; employees are described as being kept in the dark and fed manure, left to stew, and finally canned
*   Stovepipe or Silos: A structure that supports mostly up-down flow of data but inhibits cross organizational communication
*   Vendor lock-in: Making a system excessively dependent on an externally supplied component

#### Conduite de projet

*   Avalanche: An inappropriate mashup of the Waterfall model and Agile Development techniques
*   Death march: Everyone knows that the project is going to be a disaster – except the CEO – so the truth is hidden to prevent immediate cancellation of the project - (although the CEO often knows and does it anyway to maximize profit). However, the truth remains hidden and the project is artificially kept alive until the Day Zero finally comes ("Big Bang"). Alternative definition: Employees are pressured to work late nights and weekends on a project with an unreasonable deadline.
*   Groupthink: During groupthink, members of the group avoid promoting viewpoints outside the comfort zone of consensus thinking
*   Overengineering: Spending resources making a project more robust and complex than is needed
*   Scope Creep: Uncontrolled changes or continuous growth in a project’s scope, or adding new features to the project after the original requirements have been drafted and accepted. 
*   Smoke and mirrors: Demonstrating unimplemented functions as if they were already implemented
*   Software bloat: Allowing successive versions of a system to demand ever more resources

#### Design

*   Abstraction inversion: Not exposing implemented functionality required by users, so that they re-implement it using higher level functions
*   Ambiguous viewpoint: Presenting a model (usually Object-oriented analysis and design (OOAD)) without specifying its viewpoint
*   Big ball of mud: A system with no recognizable structure
*   Database-as-IPC: Using a database as the message queue for routine interprocess communication where a much more lightweight mechanism would be suitable
*   Gold plating: Continuing to work on a task or project well past the point at which extra effort is adding value
*   Inner-platform effect: A system so customizable as to become a poor replica of the software development platform
*   Input kludge: Failing to specify and implement the handling of possibly invalid input
*   Interface bloat: Making an interface so powerful that it is extremely difficult to implement
*   Magic pushbutton: Coding implementation logic directly within interface code, without using abstraction
*   Race hazard: Failing to see the consequence of different orders of events
*   Stovepipe system: A barely maintainable assemblage of ill-related components

#### Spécifique Objets

*   Anemic Domain Model: The use of the domain model without any business logic. The domain model's objects cannot guarantee their correctness at any moment, because their validation and mutation logic is placed somewhere outside (most likely in multiple places).
*   BaseBean: Inheriting functionality from a utility class rather than delegating to it
*   Call super: Requiring subclasses to call a superclass's overridden method
*   Circle-ellipse problem: Subtyping variable-types on the basis of value-subtypes
*   Circular dependency: Introducing unnecessary direct or indirect mutual dependencies between objects or software modules
*   Constant interface: Using interfaces to define constants
*   God object: Concentrating too many functions in a single part of the design (class)
*   Object cesspool: Reusing objects whose state does not conform to the (possibly implicit) contract for re-use
*   Object orgy: Failing to properly encapsulate objects permitting unrestricted access to their internals
*   Poltergeists: Objects whose sole purpose is to pass information to another object
*   Sequential coupling: A class that requires its methods to be called in a particular order
*   Yo-yo problem: A structure (e.g., of inheritance) that is hard to understand due to excessive fragmentation

#### Spécifique SOA

*   Multi Service also known as God Object corresponds to a service that implements a multitude of methods related to different business and technical abstractions. This service aggregates too many methods into a single service, such a service is not easily reusable because of the low cohesion of its methods and is often unavailable to end-users because of its overload, which may induce a high response time.
*   Tiny Service is a small service with few methods, which only implements part of an abstraction. Such service often requires several coupled services to be used together, resulting in higher development complexity and reduced usability. In the extreme case, a Tiny Service will be limited to one method, resulting in many services that implement an overall set of requirements.
*   Sand Pile is also known as Fine-Grained Services. It appears when a service is composed by multiple smaller services sharing common data. It thus has a high data cohesion. The common data shared may be located in a Data Service antipattern (see below).
*   Chatty Service corresponds to a set of services that exchange a lot of small data of primitive types, usually with a Data Service antipattern. The Chatty Service is also characterized by a high number of method invocations. Chatty Services chat a lot with each other.
*   The Knot is a set of very low cohesive services, which are tightly coupled. These services are thus less reusable. Due to this complex architecture, the availability of these services may be low, and their response time high.
*   Nobody Home corresponds to a service, defined but actually never used by clients. Thus, the methods from this service are never invoked, even though it may be coupled to other services. Yet, it still requires deployment and management, despite of its non usage.
*   Duplicated Service, a.k.a. The Silo Approach introduced by IBM, corresponds to a set of highly similar services. Because services are implemented multiple times as a result of the silo approach, there may have common or identical methods with the same names and-or parameters.
*   Bottleneck Service is a service that is highly used by other services or clients. It has a high incoming and outgoing coupling. Its response time can be high because it may be used by too many external clients, for which clients may need to wait to get access to the service. Moreover, its availability may also be low due to the traffic.
*   Service Chain a.k.a. Message Chain in OO systems corresponds to a chain of services. The Service Chain appears when clients request consecutive service invocations to fulfill their goals. This kind of dependency chain reflects the subsequent invocation of services. Data Service, a.k.a. Data Class in OO systems, corresponds to a service that contains mainly accessor methods, i.e., getters and setters. In the distributed applications, there can be some services that may only perform some simple information retrieval or data access to such services. Data Services contain usually accessor methods with small parameters of primitive types. Such service has a high data cohesion.

#### Programmation

*   Accidental complexity: Introducing unnecessary complexity into a solution
*   Action at a distance: Unexpected interaction between widely separated parts of a system
*   Blind faith: Lack of checking of (a) the correctness of a bug fix or (b) the result of a subroutine
*   Boat anchor: Retaining a part of a system that no longer has any use
*   Busy waiting: Consuming CPU while waiting for something to happen, usually by repeated checking instead of messaging
*   Caching failure: Forgetting to reset an error flag when an error has been corrected
*   Cargo cult programming: Using patterns and methods without understanding why
*   Coding by exception: Adding new code to handle each special case as it is recognized
*   Error hiding: Catching an error message before it can be shown to the user and either showing nothing or showing a meaningless message. Also can refer to erasing the Stack trace during exception handling, which can hamper debugging.
*   Hard code: Embedding assumptions about the environment of a system in its implementation
*   Lava flow: Retaining undesirable (redundant or low-quality) code because removing it is too expensive or has unpredictable consequences
*   Loop-switch sequence: Encoding a set of sequential steps using a switch within a loop statement
*   Magic numbers: Including unexplained numbers in algorithms
*   Magic strings: Including literal strings in code, for comparisons, as event types etc.
*   Repeating yourself: Writing code which contains repetitive patterns and substrings over again; avoid with once and only once (abstraction principle)
*   Shotgun surgery: Developer adds features to an application codebase which span a multiplicity of implementors or implementations in a single change.
*   Soft code: Storing business logic in configuration files rather than source code[7]
*   Spaghetti code: Programs whose structure is barely comprehensible, especially because of misuse of code structures
*   Lasagna code: Programs whose structure consists of too many layers

#### Méthodo

*   Copy and paste programming: Copying (and modifying) existing code rather than creating generic solutions
*   Golden hammer: Assuming that a favorite solution is universally applicable (See: Silver Bullet)
*   Improbability factor: Assuming that it is improbable that a known error will occur
*   Not Invented Here (NIH) syndrome: The tendency towards reinventing the wheel (Failing to adopt an existing, adequate solution)
*   Invented Here: The tendency towards dismissing any innovation or less than trivial solution originating from inside the organization, usually because of lack of confidence in the staff
*   Premature optimization: Coding early-on for perceived efficiency, sacrificing good design, maintainability, and sometimes even real-world efficiency
*   Programming by permutation (or "programming by accident", or "programming by coincidence"): Trying to approach a solution by successively modifying the code to see if it works
*   Reinventing the square wheel: Failing to adopt an existing solution and instead adopting a custom solution which performs much worse than the existing one
*   Silver bullet: Assuming that a favorite technical solution can solve a larger process or problem
*   Tester Driven Development: Software projects in which new requirements are specified in bug reports

#### Configuration

*   Dependency hell: Problems with versions of required products
*   DLL hell: Inadequate management of dynamic-link libraries (DLLs), specifically on Microsoft Windows
*   Extension conflict: Problems with different extensions to pre-Mac OS X versions of the Mac OS attempting to patch the same parts of the operating system
*   JAR hell: Overutilization of the multiple JAR files, usually causing versioning and location problems because of misunderstanding of the Java class loading model

## Focus sur les VRAIMENT TRES dangereux en objets

### Blob

##### Problème

The Blob (also called God class) corresponds to a large controller class that depends on data stored in surrounding data classes. A large class declares many ﬁelds and methods with a low cohesion. A controller class monopolises most of the processing done by a system, takes most of the decisions, and closely directs the processing of other classes [44]. Controller classes can be identiﬁed using suspicious names such as Process, Control, Manage, System, and so on. A data class contains only data and performs no processing on these data. It is composed of highly cohesive ﬁelds and accessors.

![](http://sourcemaking.com/files/sm/images/antipatterns/img_21.jpg)

##### Solution

*   Identifier les catégories d'attributs appartenant au mm contrat. Ils doivent de la mm famille et les interfaces résultantes doivent être cohésives !
*   Trouver des emplacements naturels pour vos interfaces. Des packages addaptés en Java par ex
*   Supprimer les couplages distant et transitifs
*   Migrer les attributs dans des classes de spécialisations

### Fonctionnal Decomposition

##### Problème

The Functional Decomposition antipattern may occur if experienced procedural developers with little knowledge of object-orientation implement an object-oriented system. Brown describes this antipattern as “a ‘main’ routine that calls numerous subroutines”. The Functional Decomposition design smell consists of a main class, i.e., a class with a procedural name, such as Compute or Display, in which inheritance and polymorphism are scarcely used, that is associated with small classes, which declare many private ﬁelds and implement only a few methods.

![](http://sourcemaking.com/files/sm/images/antipatterns/img_31.jpg)

##### Solution

*   Trouver les fonctions critiques
*   Motivations sous-jascente à ces Fx
*   Documentation détaillée pour chaque Fx
*   Modèle qui intègre les Fx principales.

*   Ne pas chercher à tout inclure
*   Ne pas chercher à améliorer le modèle existant
*   Juste créer un modèle qui fit.

*   Pour les Fx secondaires

*   Si une classe se résume à une méthode: Essayer des les grouper ailleurs
*   Une classe d'une méthode PEUT être justifiée

*   Essayer de merger des classes similaires en gardant une certain max en taille
*   Si une classe ne contient pas d'état interne, cela veux p e dire que c'est uen fonction
*   Considérer les sous-système et éssayer des les fusionner car il y a svt duplication

### Spaghetti

##### Problème

The Spaghetti Code is an antipattern that is characteristic of procedural thinking in object-oriented programming. Spaghetti Code is revealed by classes with no structure, declaring long methods with no parameters, and utilising global variables. Names of classes and methods may suggest procedural programming. Spaghetti Code does not exploit and prevents the use of object-orientation mechanisms, polymorphism and inheritance.

##### Solution

En général... Reprendre from scratch... Le tout après un cours de OO...

### Swiss Army Kniss

##### Problème

The Swiss Army Knife refers to a tool fulﬁlling a wide range of needs. The Swiss Army Knife design smell is a complex class that offers a high number of services, for example, a complex class implementing a high number of interfaces. A Swiss Army Knife is different from a Blob, because it exposes a high complexity to address all foreseeable needs of a part of a system, whereas the Blob is a singleton monopolising all processing and data of a system. Thus, several Swiss Army Knives may exist in a system, for example utility classes.

![](http://sourcemaking.com/files/sm/images/antipatterns/img_51.jpg)

##### Solution

Etablir des familles de fonctionnalités et redécouper en interface correspondante

## Cause d'apparitions

Comme vous l'aurez sans doute remarqué. Les anti-patrons patrons objets sont souvent causé par des pratiques de dev. procédurals. De la même manière, les anti-patrons SOA sont causé par des pratiques de dev objets. Ainsi, de manière général, les anti-patrons apparaissent à cause de l'utilisation de technique de prog. antérieures

## Refactoring

### Refactoring, pourquoi ?

Le Refactoring est une technique disciplinée pour améliorer la structure de code existant sans changer le comportement observable. Comme Danny Dig expose sur son site [Web](http://refactoring.info/). Pour faire court : changez la structure de votre code, sans changer le comportement. En utilisant le Refactoring, vous pouvez facilement déplacer des champs(domaines), méthodes ou des classes dans votre programme sans rien abimer. Les Refactorings peuvent être aussi simple que de renomer un champ ou infiniment plus complexe via lors de la séparation des responsabilité dans une architectures

### Refactoring by Fowler & Dig

Le site de Martin Fowler sur le refactoring [http://refactoring.com](http://refactoring.com). Si vous ne connaissez pas encore [Fowler](http://martinfowler.com/) je ne peux que vous conseiller d'acquérir sa bibliographie au plus vite. (Lien amazon [ici](http://amzn.to/ZkFbOi))

Vous pouvez aussi vous référer au site de Danny Dig sur le refactoring [ici](http://refactoring.info) ou encore [http://sourcemaking.com/](http://sourcemaking.com/) qui propose des explications simples et illustrées.

### Exemple de Refactoring dans NetBeans

Télécharger le projet [INF2015_Refactoring](/media/INF2015_Refactoring.zip). Déziper-le puis importer le dans NetBeans

*   Franciser les param de Etudiants. (CTRL+R)
*   Remonter date de naissance dans Humain (Pull Up), les getters/setters aussi.
*   Renomer codePermanent en codePermat
*   Introduire un champs BaseCommune
*   Inliner la méthode concateDate dans createCodePerma
*   Dans HUMAIN. Changer la visibiliter de age en privé. Générer des accésseurs pour les 3 champs
*   Dans COURS. Extraire une superclasse pour pouvoir en dériver des démos
*   Créer une classe Salle, puis extraire une superclasse lieuEnseignement pour en dériver labos

### Projet Final

La correction [ICI !](/media/INF2015_Refactoring-correction.zip)

## Mais comment je fais pour les détecter ? Pour savoir qu'ils sont là ?

Bien que la classifcation d'un code en smell ou en anti-pattern soit souvent subjective car il existe plein d'exceptions pour lesquelles il est acceptable d'avoir un anti-pattern, des outils gratuits existent pour analyser automatiquement votre code et vous faire un retour qualité.

### CheckStyle

![](http://assets.devx.com/articlefigs/15466.gif)

### PMD

![](http://plugins.netbeans.org/data/images/1340992348_pmdSmall.png)

### FindBugs

![](http://jroller.com/andyl/resource/findbugs_1.3.2_news.png)
