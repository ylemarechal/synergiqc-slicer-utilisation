{% include toc.html html=content %}

## Utilisation de slicer pour les annotations

Slicer est utilisé comme plateforme d'annotation des images. 

## Démarrage

Pour lancer Slicer, une icône se trouve sur le bureau ou via le menu démarrer sur windows ou avec 
stoplight sur mac (pomme + espace).

{% include figure.html img="img/slicer_bureau.PNG" caption="Icone Slicer sur le bureau" %}

Une fois démarré, vous arrivez sur la page d'accueil de slicer 

![Image](img/slicer_accueil.PNG)
{% include figure.html img="img/slicer_accueil.PNG" caption="Icone Slicer sur le bureau" %}

## Récupérer des images

Pour charger les images, il faut utiliser le module dicomweb, accessible via la recherche (loupe).

![Image](img/slicer_loupe.PNG)

Il suffit de rechercher le module souhaité dans le menu déroulant, ou en écrivant son nom, ici ````dicomweb````

![Image](img/slicer_dicomweb.PNG)

Il ne reste plus qu'à double-cliquer ou à cliquer sur ````Switch to module````.
Sur le bandeau de gauche, il y a le bouton ````Show browser```` pour accéder aux données.

![Image](img/slicer_dicomweb_menu.PNG)

Dans la partie ````Server url````, il faut renseigner l'url fournie à la première utilisation et est enregistrée ensuite.


![Image](img/slicer_dicomweb_url.PNG)

{% include note.html content="Le bouton ````Use cached server response```` est coché par défaut pour charger plus rapidement la liste, mais ne la met pas forcément à jour. Ne pas oublier de la décocher si le patient souhaité n'est pas trouvé. Le temps de réponse peut être très long et slicer peut sembler ne plus répondre." %}

La partie ````Studies```` affiche l'ensemble des études disponibles. En cliquant sur une en particulier, les séries 
associées s'affichent. Il est possible de filtrer à l'aide de la partie ````Filter````. Ce filtre s'applique sur toutes 
les colonnes de la partie ````Studies````. Après avoir sélectionné la ou les séries ou études souhaitées, il faut les 
récupérer localement via le bouton de téléchargement (entouré en rouge dans l'image ci-dessous). Le bouton entouré en 
récupère également et le charge dans slicer directement. Dans l'exemple ci-dessous, au niveau des séries, la série 1 est
présente localement, représenté par l'icone cylindrique, la ligne 2 est en cours de téléchargement et les lignes 3-6 ne 
sont présentes que sur le serveur. Une fois les images récupérées on peut fermer cette fenêtre.

![Image](img/slicer_dicomweb_chargement.PNG)

## Charger des images

Pour aller dans la base d'images locales, il suffit de cliquer sur le bouton ````dcm````

![Image](img/slicer_dicom.PNG)

Pour charger une série CT, il faut sélectionner le patient, puis l'étude et enfin la série concernée puis cliquer sur ````load````.

![Image](img/slicer_dicom_studies.PNG)

La série devrait s'afficher, et la série chargée sur la partie gauche.
{% include warning.html content="Vérifier qu'il n'y ait qu'une seule étude chargée afin de ne pas risquer de mélanger les patients. Si une série non voulue est chargée, il suffit de faire un clic droit et delete" %}

![Image](img/slicer_dicom_serie_chargee.PNG)


## Contourages

Une fois chargé, le TDM apparait à droite. Il reste à charger le module ````Quantitative Reporting````
{% include figure.html img="img/slicer_module_qr.PNG" %}

Pour une nouvelle segmentation, dans ````Mesurement report````, il faut créer une nouvelle table et dans ````Master volume````
sélectionner le volume à contourer. Il ne devrait y en avoir que un.

{% include figure.html img="img/slicer_qr_new.PNG" %}

Ensuite on peut rajouter une nouvelle segmentation. 
{% include figure.html img="img/slicer_qr_add.PNG" %}

Une fois une nouvelle segmentation générée, on peut segmenter directement sur le CT en sélectionnant le pinceau (en rouge)
dans la figure ci-dessous et le diamètre de peinture (en bleu sur la figure). 

{% include figure.html img="img/slicer_qr_segmentation.PNG" %}

Pour changer le fenêtrage de l'image, il suffit de cliquer sur l'icone en haut de l'écran (en rouge sur la figure ci-dessous)
et changer les options en déplaçant la sourir avec le clic gauche enfoncé. Pour revenir à la navigation par souris, il suffit de 
sélection le curseur (bleu sur la figure).
{% include figure.html img="img/slicer_ct_fenetrage.PNG" %}

En cliquant sur la couleur à gauche du nom de l'organe, on arrive à l'outil de selection du nom et de la couleur de segmentation
{% include figure.html img="img/slicer_qr_list_organ.PNG" %}

Le contourage apparait sur les 3 dimensions du CT en surimpression.
{% include figure.html img="img/slicer_qr_contour.PNG" %}

Une fois terminé, il suffit de cliquer sur ````Complete Report````
{% include figure.html img="img/slicer_qr_contour.PNG" %}

Il sera demandé de valider les métadonnées concernant la segmentation.
{% include figure.html img="img/slicer_qr_save_option.PNG" %}


## Envoyer un examen

Pour envoyer des images, il suffit d'aller dans le module ````dcm```` en haut à gauche de Slicer, de sélectionner les 
examens à envoyer, et faire un clic droit ````Send to dicom server````. Ensuite il faut sélectionner le protocole
````DICOMweb```` et inscrire l'adresse de destination fournie. 

## Générer un lien pour récupérer les images

Pour générer un lien depuis un album de Kheops, il faut aller dans la section réglages
{% include figure.html img="img/kheops_reglages.PNG"  %}

Puis aller dans la section ````token```` et cliquer sur ````Nouveau token````
{% include figure.html img="img/kheops_reglages_token.PNG" %}

Il ne reste plus qu'à choisir les options. Dans notre cas, il faut choisir en lecture et écriture
{% include figure.html img="img/kheops_nouveau_token.PNG" %}

Le lien d'accès apparaitra et sera de type https://url/view/AbC123CDDSGXXX. Pour pouvoir l'utiliser dans Slicer, il faut
remplacer la partie ````view```` par ````api/link```` dans le lien.
