# space-invaders

ce projet à pour objectif de creer le jeu space invaders

les commandes qui vont etre utiliser sont:
-pour tirer: la barre d'espace
-diriger le canon: les fleches
-faire pause: lettre p

les imports qui vont nous etre utiles sont les suivants:
from random import *


la premiere fonction que je vais coder est celle ui va servir à afficher l'écran de présentation du jeu, avec un 
def EcranDePresentation():
pour cela j'ai utiliser 'global DebutJeu' et j'ai defini la variable 'DebutJeu = 0'

j'ai egalement commencé à créé un bouton 'commencer' et un bouton 'quitter'

le 29/03/21 
nous avons Défini des touches qui vont permettre de diriger le canon mobile: Right, Left, space pour tirer et p pour pause
pour cela nous avons du definir les fonctions

le jeudi 1/04/21
nous allons creer le __main__


evolution de notre programme: 
from tkinter import *
from random import *

# Cette fonction affiche l'écran de présentation du jeu
def EcranDePresentation():
    global DebutJeu
    if DebutJeu!=1:
        AffichageScore.configure(text="",font=('Fixedsys',16))
        AffichageVie.configure(text="",font=('Fixedsys',16))
        can.delete(ALL)
        fen.after(1500,Titre)
        
#definir les fonctions       
def right(event):
    # Modification de la variable globale direction
    global direction
    direction = 'right'
    
def left(event):
    # Modification de la variable globale direction
    global direction
    direction = 'left'
    
def down(event):
    # Modification de la variable globale direction
    global direction
    direction = 'down'
    
def up(event):
    # Modification de la variable globale direction
    global direction
    direction = 'up'
        
if __name__ == "__main__":
    #defini la variable DebutJeu
    DebutJeu = 0
    #créé un bouton 'commencer' et un bouton 'quitter'
    fenetre = Tk()
    bouton=Button(fenetre, text="commencer", command=fenetre.quit).pack(side=LEFT, padx=50, pady=5)
    bouton2=Button(fenetre, text="quitter", command=fenetre.quit).pack(side=RIGHT, padx=50, pady=5)
    
    
    # Création de la fenêtre principale
    
    fen=Tk()
    
    # Titre de la fenêtre
    
    fen.title('Space invaders')
    
    # Définition du canevas ( Ecran de jeu )
    
    can=Canvas(fen,width=640,height=480,bg='black')
    
    # Définition des touches qui vont permettre
    # de diriger le canon mobile
    
    can.bind_all("<Right>",right)
    can.bind_all("<Left>",left)
    can.bind_all("<space>",tir_joueur)
    can.bind_all("<p>",time.pause)
    
    can.grid(row=1,column=0,columnspan=2,rowspan=3)
    

