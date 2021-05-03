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

Le lundi 03/05/21
Pendant les vancances, j'a renconter quelque difficulter avec mon programme, j'ai donc decider de le recommencer.
J'ai commmencer par modifier les import, j'ai decider d'utiliser un import turtle et un import os et d'enlever les tkinter.
Je me suiis rendu compte que cherchais à faire quelque chose de trop compliqué. J'ai donc décider de faire un programme plus simple, mais plus effectif.
J'ai commencer par créé l'ecran d'acceuil et le joueur, et faire bouger le joueur de gauche à droite.
J'ai rencontré quelque probleme avec le cannon, mais j'ai réussi à me débloquer grace à l'aide de mon père.
Mes inspirations principales sont, la chaine TokyoEdtech sur youtube, ansi qu'un programme sur internet dont je ne retrouve pas le nom. J'ai egalement fait appel à l'aide de mon père lorsque j'etait trop bloqué.


import turtle
import os
import math

#écran du jeu
wn = turtle.Screen()
wn.bgcolor("black")
wn.title("Space invader - Enora et Marine")
#wn.bgpic("Space_invaders_background.gif")

#enemi et joueur
#turtle.register_shape("invader.gif")
#turtle.register_shape("player.gif")

border_pen = turtle.Turtle()
border_pen.speed(0)
border_pen.color("white")
border_pen.penup()
border_pen.setposition(-300,-300)
border_pen.pendown()
border_pen.pensize(3)
for side in range(4):
    border_pen.fd(600)
    border_pen.lt(90)
border_pen.hideturtle()

#Creation du joueur
player = turtle.Turtle()
player.color("yellow")
player.shape("square")
player.penup()
player.speed()
player.setposition(0, -250)
player.setheading(90)
playerspeed = 20

ennemi = turtle.Turtle()
ennemi.color("red")
ennemi.shape("triangle")
ennemi.penup()
ennemi.speed()
ennemi.setposition(-200, 250)
ennemispeed = 3

#definition pour bouger le joueur
def move_left():
    x = player.xcor()
    x -= playerspeed
    if x < -280:
        x = - 280
    player.setx(x)

def move_right():
    x = player.xcor()
    x += playerspeed
    if x > 280:
        x = 280
    player.setx(x)

def shoot_bullet():
    global bulletstate
    if bulletstate == "ready":
        bulletstate = "shoot"
    x = player.xcor()
    y = player.ycor() + 10
    bullet.setposition(x, y)
    bullet.showturtle()

def iscollision(t1, t2):
    distance = math.sqrt(math.pow(t1.xcor()-t2.xcor(),2)+math.pow(t1.xcor()-t2.xcor(),2)+math.pow(t1.ycor()-t2.ycor(),2))
    if distance < 15:
        return True
    else:
        return False

# touche du clavier qui permettent de le bouger
turtle.listen()
turtle.onkey(move_left,"Left")
turtle.onkey(move_right,"Right")
turtle.onkey(shoot_bullet,"space")

#creation du cannon
bullet = turtle.Turtle()
bullet.color("red")
bullet.shape("circle")
bullet.penup()
bullet.speed()
bullet.setheading(90)
bullet.shapesize(0.5, 0.5)
bullet.hideturtle()
bulletspeed = 20
bulletstate = "ready"

#main loop
while True :

    #bouger l'ennemi
    x = ennemi.xcor()
    x += ennemispeed
    ennemi.setx(x)

    if ennemi.xcor() > 280:
        y = ennemi.ycor()
        y -=40
        ennemispeed *= -1
        ennemi.sety(y)

    if ennemi.xcor() < -280:
        y = ennemi.ycor()
        y -=40
        ennemispeed *= -1
        ennemi.sety(y)

    #bouger le cannon
    if bulletstate == "shoot":
        y = bullet.ycor()
        y += bulletspeed
        bullet.sety(y)

    if bullet.ycor() > 275:
        bullet.hideturtle()
        bulletstate= "ready"

    #regarder si il y a eu collision
    if iscollision(bullet, ennemi):
        #Reset le cannon
        bullet.hideturtle()
        bulletstate = "ready"
        bullet.setposition(0, -400)
        #Reset l'ennemi
        ennemi.setposition(-200, 250)

delay = input("Press enter to finish")
