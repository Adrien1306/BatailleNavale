# BatailleNavale
Jeu de bataille navale

On consid�re 5 types de navires:
- porte avion long=5
- croiseur long=4
- fr�gate long=3
- sous-marin long=3
- escorteur long=2 (x2)

La grille fait 8x8.

Chaque navire est positionn� par un point de d�part D(x,y) et un point d'arriv�e A(x,y).

Le joueur distant est identifi� par un nom de machine sur le r�seau.
A l'initialisation, le premier joueur envoyant une commande donne automatiquement la main (jeton) � l'autre joueur.

Fonctionnement:
LE joueur d�bute la partie 
La liaison doit �tre v�rifi�e avant d'accepter l'envoi de chaque 'coup'.
Un coup doit �tre v�rifi� avant d'�tre �mis:
- pas de rejeu (en option, on peut ult�rieurement accepter un coup d�j� jou�)
- dans la grille (0<x<9, 0<y<9)
Un message retour informe le joueur que la commande est bien pass�e et pr�cise le r�sultat du coup:
- dans l'eau
- touch�
-coul� (avec le type de b�teau)
- fin de partie (tous b�teaux coul�s)

Structure:
* classe connexion
G�re l'�tat de la liaison:
- nom destinataire
- �tat du lien r�seau (disponible ou cass�)
- �tat du serveur distant (r�pond ou pas - plusieures tentatives avant de conclure)
- op�ration en cours (�tablissement du lien, v�rification du lien, idem pour le serveur distant)
- produire une synth�se utilis�e par l'objet Affichage.
- produire un warning � usage de l'objet Action.
- indication � disposition du joueur distant que notre grille est disponible 'ready'

* classe grille
G�re l'�tat du jeu:
- initialisation des grilles joueur1 et joueur2
	. interface utilisateur (saisie des positions des b�teaux via leurs identifiants)
	. respect des r�gles (position, dimension, superposition)
- �tablissement d'un coup (client)
	. saisie et contr�le de sa validit�
	. attendre la confirmation de sa prise en compte
	. affichage et mise � jour
	(apr�s d�finition du coup, apr�s r�ception du coup adversaire:
	si impact, placer T dans la case ou C dans chaque case du b�teau)
- r�ception d'un coup (serveur)
	. analyse du coup et impact (dans l'eau, touch�, coul�)
	. envoi du message impact vers l'adversaire
	. affichage grille et effet constat� (log ou popup)'

* classe b�teau
G�re l'�tat d'un b�teau
- identifiant (List)
- longueur
- positions m�moris�es ? (peut-�tre que l'info dans la grille est suffisant)
- �tat pour chaque position (intact, touch�)
- �tat global (coul�: compteur = longueur puis d�cr�mente si touch�)
