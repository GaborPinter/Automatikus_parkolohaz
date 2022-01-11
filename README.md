from sense_hat import SenseHat
from time import *



sense = SenseHat()

red = [255,0,0]
blue = [0,0,255]
green = [0,255,0]
black = [0,0,0]
feher = [255,255,255]
sarga = [255,255,0]

s = 59

a=63
b=59
c=52
d=50
e=59
f=55

bejelentkezes =["abc-123", "efc-456"]
t = []
mehet = None
pozi = 1
proba3 = None
proba2 = None
hely1 = False
hely2 = False
hely3 = False
hely4 = False
hely5 = False
autoszam = 5

    
##feltöltjük a tömböt
for i in range(64):
    t.append(black)
    
#64-60-ig út
for i in range(63,58,-1):
    sleep(0.5)
    if i != 59:
        t[i] = red
    if i <63 or i == 60:
        t[i+1] = black 
       
    sense.set_pixels(t)
    sense.set_pixel(0,5,red),sense.set_pixel(1,5,red),sense.set_pixel(2,5,red),sense.set_pixel(3,5,red),
    sense.set_pixel(4,5,red),sense.set_pixel(5,5,red),sense.set_pixel(6,5,red),sense.set_pixel(7,5,red), 
    sense.set_pixel(0,1,feher),sense.set_pixel(1,1,feher),sense.set_pixel(6,1,feher),sense.set_pixel(7,1,feher),
    sense.set_pixel(6,3,feher),sense.set_pixel(7,3,feher),sense.set_pixel(0,2,blue),sense.set_pixel(1,2,blue)
    sense.set_pixel(0,3,blue),sense.set_pixel(1,3,blue)
    
sense.set_pixel(4,6,red)
sleep(0.5)

beir = input("Az autó rendszáma: ")
if beir in bejelentkezes:
    mehet = True
else: mehet = False


if bool(mehet == False):
    sense.show_message("Sikertelen",scroll_speed = 0.08, text_colour = red)
    
    #53-51-ig út
    for i in range(52,49,-1):
        sleep(0.5)
        if i!= 50:
            t[i] = red
        if i==51 or i == 49:
            t[i+1] = black
      
        sense.set_pixels(t)
        sense.set_pixel(0,5,red),sense.set_pixel(1,5,red),sense.set_pixel(2,5,red),sense.set_pixel(3,5,red),
        sense.set_pixel(4,5,red),sense.set_pixel(5,5,red),sense.set_pixel(6,5,red),sense.set_pixel(7,5,red), 
        sense.set_pixel(0,1,feher),sense.set_pixel(1,1,feher),sense.set_pixel(6,1,feher),sense.set_pixel(7,1,feher),
        sense.set_pixel(6,3,feher),sense.set_pixel(7,3,feher),sense.set_pixel(0,2,blue),sense.set_pixel(1,2,blue)
        sense.set_pixel(0,3,blue),sense.set_pixel(1,3,blue)
    
        
    
    #60-56-ig út
    for i in range(59,54,-1):
        sleep(0.5)
        if i != 55:
            t[i] = red
        
        if i < 59 or i == 54:
            t[i+1] = black
            
        sense.set_pixels(t)
        sense.set_pixel(3,6,black)
        sense.set_pixel(0,5,red),sense.set_pixel(1,5,red),sense.set_pixel(2,5,red),sense.set_pixel(3,5,red),
        sense.set_pixel(4,5,red),sense.set_pixel(5,5,red),sense.set_pixel(6,5,red),sense.set_pixel(7,5,red), 
        sense.set_pixel(0,1,feher),sense.set_pixel(1,1,feher),sense.set_pixel(6,1,feher),sense.set_pixel(7,1,feher),
        sense.set_pixel(6,3,feher),sense.set_pixel(7,3,feher),sense.set_pixel(0,2,blue),sense.set_pixel(1,2,blue)
        sense.set_pixel(0,3,blue),sense.set_pixel(1,3,blue)
    
     
