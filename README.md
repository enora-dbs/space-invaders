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
nous avons creer le __main__ et nous avons commmencer a creer la classe pour les ennemis

le vendredi 2/04/21
nous avons continuer la class pour les ennemis et nous allons commencer a creer le joueur qui sera representé par un canon

le mardi 5/04/21
j'avais oublier de le marquer sur le readme, mais nous avons creer une fonction qui va permettre d'enregistrer le meilleur score
avec un def SaveMeilleurScore. J'ai egalement defini le score de départ = 0

le jeudi 8/04/21
J'ai decider d'ameliorer la fonction def SaveMeilleurScore avec une autre fonction pour pouvoir afficher le nouveau score.
J'utilise un def LoadMeilleurScore (j'ai trouvé ce def sur internet). 
Comme jusqu'a present je n'ai pas rencontrer d'erreurs avec, j'ai decider d'utiliser un global.
J'ai creer un  def existe afin de verifier l'existence d'un fichier, et pour m'en servir pour definir le score de depart.
Pour le moment mon programme ne m'affiche pas d'erreur mais je n'arrive pas encore a interagir avec le jeu.


evolution de notre programme: 
from tkinter import *
from random import *
import pickle

# Cette fonction affiche l'écran de présentation du jeu
def EcranDePresentation():
    global DebutJeu
    if DebutJeu!=1:
        AffichageScore.configure(text="",font=('Fixedsys',16))
        AffichageVie.configure(text="",font=('Fixedsys',16))
        can.delete(ALL)
        fen.after(1500,Titre)
        
#creation de la class pour les ennemi
class Ennemi():

    def __init__(self,x,y,direction,ennemiType):

        self.EnnemiType = ennemiType
        self.Direction = direction

        if ennemiType == 1:
            ennemiImage = pygame.image.load("invader1.jpge")
            self.Speed = 1
            self.Score = 5

        if ennemiType == 2:
            ennemiImage = pygame.image.load("invader2.png")
            self.Score = 10
            self.Speed = 1
            
    def moveEnnemi(self):
        if self.Direction == "right":
            self.rect.x += self.Speed
        
        if self.Direction == "left":
            self.rect.x -= self.Speed

#definir les fonctions       
def right(event):
    # Modification de la variable globale direction
    global direction
    direction = 'right'
    
def left(event):
    # Modification de la variable globale direction
    global direction
    direction = 'left'
    
def tir_joueur(event):
    # Modification de la variable globale direction
    global direction
    direction = 'tir_joueur'
    
def pause(event):
    # Modification de la variable globale direction
    global direction
    direction = 'pause'
        
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
    can.bind_all("<p>",pause)

# on verifie l'existence d'un fichier

    def existe(fname):
        try:
            f=open(fname,'r')
            f.close()
            return 1
        except:
            return 0

# on defini le score de départ avec la valeur 0

if existe('HighScore')==0: 
    FichierScore=open('HighScore','w')
    pickle.dump(0,FichierScore)
    FichierScore.close()

# Cette fonction va permettre d'enregistrer le meilleur score

    def SaveMeilleurScore(resultat):
        FichierScore=open('HighScore','r')
        if resultat>lecture:
            FichierScore=open('HighScore','w')
            pickle.dump(resultat,FichierScore)
            FichierScore.close()
            fen.after(2000,MessageRecord)
        else:
            fen.after(15000,EcranDePresentation)
        FichierScore.close()
    
    def LoadMeilleurScore():
        global DebutJeu
        if DebutJeu!=1:
            FichierScore=open('HighScore','r')
            lecture=pickle.load(FichierScore)
            can.delete(ALL)
            can.create_text(320,240,font=('Fixedsys',24),text="HIGH SCORE",fill='purple')
            can.create_text(320,270,font=('Fixedsys',24),text=str(lecture),fill='purple')
            FichierScore.close()
        fen.after(3000,EcranDePresentation)

    
    can.grid(row=1,column=0,columnspan=2,rowspan=3)
    
    Ennemi()
    EcranDePresentation()
    afficherScore=[]
    fen.mainloop()
