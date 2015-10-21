# Introduction à Sass

[Sass](http://sass-lang.com/) est un préprocesseur CSS qui compile et transforme votre code Sass en code CSS. CSS est au départ un language simple et de nature purement déclarative. Sass vous permet d'étendre les possibilités du language CSS en utilisant des éléments de programmation.

- variables, listes, maps
- fonctions
- operations (mathématiques, couleurs, etc.)
- structures de controles (`@if`, `@for`, `@each` et `@while`)

Sass vous permet également de gérer plus efficacement votre code CSS et de ne pas vous répéter inutilement.

- nesting
- `@mixins`
- `@extend`
- `@media`
- `@import`

Attention cependant, Sass n'est pas une technologie qui vous fera magiquement écrire du code CSS propre et optimisé. Le prérequis est de bien connaître CSS d'abord et d'être toujours attentif au code généré. Sass est un outil qui peut vous faciliter la vie mais ce qui importe, en fin de compte, c'est le code CSS généré.

A mon sens, les avantages de Sass sont:

- A travers les mixins, les fonctions, les variables et `@extend` Sass vous permet de réutiliser votre code dans le cadre de plusieurs projets.
- Utiliser `@import` vous permet également de simplifier la maintenance de vos projets CSS en travaillant à l'aide de fichiers séparés et hiérarchisés
- Sass vous permet de compresser automatiquement vos fichiers CSS, les rendant plus légers à transférer vers les navigateurs de vos utilisateurs.

Nous verrons plus loin que, grâce à sa syntaxe `scss`, Sass est entièrement compatible avec le language CSS que vous connaissez déjà. Autrement dit, prenez un fichier CSS existant et changez son extension de fichier en `.scss` et vous écrivez du Sass. Cela rend cette technologie facile à apprendre et vous permet de l'adopter petit à petit dans vos projets.

Sass dépend de [Ruby](https://www.ruby-lang.org/). Cela ne veut pas pour autant dire que vous devez maîtriser ce language pour utiliser Sass. De la même manière, même si Sass peut être entièrement géré depuis votre terminal en lignes de commande, vous n'êtes pas obligés de suivre cette voie. Il existe de très bons programmes GUI vous permettant d'utiliser Sass sans pour autant devoir recourir à votre terminal (voir suite).

## Deux syntaxes

Vous pouvez utiliser deux syntaxes différentes pour écrire vos fichiers: la syntaxe `scss` et la syntaxe indentée ou `Sass` plus ancienne.

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

Vous remarquerez que les fichiers CSS sont générés avec un certain style d'output. Il en existe 4 différents avec sass:

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

Si ces quelques lignes de commande vous rebutent, vous pouvez également utiliser des applications GUI qui feront le travail pour vous. Il en existe beaucoup et même si [Scout](http://mhs.github.io/scout-app/) (Mac et Windows) et [CodeKit](http://incident57.com/codekit/) (Mac) sont sans doute les plus connus [il en existe d'autres](http://sass-lang.com/install).

Les outils de build ou task runners que sont [Grunt](http://gruntjs.com/) et [Gulp](http://gulpjs.com/) permettent également de compiler du code Sass en CSS.

## Concepts

Maintenant que nous avons installé Sass et que nous avons un workflow, pratiquons un peu.

### Imports et partials

`@import` vous permet d'importer des fichiers Sass les uns dans les autres et ainsi de structurer efficacement votre projet CSS. Cette fonctionnalité prend tout son sens lorsque vous travaillez sur des projets de grande taille et relativement complexe.

Habituellement, vos fichiers sont structurés de telle manière que votre fichier Sass principal ne contienne que des directives `@import`. Vous pouvez préfixer le nom des fichiers importés avec `_` de manière à ce que Sass ne les compile pas directement.

Voici, par exemple, une structure possible pour vos fichiers Sass dans le cadre d'un projet plus complexe. Un [boiletrplate et des expications détaillées sont disponibles](http://sass-guidelin.es/#the-7-1-pattern) sur le site Sass Guildelines.

```
base/
	_base.scss
	_typography.scss
components/
	_banners.scss
	_buttons.scss
	_icons.scss
	_links.scss
	_lists.scss
	_media.scss
	_modules.scss
layout/
	_grid.scss
	_main.scss
	_header.scss
	_footer.scss
pages/
	_home.scss
	_contact.scss
themes/
	_default.scss
utils/
	_variables.scss
	_functions.scss
	_mixins.scss
	_helpers.scss
	_cssobjects.scss
vendors/
	normalize.scss

screen.scss
```

### Variables, Listes et maps

Les variables, les listes et les maps sont sans doute les fonctionnalités de Sass que vous intégrerez le plus facilement à votre workflow existant.

#### Variables

Qui n'a jamais rêvé en CSS de pouvoir travailler avec des variables pour les couleurs de la charte graphique utilisée ? C'est désormais possible en Sass.

```scss
$color-gray-light1: 	#FBFBFB;
$color-gray-light2: 	#F8F8F8;
$color-gray-light3: 	#E5E5E5;
$color-gray-light4: 	#C9C9C9;

$color-gray-dark1: 	  #9D9D9D;
$color-gray-dark2: 	  #595959;
$color-gray-dark3: 	  #2F2F2F;
$color-gray-dark4: 	  #221F1F;

$color-brand-primary:   #FFED00;
$color-brand-secondary: #00ABE7;

body
{
	background: $color-gray-light1;
	color: $color-gray-dark3;
}

a
{
	color: $color-brand-secondary;
}
```

*Exercice: créer un fichier _variables.scss, définissez quelques variables pour les couleurs et importez-le dans votre fichier Sass principal. Tant que vous y êtes, voyez comment vous pouvez appliquer cette logique pour d'autres choses (comme par exemple [utiliser des listes](https://speakerdeck.com/hugogiraudel/three-years-of-purging-sass) pour vos font-stacks).*

#### Listes

Les listes sont un bon moyen de créer des variables complexes en Sass, qui offre différents fonctions spécifiques aux listes pour les exploiter au mieux. Nous en verrons un exemple un peu plus loin.

En gros vous pouvez créer des listes simples ou des listes imbriquées dans Sass. Vous pouvez utiliser ou des virgules ou des espaces comme séparateurs.

```scss
$fruits-espaces:    "pomme" "poire" "orange";
$fruits-virgules:   "pomme", "poire", "orange";
$fruits-ideal:      ("pomme", "poire", "orange");
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

Sass possède [de nombreuses fonctions](http://sass-lang.com/documentation/Sass/Script/Functions.html) vous permettant de manipuler des listes. Celles-ci sont similaires à ce que vous pouvez trouver dans d'autres langages de programmation.

#### Maps

Les maps sont un outil un peu plus avancé que les listes. Ce sont essentiellement ce que l'on appelle des tableaux associatifs dans d'autres langauges de programmation. Les maps associent des clefs à des valeurs.

Contrairement aux listes, les maps sont toujours entourées par des parenthèses, `:` est utilisé pour séparer les clefs des valeurs et des `,` sont utilisées pour séparer les groupes de clefs et de valeurs.

```
$map:
(
  key: value,
  other-key: other-value
);
```

tout comme les listes, les maps peuvent également être imbriquées si besoin est.

```
$nested-map:
(
  key: (
		nested-key1: nested-value1,
		nested-other-key1: nested-other-value1
	),
	other-key: (
		nested-key2: nested-value2,
		nested-other-key2: nested-other-value2
	)
);
```

L'inévitable Hugo Giraudel propose un bon [article d'introduction à l'utilisation des maps](http://www.sitepoint.com/using-sass-maps/) sur SitePoint.

Sass possède [de nombreuses fonctions](http://sass-lang.com/documentation/Sass/Script/Functions.html) vous permettant de manipuler des maps. Les listes conviennent surtout pour stocker des données assez simples tandis que les maps conviennent d'avantage au stockage de données plus complexes. Il est en général plus facile de manipuler les maps que les listes.

### Nesting et l'opérateur "&"

Sass vous permet d'imbriquer vos sélecteurs CSS. Dans certain cas c'est bien utile, mais cela peut également dégénérer très rapidement.

Je vous conseille donc de ne pas en abuser et de vous limiter à imbriquer uniquement ce qui peut l'être sans risque, comme les pseudo-éléments et les pseudo-classes par exemple.

L'opérateur "&" est utile dans ce contexte puisqu'il permet de référencer le sélecteur parent. Voici un exemple de nesting raisonnable et d'utilisation de "&" dans Sass pour un menu de navigation.

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
}

.navbar__item > a
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
}

.navbar__item--current > a,
.navbar__item--current > a:hover
{
  background:#F16C32;
  color:#020202;
}
```

compilé cela donne

```css
.navbar {
  width: 100%;
  list-style: none;
  margin: 0;
  padding: 0;
  background: #000;
}

.navbar__item {
  display: inline-block;
}

  .navbar__item > a {
    display: block;
    padding: .5em 1em;
    background: #000;
    color: #ccc;
    text-decoration: none;
    text-transform: uppercase;
  }

    .navbar__item > a:hover {
      background: #333;
      color: #fff;
    }

  .navbar__item--current > a, .navbar__item--current > a:hover {
    background:#F16C32;
    color:#020202;
  }
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

Deux articles intéressants concernant le nesting avec Sass: "[the inception rule](http://thesassway.com/beginner/the-inception-rule/)" et "[Avoid nested selectors for more modular CSS](http://thesassway.com/intermediate/avoid-nested-selectors-for-more-modular-css/)".

### Commentaires

A ce stade vous allez sans doute commencer à avoir besoin de commentaires. Voici les différents types de commentaires existants dans Sass:

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

Les [opérateurs mathématiques de base](http://sass-lang.com/documentation/file.SASS_REFERENCE.html#number_operations) (`-`, `+`, `*` et `/`) sont disponibles.

Pour éviter les problèmes, travaillez toujours avec des nombres sans unités et faites intervenir les unités en dernier lieu via une simple multiplication ou

```scss
// add a unit
div
{
	margin: 87 * 1px; // Output: 87px
}

// remove a unit
div
{
	margin: 87px / 1px; // Output: 87
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
	float: left;
	width: percentage(600/960);
}

.content__secondary
{
	float: right;
	width: percentage(300/960);
}
```

##### Fonctions liées aux couleurs

Une fois que vous avez établi vos variables de base pour vos couleurs, vous pouvez utilisez Sass pour en générer d'autres sur cette base. Il est préférable d'utiliser la fonction `mix` avec du noir et du blanc plutôt que d'utiliser les fonctions `lighten` et `darken` qui sont beaucoup moins fines ([Merci Hugo](http://sass-guidelin.es/#lightening-and-darkening-colors)).

```scss
$color-accent: #F16C32;

.somediv
{
	background: lighten($color-accent, 10%);
}

.someotherdiv
{
	background: darken($color-accent, 20%);
}
```

Il existe [bien d'autres fonctions liées aux couleurs dans Sass](http://sass-lang.com/documentation/Sass/Script/Functions.html). N'hésitez pas à les découvrir par vous même.

### Fonctions

Vous pouvez également écrire vos propres fonctions dans Sass. Un exemple type consiste à calculer une taille de police spécifiée en pixels en em, avec une taille de texte de base spécifiée à 16px.

```scss
@function calc-em($sizeinpixels, $basefont)
{
  @return $sizeinpixels / $basefont * 1em;
}

.page
{
	padding: calc-em(30px, 16px);
}

```

ce qui donne

```css
.page
{
	padding: 1.875em;
}
```

Vous pouvez spécifier des arguments par défaut pour votre fonction en utilisant la notation suivante:

```scss
@function calc-em($sizeinpixels, $basefont:16px)
{
  @return $sizeinpixels / $basefont * 1em;
}

.page
{
	padding: calc-em(30);
}
```

### Mixins: `@mixin` et `@content`

Les `@mixin` vous permettent simplement de réutiliser du code à différents endroits.

Un bon exemple pour une `@mixin` est par exemple le fait de spécifier une taille de police en `rem`. Certains navigateurs ne comprennent pas cette unité et il leur faut alors un fallback spécifié en `px`.

```scss
@mixin fontsize-rem($pixels)
{
	font-size: $pixels;
	font-size: ($pixels / 16px) * 1rem;
}

.title-page
{
	@include fontsize-rem(48px);
}
```

ce qui produirait en CSS

```css
.title-page
{
  font-size: 48px;
  font-size: 3rem;
}
```

La directive `@content` permet d'envoyer des blocs de règles CSS à une `@mixin` pour qu'elles y soit incluses. Nous verrons plus loin un exemple avec des media queries.

### Extend et classes silencieuses

Via la directive `@extend`, Sass vous permet d'étendre des classes existantes assez facilement.

```scss
.btn
{
	display: inline-block;
	padding: 1em;
	text-transform: uppercase;
}

.btn--alert
{
	@extend .btn;
	background: #ff0000;
}
```

Sass va générer la CSS suivante

```css
.btn, .btn--alert {
  padding: 1em;
  text-transform: uppercase;
}

.btn--alert {
  background: #ff0000;
}
```

Très souvent, `@extend` est utilisé en combinaison avec ce que l'on appelle les classes silencieuses ou les placeholders. Ces classes  silencieuses ne sont pas transcrites dans la CSS compilées. Les règles CSS liées à cette classes silencieuse n'existeront dans la CSS compilée qu'à partir du moment où elles sont utilisées par `@extend`.

```scss
%btn
{
	display: inline-block;
	padding: 1em;
	text-transform: uppercase;
}

.btn--alert
{
	@extend %btn;
	background: #ff0000;
}

.btn--success
{
	@extend %btn;
	background:#00ff00;
}
```

Sass va générer la CSS suivante

```css
.btn--alert, .btn--success {
	display: inline-block;
	padding: 1em;
	text-transform: uppercase;
}

.btn--alert {
  background: #ff0000;
}

.btn--success {
  background: #00ff00;
}
```

### Quand utiliser `@extend` ?

[Comme le fait assez justement remarquer Harry Roberts](http://csswizardry.com/2014/11/when-to-use-extend-when-to-use-a-mixin/), `@extend` créée des relations entre vos sélecteurs, ce qui peut [créer des problèmes et même être contre-productif](http://www.smashingmagazine.com/2015/05/extending-in-sass-without-mess/) dans le cas d'une utilisation non réfléchie.

Il est fortelent conseillé d'utiliser `@extend` avec parcimonie et d'entendre uniquement des classes silencieuses dans le cadre de relations explicites entre sélecteurs lorsque ces derniers partagent des règles CSS de façon claire (comme dans l'exemple des boutons donné plus haut).

Dans tous les autres cas où vous souhaitez simplement éviter les répétitions, il est préférable d'utiliser des variables ou des mixin sans arguments.

### Media Queries avec la directive `@media`

Sass permet également de gérer efficacement les media queries via la directive `@media` et un mécanisme nommé "`@media` bubbling". Ce mécanisme vous permet d'écrire vos media queries imbriquées dans vos sélecteurs et Sass va se charger de les faire remonter (bubbling) pour vous dans le code CSS généré.

```scss
body
{
    background-color: red;

    @media all and (min-width: 750px)
    {
        background-color: red;
    }
}
```

Ce qui donnera en CSS une fois compilé

```css
body
{
  background-color: red;
}

@media all and (min-width: 750px)
{
	body
	{
		background-color: red;
	}
}
```

Cela pose deux questions:

1. tout cela n'est pas très DRY puisque nous devons réécrire nos media queries à chaque fois. Nous verrons dans la suite que nous pouvons créer une `mixin` pour éviter le problème et nous faciliter la vie.
2. Est-ce que cela ne pose pas des problèmes de performance d'avoir toutes ces media queries identiques séparées les unes des autres plutôt que de les grouper. La réponse est que cela à une incidence, mais qu'elle est réellement minime par rapport aux gains de temps que nous procure cette façon de travailler.

Comme je sais vous ne faites pas toujours confiance à vos professeurs, [voici un est pour vous le prouver](http://aaronjensen.github.io/media_query_test/). Ce test ne prend pas en compte le fait que les fichiers CSS sont en général utilisées avec Gzip qui ne fait qu'une bouchée des chînes de caractères répétées de nombreuses fois dans une stylesheet. La différence entre les deux approches est donc plus que négligeable.

### Structures de contrôle

Sass possède quelques structures de contrôle de base: `@if`, `@else`, `@for`, `@each` et `@while`. Plutôt que de les passer en revue, je vous invite à [consulter la documentation](http://sass-lang.com/documentation/file.SASS_REFERENCE.html#control_directives).

Nous allons maintenant utiliser ces structures de contrôle pour créer une `@mixin` un peu plus complexe nous permettant de gérer efficacement nos media queries en Sass.

### Mixins complexes, directive @content, listes, structures de contrôle et directive @warn

Notre problème est de créer une `@mixin` efficace pour éviter de devoir répéter nos media queries à chaque fois dans notre code.

Une première possibilité est de simplement metre en place des media queries "nommées" et d'utiliser la directive `@content`, ainsi que quelques conditions.

```scss
@mixin mq($breakpoint-name)
{
	$breakpoint-name: unquote($breakpoint-name);
  //medium screens: 750px
  @if ($breakpoint-name == "medium")
  {
    @media screen and (min-width: 46.875em)
    {
      @content;
    }
  }
  //large screens: 1024px
  @else if ($breakpoint-name == "large")
  {
    @media screen and (min-width: 64em)
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
body
{
  background-color: red;

  @include mq("large")
  {
      background-color: red;
  }
}
```

Cependant, notre `@mixin` n'est pas encore très DRY. Beaucoup de code est répété et ajouter une media query supplémentaire est encore assez complexe. Nous pouvons faire mieux en utilisant les maps en Sass.

```scss
$breakpoints: (
	medium: "(min-width:46.875em)",
  large: "(min-width:64em)"
);

@mixin mq($breakpoint-name)
{
	$breakpoint-name: unquote($breakpoint-name);
	@if map-has-key($breakpoints, $breakpoint-name)
	{
		$query: @map-get($breakpoints, $breakpoint-name)
		@media all and #{$query}
		{
			@content;
		}
	}
}
```

Il ne nous reste plus qu'à implémenter un message d'erreur informatif et l'objectif est rempli.

```scss
$breakpoints: (
	medium: "(min-width:46.875em)",
  large: "(min-width:64em)"
);

@mixin mq($breakpoint-name)
{
	$breakpoint-name: unquote($breakpoint-name);
	@if map-has-key($breakpoints, $breakpoint-name)
	{
		$query: @map-get($breakpoints, $breakpoint-name)
		@media all and #{$query}
		{
			@content;
		}
	}
	else
	{
		@warn "#{$mq-name} is not a value defined in the 'breakpoints' map.";
	}
}
```

## Ressources

- "[Why Sass?](http://alistapart.com/article/why-sass)" un bon article de Dan Cederholm sur A List Apart. Son livre "[Sass for Web Designers](http://www.abookapart.com/products/sass-for-web-designers)" est également disponible via A Book Apart
- [Sass Basics](http://sass-lang.com/guide): une bonne petite ressource pour commencer ou si vous avez besoin de vous rafraîchir les idées
- Sass: [site officiel](http://sass-lang.com/) et [documentation](http://sass-lang.com/documentation/file.SASS_REFERENCE.html)
- [The Sass way](http://thesassway.com/): un bon ensemble d'articles publiés concernant Sass
- [Une impressionnante liste de ressources](https://github.com/HugoGiraudel/awesome-sass) compilée par Hugo Giraudel
- [Sass guidelines](http://sass-guidelin.es/) Bonnes pratiques et super infos sur la structuration des projets Sass. Merci Hugo Giraudel!
- [Three years of purging Sass](https://speakerdeck.com/hugogiraudel/three-years-of-purging-sass): Quelques astuces pour éviter les pièges en écrivant du code Sass par le désormais célèbre Hugo Giraudel.
- [Mes quelques ressources personnelles concernant Sass](https://pinboard.in/search/u:jeromecoupe/?query=sass) archivées sur Pinboard