elif bool(mehet == True):
    sense.show_message("Sikeres",scroll_speed = 0.08, text_colour = green)
    #sense.set_pixel(0,5,red),sense.set_pixel(1,5,red),sense.set_pixel(2,5,red),sense.set_pixel(3,5,red),
    #sense.set_pixel(4,5,red),sense.set_pixel(5,5,red),sense.set_pixel(6,5,red),sense.set_pixel(7,5,red), 
    #sense.set_pixel(0,5,red),sense.set_pixel(1,5,red),sense.set_pixel(2,5,red),sense.set_pixel(3,5,red),
    #sense.set_pixel(4,5,red),sense.set_pixel(5,5,red),sense.set_pixel(6,5,red),sense.set_pixel(7,5,red), 
    sense.set_pixel(0,1,feher),sense.set_pixel(1,1,feher),sense.set_pixel(6,1,feher),sense.set_pixel(7,1,feher),
    sense.set_pixel(6,3,feher),sense.set_pixel(7,3,feher),sense.set_pixel(0,2,blue),sense.set_pixel(1,2,blue)
    sense.set_pixel(0,3,blue),sense.set_pixel(1,3,blue)
    sense.set_pixel(4,6,red)
    
    sense.set_pixel(0,0,sarga)
    #while True
    while hely1 == False and hely2 == False:
        for event in sense.stick.get_events():
            if event.action == "pressed":
                if event.direction == "left":
                    pozi = pozi-1
                    if pozi < 1:
                        pozi = 5
                    if pozi == 1:
                        sense.set_pixel(7,0,black)
                        sense.set_pixel(0,0,sarga)
                    if pozi == 2:
                        sense.set_pixel(7,2,black)
                        sense.set_pixel(7,0,sarga)
                    if pozi == 3:
                        sense.set_pixel(0,4,black)
                        sense.set_pixel(7,2,sarga)
                        #hely3 = True
                    if pozi == 4:
                        sense.set_pixel(7,4,black)
                        sense.set_pixel(0,4,sarga)
                    if pozi == 5:
                        sense.set_pixel(0,0,black)
                        sense.set_pixel(7,4,sarga)
                        
                    
                elif event.direction == "right":
                    pozi = pozi+1
                    if pozi > 5:
                        pozi = 1
                    if pozi == 1:
                        sense.set_pixel(0,0,sarga)
                        sense.set_pixel(7,4,black)
                    if pozi == 2:
                        sense.set_pixel(0,0,black)
                        sense.set_pixel(7,0,sarga)
                        #hely2 = True
                    if pozi == 3:
                        sense.set_pixel(7,0,black)
                        sense.set_pixel(7,2,sarga)
                    if pozi == 4:
                        sense.set_pixel(7,2,black)
                        sense.set_pixel(0,4,sarga)
                    if pozi == 5:
                        sense.set_pixel(0,4,black)
                        sense.set_pixel(7,4,sarga)
                elif event.direction == "up":
                    if pozi == 2:
                        hely2 = True
                        break
                    if pozi == 3:
                        hely3 = True
                        break

    
    if hely2 == True:
        for i in range(45,11,-1):
            sleep(0.1)
            if i == 44 or i == 36 or i== 28 or i == 20 or i == 12:
                t[i] = red
            if i == 36:
                t[44] = black
            if i == 28:
                t[36] = black
            if i == 20:
                t[28] = black
            if i == 12:
                t[20] = black
            
            sense.set_pixels(t) 
            sense.set_pixel(0,1,feher),sense.set_pixel(1,1,feher),sense.set_pixel(6,1,feher),sense.set_pixel(7,1,feher),
            sense.set_pixel(6,3,feher),sense.set_pixel(7,3,feher),sense.set_pixel(0,2,blue),sense.set_pixel(1,2,blue)
            sense.set_pixel(0,3,blue),sense.set_pixel(1,3,blue)
               
               
        for i in range(4,9,1):
            sleep(0.8)
            if i != 9:
                t[i] = red
            if i > 4 and  i != 8:
                t[i-1] = black
            sense.set_pixels(t)
            sense.set_pixel(4,1,black)
            sense.set_pixel(0,1,feher),sense.set_pixel(1,1,feher),sense.set_pixel(6,1,feher),sense.set_pixel(7,1,feher),
            sense.set_pixel(6,3,feher),sense.set_pixel(7,3,feher),sense.set_pixel(0,2,blue),sense.set_pixel(1,2,blue)
            sense.set_pixel(0,3,blue),sense.set_pixel(1,3,blue)
            
           
    if hely3 == True:
        for i in range(45,20,-1):
            sleep(0.1)
            if i == 44 or i == 36 or i== 28 or i == 20:
                t[i] = red
            if i == 36:
                t[44] = black
            if i == 28:
                t[36] = black
            if i == 20:
                t[28] = black
            
            sense.set_pixels(t) 
            sense.set_pixel(0,1,feher),sense.set_pixel(1,1,feher),sense.set_pixel(6,1,feher),sense.set_pixel(7,1,feher),
            sense.set_pixel(6,3,feher),sense.set_pixel(7,3,feher),sense.set_pixel(0,2,blue),sense.set_pixel(1,2,blue)
            sense.set_pixel(0,3,blue),sense.set_pixel(1,3,blue)
               
               
        for i in range(20,25,1):
            sleep(0.8)
            if i != 25:
                t[i] = red
            if i > 20 and  i != 24:
                t[i-1] = black
            sense.set_pixels(t)
            sense.set_pixel(4,1,black)
            sense.set_pixel(0,1,feher),sense.set_pixel(1,1,feher),sense.set_pixel(6,1,feher),sense.set_pixel(7,1,feher),
            sense.set_pixel(6,3,feher),sense.set_pixel(7,3,feher),sense.set_pixel(0,2,blue),sense.set_pixel(1,2,blue)
            sense.set_pixel(0,3,blue),sense.set_pixel(1,3,blue)     
            
            
           
sleep(3)
sense.clear()
