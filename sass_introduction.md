# Introduction à Sass

[Sass](http://sass-lang.com/) est un préprocesseur CSS qui compile et transforme votre code Sass en code CSS. CSS est au départ un language simple et de nature purement déclarative. Sass vous permet d'étendre les possibilités du language CSS en utilisant des éléments de programmation.

- variables, listes, maps et fonctions
- operations (mathématiques, couleurs)
- structures de controles (@if, @for, @each et @while)

Sass vous permet également de gérer plus efficacement votre code CSS et de ne pas vous répéter inutilement.

- nesting
- `@mixins`
- `@extend`
- `@media`
- `@import`

Attention cependant, Sass n'est pas une technologie qui vous fera magiquement écrire du code CSS propre et optimisé. Le prérequis est de bien connaître CSS d'abord et d'être toujours attentif au code généré. Sass est un outil qui peut vous faciliter la vie mais ce qui importe en fin de compte c'est le code CSS généré.

A mon sens, les avantages de Sass sont:

- A travers les mixins, les fonctions, les variables et `@extend` Sass vous permet de réutiliser votre code dans le cadre de plusieurs projets.
- Utiliser `@import` vous permet également de simplifier la maintenance de gros projets CSS en travaillant à l'aide de fichiers séparés et hiérarchisés
- Sass vous permet de compresser automatiquement vos fichiers CSS en une seule ligne, les rendant plus légers à transférer vers les navigateurs de vos utilisateurs.

Nous verrons plus loin que, grâce à sa syntaxe `scss`, Sass est entièrement compatible avec le language CSS que vous connaissez déjà. Autrement dit, prenez un fichier CSS existant et changez son extension de fichier en `.scss` et vous écrivez du Sass. Cela rend cette technologie facile à apprendre et vous permet de l'adopter petit à petit dans vos projets.

Sass dépend de [Ruby](https://www.ruby-lang.org/). Cela ne veut pas pour autant dire que vous devez maîtriser ce language pour utiliser Sass. De la même manière, même si Sass peut être entièrement géré depuis votre terminal en lignes de commande, vous n'êtes pas obligés de suivre cette voie. Il existe de très bons programmes GUI vous permettant d'utiliser Sass sans pour autant devoir recourir à votre terminal.

## Deux syntaxes

Vous pouvez utiliser deux syntaxes différentes pour écrire vos fichiers: la syntaxe `scss` et la syntaxe indentée ou `Sass`plus ancienne.

Nous utiliserons ici la syntaxe `scss` qui est compatible avec CSS3 et dont les fichiers fonctionnent avec l'extension `.scss`.

## Installation

Sass dépend de Ruby, il vous faudra donc installer Ruby sur votre machine avant toute chose. Sur un mac, Ruby est déjà présent, tandis que sur Windows, il vous faudra [l'installer](http://rubyinstaller.org/downloads/).

Il vous suffit ensuite d'installer la "gem" sass pour être opérationnel.

```
gem install sass
```

### Sass en ligne de commande

Utiliser Sass en ligne de commande dans votre terminal est vraiment très simple. Vous n'aurez que quelques commandes à retenir pour pouvoir travailler.

```
sass scss/screen.scss:css/screen.css
```

Permet de compiler le fichier `scss/screen.scss` vers le fichier de destination `css/screen.css`.

Lorsqu'on travaille sur un projet, il est intéressant de ne pas répéter cette opération à chaque modification. Sass est capable de détecter les changements faits dans un fichiers ou dans tous les fichiers d'un dossier et de générer votre fichier CSS automatiquement lorsque des changements sont détectés.

```
sass --watch scss/screen.scss:css/screen.css
```

ou

```
sass --watch scss/:css/
```

Vous remarquerez que les fichiers CSS ont générés avec un certain style d'output. Il en existe 4 différents avec sass:

- Nested (default)
- Expanded
- Compact
- Compressed

Typiquement, les styles `nested` ou `expanded` sont utilisés en développement, alors que `compressed` est utilisé en production pour minifier vos fichiers CSS. Personnellement, je n'utilise jamais le style `compact`.

```
sass --watch scss/:css/ --style nested
sass --watch scss/:css/ --style expanded
sass --watch scss/:css/ --style compact
sass --watch scss/:css/ --style compressed
```

### Applications

Si ces quelques ligne de commande vous rebutent vraiment, vous pouvez également utiliser des applications GUI qui feront le travail pour vous. Il en existe beaucoup mais [Scout](http://mhs.github.io/scout-app/) (Mac et Windows) et [CodeKit](http://incident57.com/codekit/) (Mac) sont sans doute les plus connus, mais [il en existe d'autres](http://sass-lang.com/install).

Les outils de build ou task runners que sont [Grunt](http://gruntjs.com/) et [Gulp](http://gulpjs.com/) permettent également de compiler du code Sass en CSS.

## Concepts

Maintenant que nous avons installé Sass et que nous avons un workflow, pratiquons un peu.

### Imports et partials

la fonction `@import` vous permet d'importer des fichiers Sass les uns dans les autres et ainsi de structurer efficacement votre projet CSS. Cette fonctionnalité prend tout son sens lorsque vous travaillez sur des projets de grande taille et relativement complexe.

Habituellement, vos fichiers sont structurés de telle manière que votre fichier .sass principal ne contienne que des directives `@import`. Vous pouvez préfixer le nom des fichiers importés avec "_" de manière à ce que Sass ne les compile pas directement.

Voici, par exemple, une structure possible pour vos fichiers Sass dans le cadre d'un projet plus complexe.

```scss
imports
	- _normalize.scss
	- _variables.scss
	- _mixins.scss
	- _functions.scss
	- _helpers.scss
	- _grid.scss
partials
	- _base.scss
	- _layout.scss
	- _typography.scss
	- _modules.scss
	- _states.scss
	- _header.scss
	- _footer.scss
vendors
	- _flexslider.scss
screen.scss
```

### Variables, Listes et maps

Les variables et les listes sont sans doute les fonctionnalités de Sass que vous intégrerez le plus facilement à votre workflow existant.

#### Variables

Qui n'a jamais rêvé en CSS de pouvoir travailler avec des variables pour les couleurs de la charte graphique utilisée ? C'est désormais possible en Sass.

```scss
$color-txt:#020202;
$color-bkg:#FEFBF6;
$color-accent:#F16C32;

body
{
	background:$color-bkg;
	color:$color-txt;
}

a
{
	color:$color-accent;
}
```

*Exercice: créer un fichier _variables.scss, définissez quelques variables pour les couleurs et importez-le dans votre fichier Sass principal. Tant que vous y êtes, voyez comment vous pouvez appliquer cette logique pour d'autres choses (comme par exemple vos font-stacks).*

#### Listes

Les listes sont un bon moyen de créer des variables complexes en Sass, qui offre différents fonctions spécifiques aux listes pour les exploiter au mieux. Nous en verrons un exemple un peu plus loin.

En gros vous pouvez créer des listes simples ou des listes imbriquées dans Sass. Vous pouvez utiliser ou des virgules ou des espaces comme séparateurs.

```scss
$fruits-espaces:    "pomme" "poire" "orange";
$fruits-virgules:   "pomme", "poire", "orange";
```
Pour des listes imbriquées, soit vous utilisez des séparateurs différents, soit vous pouvez utiliser des parenthèses.

```scss
/* Nested lists with braces and same separator */
$list: (
        ("item-1.1", "item-1.2", "item-1.3"),
        ("item-2.1", "item-2.2", "item-2.3"),
        ("item-3.1", "item-3.2", "item-3.3")
       );

/* Nested lists without braces using different separators to distinguish levels */
$list: "item-1.1" "item-1.2" "item-1.3",
       "item-2.1" "item-2.2" "item-2.3",
       "item-3.1" "item-3.2" "item-3.3";
```

Hugo Giraudel propose [un excellent article d'introduction aux listes en Sass](http://hugogiraudel.com/2013/07/15/understanding-sass-lists/) si vous voulez en savoir plus sur les listes. De manière générale, [le site de Hugo](http://hugogiraudel.com/) est une mine d'or en ce qui concerne Sass.

Sass possède [de nombreuses fonctions](http://sass-lang.com/documentation/Sass/Script/Functions.html) vous permettant de manipuler des listes. Celles-ci sont similaires à ce que vous pouvez trouver dans d'autres languages de programmation.

#### Maps

@TODO

### Nesting et l'opérateur "&"

Sass vous permet d'imbriquer vos sélecteurs CSS. Dans certain cas c'est bien utile, mais cela peut également dégénérer très rapidement.

Je vous conseille donc de ne pas en abuser et de vous limiter à imbriquer uniquement ce qui doit l'être, la règle d'or étant de ne jamais aller plus loin que trois niveaux d'imbrication.

L'opérateur "&" est très utile dans ce contexte puisqu'il permet de référencer le sélecteur parent.

Voici un exemple de nesting et d'utilisation de "&" dans Sass pour un menu de navigation.

```scss
.navbar
{
    width:100%;
    list-style:none;
    margin:0;
    padding:0;
    background:#000;
}

.navbar__item
{
    display:inline-block;

    > a
    {
        display:block;
        padding:.5em 1em;
        background:#000;
        color:#ccc;
        text-decoration:none;
        text-transform:uppercase;

        &:hover
        {
            background:#333;
            color:#fff;
        }

        &.current, &.current:hover
        {
            background:#F16C32;
            color:#020202;
        }
    }
}
```

compilé cela donne

```css
.navbar {
  width: 100%;
  list-style: none;
  margin: 0;
  padding: 0;
  background: #000; }

.navbar__item {
  display: inline-block; }

  .navbar__item > a {
    display: block;
    padding: .5em 1em;
    background: #000;
    color: #ccc;
    text-decoration: none;
    text-transform: uppercase; }

    .navbar__item > a:hover {
      background: #333;
      color: #fff; }

    .navbar__item > a.current, .navbar__item > a.current:hover {
      background: #F16C32;
      color: #020202; }
```

L'opérateur "&" et le nesting peuvent également être utilisés pour créer facilement des fallbacks avec les classes générées par [Modernizr](http://modernizr.com/). Voici un exemple pour servir une image en `.svg` et un fallback en `.png` aux navigateurs ne supportant pas ce format.

```scss
.icon--phone
{
	background:url(/img/sprite_icons.svg) 0 0 no-repeat;

	.no-svg &
	{
		background:url(/img/sprite_icons.png) 0 0 no-repeat;
	}
}
```

Deux articles intéressants sur the Sass Way sur le sujet du nesting avec Sass: "[the inception rule](http://thesassway.com/beginner/the-inception-rule/)" et "[Avoid nested selectors for more modular CSS](http://thesassway.com/intermediate/avoid-nested-selectors-for-more-modular-css/)".

### Commentaires

A ce stade vous allez sans doute commencer à avoir besoin de commentaires. Voici les différents types de commentaires Sass:

```scss
/*
commentaire
qui peut être en plusieurs lignes et qui apparaîtra dans la CSS générée (sauf en style compressed)
*/
```

```scss
/*!
commentaire
qui peut être en plusieurs lignes et qui apparaîtra dans la CSS générée (y compris en style compressed)
*/
```

```scss
// commentaire en une ligne qui n'apparait pas dans la CSS générée
```

### Opérations

Avec Sass, vous pouvez effectuer pas mal d'opérations, dont des opérations mathématiques et des opérations sur les couleurs.

#### Opérations mathématiques

Les [opérateurs mathématiques de base](http://sass-lang.com/documentation/file.SASS_REFERENCE.html#number_operations) (`-`, `+`, `*` et `/`) sont disponibles. Si des unités sont présentes, Sass tentera de faire une conversion.

```scss
body
{
	margin:10px + 10px;
}
```

Les opérateurs d'égalité (`==` et `!=`) sont également disponibles, ainsi que les opérateurs logiques (`and`, `or` et `not`).

#### Fonctions natives disponibles dans Sass

Sass possède également nativement une [liste impressionnante de fonctions](http://sass-lang.com/documentation/Sass/Script/Functions.html). Nous en verrons quelques unes dans la suite du cours mais en voici deux assez intéressantes.

##### percentage

Voici une fonction très utile lorsque vous faites du responsive web design pour calculer des pourcentages selon la formule "result = target / context".

Admettons que vous deviez coder de façon fluide un design réalisé sur une grille de 960px, avec un contenu principal à 600px, un gutter de 60px et un contenu secondaire de 300px. Plus besoin de votre calculatrice, vous pouvez utiliser ces valeurs directement dans Sass.

```scss
.content__primary
{
	float:left;
	width:percentage(600/960);
}

.content__secondary
{
	float:right;
	width:percentage(300/960);
}
```

##### Fonctions liées aux couleurs

Une fois que vous avez établi vos variables de base pour vos couleurs, vous pouvez utilisez Sass pour en générer d'autres sur cette base.

```scss
$color-accent:#F16C32;

.somediv
{
	background:lighten($color-accent, 10%);
}

.someotherdiv
{
	background:darken($color-accent, 20%);
}
```

Il existe [bien d'autres fonctions liées aux couleurs dans Sass](http://sass-lang.com/documentation/Sass/Script/Functions.html). N'hésitez pas à les découvrir par vous même.

### Fonctions

Vous pouvez également écrire vos propres fonctions dans Sass. Un exemple type consiste à calculer une taille de police spécifiée en pixels en em, avec une taille de texte de base spécifiée à 16px.

```scss
@function calc-em($target-px, $context) {
	@return ($target-px / $context) * 1em;
}

.page
{
	padding:calc-em(30px, 16px);
}

```

ce qui donne

```css
.page
{
	padding:1.875em;
}
```

Vous pouvez spécifier des arguments par défaut pour votre fonction en utilisant la notation suivante:

```scss
@function calc-em($target, $context:16px) {
	@return ($target / $context) * 1em;
}

.page
{
	padding:calc-em(30);
}
```

ou encore, en utilisant une variable:

```scss
$base-fontsize:16px;

@function calc-em($target, $context:$base-fontsize) {
	@return ($target / $context) * 1em;
}

.page
{
	padding:calc-em(30);
}
```

### Mixins: @mixin et @content

Les `@mixin` vous permettent simplement de réutiliser du code à différents endroits.

Un bon exemple pour une `@mixin` est par exemple le fait de spécifier une taille de police en `rem`. Certains navigateurs ne comprennent pas cette unité et il leur faut alors un fallback spécifié en `px`.

```scss
$base-fontsize:16px;

@mixin fontsize-rem($pixels)
{
	font-size:$pixels;
	font-size:($pixels / $base-fontsize) * 1rem;
}

.title-page
{
	@include fontsize-rem(48px);
}
```

ce qui produirait en CSS

```css
.title-page {
  font-size: 48px;
  font-size: 3rem; }
```

La directive `@content` permet d'envoyer des blocs de règles CSS à une `@mixin` pour qu'elles y soit incluses. Nous verrons plus loin un exemple avec des media queries.

### Extend et classes silencieuses

Via la directive `@extend`, Sass vous permet d'étendre des classes existantes assez facilement.

```scss
.btn
{
	display:inline-block;
	padding:1em;
	text-align:center;
	text-transform:uppercase;
}

.btn--alert
{
	@extend .btn;
	background:#9c3;
}
```

Sass va générer la CSS suivante

```css
.btn, .btn--alert {
  padding: 1em;
  text-align: center;
  text-transform: uppercase;
}

.btn--alert {
  background: #9c3;
}
```

Voici un autre exemple pour vous parler des classes silencieuses. Lorsque vous utilisez une classe `clearfix`, vus ne souhaitez pas que cette classe apparaisse dans votre css en tant que telle. Seules les classes qui l'étendent vous intéressent. Dans ce cas, il suffit d'utiliser les classes silencieuses dans Sass.


```scss
.clearfix
{
	&:after
	{
		content: "";
		display: table;
		clear: both;
	}
}


.navbar
{
	@extend .clearfix;
}

.content
{
	@extend .clearfix;
}
```

cela produirait le code suivant

```css
.clearfix:after, .navbar:after, .content:after {
  content: "";
  display: table;
  clear: both;
}
```

Or nous n'avons pas besoin de la classe `.clearfix:after` dans notre CSS. Cette classe ne sert qu'à être étendue. Nous pouvons donc réécrire notre sass en utilisant une classe silencieuse, préfixée avec "%" plutôt que ".".

```scss
%clearfix
{
	&:after
	{
		content: "";
		display: table;
		clear: both;
	}
}


.navbar
{
	@extend %clearfix;
}

.content
{
	@extend %clearfix;
}
```

ce qui produira

```css
.navbar:after, .content:after {
  content: "";
  display: table;
  clear: both;
}
```

### @extend ou @mixin ?

Vous vous posez peut-être la question suivante: quand dois-je utiliser `@extend` et quand dois-je utiliser `@mixin`. La règle de base est assez simple: si vous avez besoin de paramètres, utilisez `@mixin`. Si ce n'est pas le cas, utilisez `@extend`. Sachez aussi que `@extend` ne répétant pas le code de vos déclaration CSS, vous produirez un code plus DRY qu'avec `@mixin`.

### Media Queries avec la directive @media

Sass permet également de gérer efficacement les media queries via la directive `@media` et un mécanisme nommé "@media bubbling". Ce mécanisme vous permet d'écrire vos media queries imbriquées dans vos sélecteurs et Sass va se charger de les faire remonter (bubbling) pour vous dans le code CSS généré.

Si nous reprenons notre `@mixin` développée plus haut mais que nous voulons par exemple changer la taille de texte de nos titres suivant la taille d'écran de l'utilisateur, voici comment procéder.

```scss
.title-page
{
    @include fontsize-rem(32px);

    @media screen and (min-width: 1024px)
    {
        @include fontsize-rem(48px);
    }
}
```

Cela pose deux questions:

1. tout cela n'est pas très DRY puisque nous devons réécrire nos media queries à chaque fois. Nous verrons dans la suite que nous pouvons créer une `mixin` pour éviter le problème et nous faciliter la vie.
2. Est-ce que cela ne pose pas des problèmes de performance d'avoir toutes ces media queries identiques séparées les unes des autres plutôt que de les grouper comme on le fait lorsqu'on écrit sa CSS à la main. La réponse est que cela à une incidence, mais qu'elle est réellement minime par rapport aux gains de temps que nous procure cette façon de travailler.

Comme je sais que vous ne faites pas toujours confiance à vos professeurs, [voici un est pour vous le prouver](http://aaronjensen.github.io/media_query_test/).

### Structures de contrôle

Sass possède quelques structures de contrôle de base: `@if`, `@else`, `@for`, `@each` et `@while`. Plutôt que de les passer en revue, je vous invite à [consulter la documentation](http://sass-lang.com/documentation/file.SASS_REFERENCE.html#control_directives).

Nous allons plutôt utiliser ces structures de contrôle pour créer une `@mixin` complexe nous permettant de gérer efficacement nos media queries en Sass.

### Mixins complexes, directive @content, listes, structures de contrôle et directive @warn

Notre problème est donc de créer une `@mixin` efficace pour éviter de devoir répéter nos media queries à chaque fois dans notre code.

Une première possibilité est de simplement metre en place des media queries "nommées" et d'utiliser la directive `@content`, ainsi que quelques conditions.

```scss
@mixin mq($breakpoint-name)
{
    //medium screens: 750px
    @if (unquote($breakpoint-name) == "medium")
    {
        @media screen and (min-width:46.875em)
        {
            @content;
        }
    }
    //large screens: 1024px
    @else if (unquote($breakpoint-name) == "large")
    {
        @media screen and (min-width:64em)
        {
            @content;
        }
    }
    @else
    {
        @warn "#{$breakpoint-name} is not defined as a valid media query value";
    }
}
```

Cela nous permet d'écrire les media queries de la façon suivante dans nos fichiers `.scss`. Les règles CSS passées à la `@mixin` sont placées dans les blocs media grâce à la directive `@content`.

```css
.title-page
{
    font-size:2em;

    @include mq(large)
    {
        font-size:3em;
    }
}
```

Cependant, notre `@mixin` n'est pas encore très DRY, il y a beaucoup de code répété et ajouter une media query supplémentaire est encore assez complexe. Nous pouvons faire mieux en utilisant les listes en Sass.

```scss
$breakpoints-list:  "medium"    "(min-width:46.875em)",
                    "large"     "(min-width:64em)";

@mixin mq($mq-name)
    {
    @each $breakpoint in $breakpoints-list
    {
        $breakpoint-name:     nth($breakpoint, 1);
        $breakpoint-params:   nth($breakpoint, 2);

        @if(unquote($mq-name) == $breakpoint-name)
        {
            @media screen and #{$breakpoint-params}
            {
                @content;
            }
        }
    }
}
```

Il ne nous reste plus qu'à implémenter un message d'erreur informatif et l'objectif est rempli.

```scss
$breakpoints-list:  "medium"    "(min-width:46.875em)",
                    "large"     "(min-width:64em)";
                    
@mixin mq($mq-name)
{
    $breakpoint-defined: false;

    @each $breakpoint in $breakpoints-list
    {
        $breakpoint-name:     nth($breakpoint, 1);
        $breakpoint-params:   nth($breakpoint, 2);

        @if(unquote($mq-name) == $breakpoint-name)
        {
            $breakpoint-defined: true;

            @media screen and #{$breakpoint-params}
            {
                @content;
            }
        }
    }

    @if ($breakpoint-defined == false)
    {
        @warn "Breakpoint \"#{$mq-name}\" is not defined in your $breakpoint-list";
    }
}
```

## Ressources

- "[Why Sass?](http://alistapart.com/article/why-sass)" un bon article de Dan Cederholm sur A List Apart. Son live "[Sass for Web Designers](http://www.abookapart.com/products/sass-for-web-designers)" est également disponible via A Book Apart
- [Sass Basics](http://sass-lang.com/guide): une bonne petite ressource pour commencer ou si vous avez besoin de vous rafraîchir les idées
- Sass: [site officiel](http://sass-lang.com/) et [documentation](http://sass-lang.com/documentation/file.SASS_REFERENCE.html)
- [The Sass way](http://thesassway.com/): un bon ensemble d'articles publiés sur Sass
- [Une impressionnante liste de ressources](https://github.com/HugoGiraudel/awesome-sass) compilée par Hugo Giraudel
- [Mes quelques ressources personnelles concernant Sass](https://pinboard.in/search/u:jeromecoupe/?query=sass) archivées sur Pinboard