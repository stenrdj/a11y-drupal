# Guide de développeur Drupal pour Accessibilité web

#### Contenu 

 1. C'est quoi l'Accessibilité web ?
 2. L'Accessibilité sur Drupal 
 3. Les bonnes pratiques
 4. Outils D'audite pour Accessibilité
 

## C'est quoi l'Accessibilité web ?

L'accessibilité web c'est un ensemble des bonnes pratiques , pour les développeurs et designers à mettre en place dans le but de crée des sites web de haute qualité , et sans exclut les personnes âgées ou ayant des capacités diminuées à utiliser , comprendre , naviguer et interagir avec le web.

## L'Accessibilité sur Drupal 
Les développeurs du core Drupal ont mise des très grand effort a fin d'intégrer l'accessibilité dans leurs ecosysteme , introduisant l'internationalisation ,Forms API, jQuery UI ainsi incluant les bonnes pratiques ARIA sur le theme par defaut Batrik qui parfaitement respect les bonnes pratiques d'accessibilité . 

Le defi, c'est les modules de contribution ne respectent pas les règles d'accessibilité , le markup générer et la gestion d'erreur dans les modules ne sont pas accessible casiment .

## Les bonnes pratiques

 ### pour les développeurs back-end :

+ Utiliser * hook_form_alter * pour ajouter les tages *aria* aux éléments des formulaires.

+ Changer ou supprimer le message des liens "read more" sur les teasers des nodes á l'aide de  *hook_link_alter* .

+ Ajouter les attributs *aria* aux blocs grace au module [Block ARIA Landmark Roles](https://www.drupal.org/project/block_aria_landmark_roles).

+ Fournir aux utilisateurs un outil qui leurs permettre de changer la taille de texte , á l'aide de module [Text Resize](https://www.drupal.org/project/text_resize).   
+ Utiliser *Drupal.announce()* pour notifier les utilisateurs avec les "Lecteur d'Ecrans" les changements fait sur la page en AJAX ou JS .
+ Éviter le *Caputcha* le plus possible .
+ Ajouter un alt texte pour les images avec un texte qui décrit l'image .
+ Améliorer l'affichage des messages d'erreurs , par exemple: 

``` [X]Le champs Nom est incorrecte ``` 

``` [✓]Le champs Nom doit contenir que des lettres uniquement ```
> ### pour les développeurs front-end :
+ Associer un label avec tout éléments de form (input,select, textarea ..).

 ex:
```html
<label for="male">Male</label>
  <input type="radio" name="gender" id="male" value="male"><br>

```
+ Identifier la langue de la page , spécifiquement pour les sites multilangue.
+ Mettre en places les attributs *aria-* sur non-standard éléments, ( Slider , caroussel , list block).
 Ex :

	```
	role="menuItem"
	aria-checked="true" (pour les formulaires)
	aria-disabled="false" (pour les formulaires)
	aria-expanded="true" (ex : toggle menu)
	aria-labelledby="label" (pour les formulaires)
	aria-describedby="idDedescirption" (tout les elements)
	aria-required="true " (pour les formulaires)
	aria-hidden="true" (tout les elements)
	aria-current="page" (lien de navigation)
	aria-pressed="true" (button pressed)
	```

+ Assurer que tout les éléments interactive sont accessible par clavier.
	```
	 [✓]La touche ESC doit quitter le model ou popup.
	 [✓]La touche Tabulation doit changer dans un Ordre cohérent le focus entre les liens et éléments interactive JS.
	 [✓]Le model de Datepicket doit également permettre a l'utilisateur de saisi la date manuellement.
	 [✓]Tout les interaction JS (Ajax) doit etre lu par les lecteurs d'ecran.
	 [✓]éviter le max possible les évènements  suivantes: ondblclick,onmousedown,onmouseup,onfocus,onblur tant qu'ils n'ont  accessible par clavier ou lecteur d'ecran .
	 
	 ```

+ L'augmentation de la taille de texte ne doit pas impacter les autres éléments .
+ Fournir aux utilisateurs la possiblité de "Skip content" , passer d'un block vers un autre (Header ,navigation , footer , newsletter ..).
+ Éviter le plus possible **display: none** et remplacer par **aria-hidden** :
 	Ex : 
```html
<div class="text">
    <label id="tp1-label" for="first">First Name:</label>
    <input type="text" id="first" name="first" size="20"
           aria-labelledby="tp1-label"
           aria-describedby="tp1"
           aria-required="false" />
    <div id="tp1" class="tooltip"
         role="tooltip"
         aria-hidden="true">Your first name is optional</div>
</div>
```

	 Et en css : ( n'est supporter sur IE9)

```css
div[aria-hidden="true"] {display:none;}
div[aria-hidden="false"] {display:block;}
```

## Outils D'audite pour Accessibilité

[A11y.css](https://github.com/ffoodd/a11y.css)  : L’objectif de ce fichier CSS est notifier l’intégrateur sur les erreurs et risques potentiels dans le code .

[A11y Checker](https://muhnad.github.io/a11y-checker/)  : une bibliothéque javascript qui aide a détecter la none-conformité aux regles de WCAG.

[Gulp Accessibility ](https://github.com/yargalot/gulp-accessibility)  : une extension gulp qui permet de signaler les éléments qui respect pas les norme d'accissibilité .


