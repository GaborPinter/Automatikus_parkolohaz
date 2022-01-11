from sense_hat import SenseHat
from time import *
import mysql.connector as mariadb
import random, smtplib

mariadb_connection = mariadb.connect(user ='mark', password = '123456', host = 'Localhost', port = '3306')

create_cursor = mariadb_connection.cursor()

create_cursor.execute("USE adatbazis")

sense = SenseHat()


red = [255,0,0]
blue = [0,0,255]
green = [0,255,0]
black = [0,0,0]
feher = [255,255,255]
sarga = [255,255,0]


t = []
ar = []
mehet = None
pozi = 1
autoszam = 10
regvbel = 1
iddb = 1
ujvmeglev = 1
hely1 = False
hely2 = False
hely3 = False
hely4 = False
hely5 = False

hely11 = False
hely12 = False
hely13 = False
hely14 = False
hely15 = False



for i in range(10000):
    ar.append(i)
    
for i in range(64):
    t.append(black)
    if i == 8 or i == 9 or i == 14 or i == 15 or i == 30 or i == 31:
        t[i] = feher
    if i == 16 or i== 17 or i == 24 or i == 25:
        t[i] = blue

  
def kiirSorompo():
    sense.set_pixel(0,5,red),sense.set_pixel(1,5,red),sense.set_pixel(2,5,red),sense.set_pixel(3,5,red)
    sense.set_pixel(4,5,red),sense.set_pixel(5,5,red),sense.set_pixel(6,5,red),sense.set_pixel(7,5,red)
    

while autoszam > 0:
    
    sense.set_pixels(t),kiirSorompo()
    ujvmeglev = int(input("Üdvözöllek a parkolóházban.\nVálassz az alábbi menüből:\n   1.Új autó\n   2.Parkoló autó\n   3.Kilépés\n"))
    while ujvmeglev < 1 or ujvmeglev > 3:
        ujvmeglev = int(input("Helytelen szám, próbáld újra: "))
        
    if sense.get_pixel(0,0) == [248,0,0] and sense.get_pixel(7,0) == [248,0,0] and sense.get_pixel(7,2) == [248,0,0] and sense.get_pixel(0,4) == [248,0,0] and sense.get_pixel(7,4) == [248,0,0]:
            print("\nNincsen szabad hely, válassz egy parkoló autót.\n")
            ujvmeglev = 2;
            
    if ujvmeglev == 1:
        print("Egy autó érkezik...")
        for i in range(63,58,-1):
            sleep(0.5)
            if i != 59:
                t[i] = red
            if i <63 or i == 60:
                t[i+1] = black 
           
            sense.set_pixels(t),kiirSorompo()
            
        
        sense.set_pixel(4,6,red)
        sleep(0.5)
        
        regvbel = int(input("Válassz az alábbi menüből:\n   1.Belépés\n   2.Regisztráció\n   3.Adatbázis megtekintése\n"))
        while int(regvbel) < 1 or int(regvbel) > 3:
            regvbel = int(input("Helytelen szám, próbáld újra: "))
           
        if regvbel == 3:
            print("\nAz adatbázis:")
            create_cursor.execute("SELECT * FROM autok")
            for x in create_cursor:
                print(x)
                print("\n")
            regvbel = int(input("Válassz az alábbi menüből:\n   1.Belépés\n   2.Regisztráció\n   3.Adatbázis megtekintése\n"))
            
        if regvbel == 2:
            create_cursor.execute('SELECT id FROM autok Order by id desc LIMIT 1')
            eredmeny = create_cursor.fetchall()
            eredmeny2 = [i[0] for i in eredmeny]
            for i in eredmeny2:
                iddb = i + 1
            nev = input("Név: ")
            rendszam = input("Rendszám: ")
            bankkartya = input("Bankkártya: ")
            sql_statement = 'INSERT INTO autok (id,nev,rendszam,bankkartyaszam) VALUES ('+str(iddb)+',"'+nev+'","'+rendszam+'","'+bankkartya+'")';
            create_cursor.execute(sql_statement)
            mariadb_connection.commit();
            print("Sikeres regisztráció, most már be tudsz lépni\n")
            
        sql = 'SELECT rendszam FROM autok'
        create_cursor.execute(sql)
        eredmeny = create_cursor.fetchall()
        bejelentkezes = [i[0] for i in eredmeny]
        
        beir = input("Az autó rendszáma: ")
        if beir in bejelentkezes:
            mehet = True
        else: mehet = False


        if bool(mehet == False):
            sense.show_message("Sikertelen",scroll_speed = 0.08, text_colour = red)
            
            for i in range(52,49,-1):
                sleep(0.5)
                
                if i!= 50:
                    t[i] = red
                    
                if i==51 or i == 50:
                    t[i+1] = black
                              
                sense.set_pixels(t),kiirSorompo()
                
                
            for i in range(59,54,-1):
                sleep(0.5)
                
                if i != 55 and i > 55:
                    t[i] = red
                
                if i < 59 or i == 54:
                    t[i+1] = black
                         
                sense.set_pixels(t),kiirSorompo()
                
            
        elif bool(mehet == True):
            sense.show_message("Sikeres",scroll_speed = 0.08, text_colour = green)
            sense.set_pixels(t)
            sense.set_pixel(4,6,red)
            
            
            
            if sense.get_pixel(0,0) == [0,0,0]: 
                sense.set_pixel(0,0,sarga)
                pozi = 1
            elif sense.get_pixel(7,0) == [0,0,0]:
                sense.set_pixel(7,0,sarga)
                pozi = 2
            elif sense.get_pixel(7,2) == [0,0,0]:
                sense.set_pixel(7,2,sarga)
                pozi = 3
            elif sense.get_pixel(0,4) == [0,0,0]:
                sense.set_pixel(0,4,sarga)
                pozi = 4
            elif sense.get_pixel(7,4) == [0,0,0]:
                sense.set_pixel(7,4,sarga)
                pozi = 5
            
            valami = "valami"
            while valami == "valami":
                if hely11 == True:          
                    sense.set_pixel(0,0,red)
                if hely12 == True:
                    sense.set_pixel(7,0,red)
                if hely13 == True:
                    sense.set_pixel(7,2,red)
                if hely14 == True:
                    sense.set_pixel(0,4,red)
                if hely15 == True:
                    sense.set_pixel(7,4,red)
                    
                for event in sense.stick.get_events():
                    if event.action == "released":
                        if event.direction == "left":
                            pozi = pozi-1  
                            if pozi < 1:
                                pozi = 1

                            if pozi == 5 and hely15 == False:
                                sense.set_pixel(0,0,black)
                                sense.set_pixel(7,4,sarga)
                            elif pozi == 5 and hely15 == True:
                                pozi = 4
                                sense.set_pixel(0,0,black)
                                sense.set_pixel(7,4,red)
                                
                            if pozi == 4 and hely14 == False:
                                sense.set_pixel(7,4,black)
                                sense.set_pixel(0,4,sarga)
                            elif pozi == 4 and hely14 == True:
                                pozi = 3
                                sense.set_pixel(7,4,black)
                                sense.set_pixel(0,4,red)
                            
                            if pozi == 3 and hely13 == False:
                                sense.set_pixel(0,4,black)
                                sense.set_pixel(7,2,sarga)
                            elif pozi == 3 and hely12 == True:
                                pozi = 2
                                sense.set_pixel(0,4,black)
                                sense.set_pixel(7,2,red)
                                
                            if pozi == 2 and hely12 == False:
                                sense.set_pixel(7,2,black)
                                sense.set_pixel(7,0,sarga)  
                            elif pozi == 2 and hely12 == True:
                                pozi = 1
                                sense.set_pixel(7,2,black)
                                sense.set_pixel(7,0,red)    
                            
                            if pozi == 1 and hely11 == False:
                                sense.set_pixel(7,0,black)
                                sense.set_pixel(0,0,sarga)
                            elif pozi == 1 and hely11 == True:
                                pozi = 6
                                sense.set_pixel(7,0,black)
                                sense.set_pixel(0,0,red)
                            
                            
                            
                        elif event.direction == "right":
                            pozi = pozi+1
                            if pozi > 5:
                               pozi = 5
                            
                            if pozi == 1 and hely11 == False:
                                sense.set_pixel(0,0,sarga)
                                sense.set_pixel(7,4,black)
                                
                            elif pozi == 1 and hely11 == True:
                                pozi = 2
                                sense.set_pixel(0,0,red)
                                sense.set_pixel(7,4,black)
                            if pozi == 2 and hely12 == False:
                                sense.set_pixel(0,0,black)
                                sense.set_pixel(7,0,sarga)
                            elif pozi == 2 and hely12 == True:
                                pozi = 3
                                sense.set_pixel(0,0,black)
                                sense.set_pixel(7,0,red)
                                    
                            if pozi == 3 and hely13 == False:
                                sense.set_pixel(7,0,black)
                                sense.set_pixel(7,2,sarga)
                            elif pozi == 3 and hely13 == True:
                                pozi = 4
                                sense.set_pixel(7,0,black)
                                sense.set_pixel(7,2,red)
                                
                            if pozi == 4 and hely14 == False:
                                sense.set_pixel(7,2,black)
                                sense.set_pixel(0,4,sarga)
                            elif pozi == 4 and hely14 == True:
                                pozi = 5
                                sense.set_pixel(7,2,black)
                                sense.set_pixel(0,4,red)
                                
                            if pozi == 5 and hely15 == False:
                                sense.set_pixel(0,4,black)
                                sense.set_pixel(7,4,sarga)
                            elif pozi == 5 and hely15 == True:
                                sense.set_pixel(0,4,black)
                                sense.set_pixel(7,4,red)
                            
                    
                        elif event.direction == "up":
                            valami = ""
                            if pozi == 1:
                                hely1 = True
                                hely11 = True
                            if pozi == 2:
                                hely2 = True
                                hely12 = True
                            if pozi == 3:
                                hely3 = True
                                hely13 = True
                            if pozi == 4:
                                hely4 = True
                                hely14 = True
                            if pozi == 5:
                                hely5 = True
                                hely15 = True
                                               
                    
                if hely1 == True:
                    hely1 = False
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
                                       
                    for i in range (5,-1,-1):
                        sleep(0.7)
                        
                        if i!= 5:
                            t[i] = red
                        if i < 6 or i == -1:
                            t[i+1] = black
                            
                           
                        sense.set_pixels(t)
                        t[12] = black 
                                            
                if hely2 == True:
                    hely2 = False
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
                           
                    for i in range(4,9,1):
                        
                        sleep(0.7)
                        if i != 8:
                            t[i] = red
                        if i > 4 and  i != 8:
                            t[i-1] = black   
                        t[12] = black                    
                        sense.set_pixels(t)
                    
                    
                if hely3 == True:
                    hely3 = False
                    for i in range(45,19,-1):
                        sleep(0.1)
                        if i == 44 or i == 36 or i== 28 or i == 20:
                            t[i] = red
                           
                        if i == 36:
                            t[44] = black
                        if i == 28:
                            t[36] = black
                        if i == 20:
                            t[28] = black
                        if i == 19:
                            t[20] = black
                        
                        
                        sense.set_pixels(t)
                        
                    for i in range(20,25,1):
                        sleep(0.7)
                        if i != 24:
                            t[i] = red                       
                        if i > 20 and  i != 24:
                            t[i-1] = black
 
                        sense.set_pixels(t)

                        
                if hely4 == True:
                    hely4 = False
                    for i in range(44,35,-1):
                        sleep(0.1)
                        if i == 44 or i == 36:
                            t[i] = red
                        if i == 36:
                            t[44] = black
                        
                        sense.set_pixels(t)
                    
                    for i in range(35,30,-1):
                        sleep(0.7)
                        if i != 31:
                            t[i] = red
                        
                        if i < 35 and i != 31:
                            t[i+1] = black
                        
                            
                        t[36] = black
                        sense.set_pixels(t)
                        
                if hely5 == True:
                    hely5 = False
                    for i in range(44,35,-1):
                        sleep(0.1)
                        if i == 44 or i == 36:
                            t[i] = red
                        if i == 36:
                            t[44] = black
                        
                        sense.set_pixels(t)
                    
                    for i in range(36,41,1):
                        sleep(0.7)
                        
                        if i != 40:
                            t[i] = red
                        
                        if i > 36 and i != 40:
                            t[i-1] = black
   
                        sense.set_pixels(t)
                        t[36] = black
                      
    if ujvmeglev == 2:
        
        if sense.get_pixel(0,0) == [248,0,0]:
            hely1 = True
            t[0] = red
        else:
            hely1 = False
            t[0] = black
        
        if sense.get_pixel(7,0) == [248,0,0]:
            hely2 = True
            t[7] = red
        else:
            hely2 = False
            t[7] = black
        
        if sense.get_pixel(7,2) == [248,0,0]:
            hely3 = True
            t[23] = red
        else:
            hely3 = False
            t[23] = black
        
        if sense.get_pixel(0,4) == [248,0,0]:
            hely4 = True
            t[32] = red
        else:
            hely4 = False
            t[32] = black
        
        if sense.get_pixel(7,4) == [248,0,0]:
            hely5 = True
            t[39] = red
        else:
            hely5 = False
            t[39] = black
        
        
        
        if hely1 == False and hely2 == False and hely3 == False and hely4 == False and hely5 == False:
            print("\nNincsen parkolt autó, visszatérés a menübe.\n")
            
        else:
            pozi = 1
            print("Válassz egy autót\n")
            valami = "valami"
            sense.set_pixels(t)
           
            if sense.get_pixel(0,0) == [248,0,0]: 
                sense.set_pixel(0,0,green)
                pozi = 1
            elif sense.get_pixel(7,0) == [248,0,0]:
                sense.set_pixel(7,0,green)
                pozi = 2
            elif sense.get_pixel(7,2) == [248,0,0]:
                sense.set_pixel(7,2,green)
                pozi = 3
            elif sense.get_pixel(0,4) == [248,0,0]:
                sense.set_pixel(0,4,green)
                pozi = 4
            elif sense.get_pixel(7,4) == [248,0,0]:
                sense.set_pixel(7,4,green)
                pozi = 5
            
            
            
            while valami == "valami":
                for event in sense.stick.get_events():
                    if event.action == "released":
                        if event.direction == "left":
                            sense.set_pixels(t)
                            pozi = pozi-1
                            if pozi < 1:
                               pozi = 1
                            if pozi == 5 and hely5 == True:
                                sense.set_pixel(7,4,green)
                            elif pozi == 5 and hely5 == False:
                                pozi = 4
                            if pozi == 4 and hely4 == True:
                                sense.set_pixel(0,4,green)
                            elif pozi == 4 and hely4 == False:
                                pozi = 3
                            if pozi == 3 and hely3 == True:
                                sense.set_pixel(7,2,green)
                            elif pozi == 3 and hely3 == False:
                                pozi = 2
                            if pozi == 2 and hely2 == True:
                                sense.set_pixel(7,0,green)
                            elif pozi == 2 and hely2 == False:
                                pozi = 1
                            if pozi == 1 and hely1 == True:
                                sense.set_pixel(0,0,green)
                            elif pozi == 1 and hely1 == False:
                                pozi = 1
                            
                                
                        elif event.direction == "right":
                            sense.set_pixels(t)
                            pozi = pozi + 1
                            
                            if pozi > 5:
                               pozi = 5
                            
                            if pozi == 1 and hely1 == True:
                                sense.set_pixel(0,0,green)
                            elif pozi == 1 and hely1 == False:
                                pozi = 2
                            if pozi == 2 and hely2 == True:
                                sense.set_pixel(7,0,green)
                                
                            elif pozi == 2 and hely2 == False:
                                pozi = 3
                            if pozi == 3 and hely3 == True:
                                sense.set_pixel(7,2,green)
                            elif pozi == 3 and hely3 == False:
                                pozi = 4
                            if pozi == 4 and hely4 == True:
                                sense.set_pixel(0,4,green)
                            elif pozi == 4 and hely4 == False:
                                pozi = 5
                            if pozi == 5 and hely5 == True:
                                sense.set_pixel(7,4,green)
                            elif pozi == 5 and hely5 == False:
                                pozi = 5
                                

                                
                        elif event.direction == "up":
                            valami = ""
                            if pozi == 1:
                                hely1 = False
                            if pozi == 2:
                                hely2 = False
                            if pozi == 3:
                                hely3 = False
                            if pozi == 4:
                                hely4 = False
                            if pozi == 5:
                                hely5 = False
                                
            print("A kiválaszott autó távozik.\n")                    
            if hely1 == False and pozi == 1:                   
                for i in range (0,5,1):
                    sleep(0.7)
                    if i!= 4:
                        t[i] = red
                    if i > 0 and i != 4:
                        t[i-1] = black
                            
                           
                    sense.set_pixels(t),kiirSorompo()
                    
                        
                for i in range(11,45,1):
                    sleep(0.1)
                    if i == 35 or i== 27 or i == 19 or i == 11:
                        t[i] = red
                    if i == 11:
                        t[3] = black
                    if i == 19:
                        t[11] = black
                    if i == 27:
                        t[19] = black
                    if i == 35:
                        t[27] = black
                    
                        
                    sense.set_pixels(t),kiirSorompo()
                  
                                            
            if hely2 == False and pozi == 2:
                for i in range(7,2,-1):
                    sleep(0.7)
                    if i != 2:
                        t[i] = red
                    if i < 7 and  i != 2:
                        t[i+1] = black                      
                    sense.set_pixels(t),kiirSorompo()
                
                
                for i in range(11,45,1):
                    sleep(0.1)
                    if i == 35 or i== 27 or i == 19 or i == 11:
                        t[i] = red
                    if i == 11:
                        t[3] = black
                    if i == 19:
                        t[11] = black
                    if i == 27:
                        t[19] = black
                    if i == 35:
                        t[27] = black
                    
                        
                    sense.set_pixels(t),kiirSorompo()                         
                           
  
            if hely3 == False and pozi == 3:                         
                for i in range(23,18,-1):
                    sleep(0.7)
                    if i != 18:
                        t[i] = red                       
                    if i < 23 and  i != 18:
                        t[i+1] = black
 
                    sense.set_pixels(t),kiirSorompo()

                for i in range(11,45,1):
                    sleep(0.1)
                    if i == 35 or i== 27 or i == 19:
                        t[i] = red
                    if i == 19:
                        t[11] = black
                    if i == 27:
                        t[19] = black
                    if i == 35:
                        t[27] = black
                        
                            
                    sense.set_pixels(t),kiirSorompo() 
                    
            if hely4 == False and pozi == 4:
                for i in range(32,36,1):
                    sleep(0.7)
                    if i != 36:
                        t[i] = red
                        
                    if i > 32 and i != 36:
                        t[i-1] = black
                        
                            
                    sense.set_pixels(t),kiirSorompo()
                              
                       
            if hely5 == False and pozi == 5:
                for i in range(39,34,-1):
                    sleep(0.7)
                    if i != 34:
                        t[i] = red
                        
                        if i < 39 and i != 34:
                            t[i+1] = black
   
                    sense.set_pixels(t),kiirSorompo()                     
                
          
            emailcim = input("Az email cím formátuma: abcd@gmail.com\nA parkoló elhagyásához adja meg az email címét: ")
            szamocska = random.choice(ar)
            server = smtplib.SMTP('smtp.gmail.com',587)
            server.starttls()
            server.login("parkolohaz2022@gmail.com", "123456Qw")
            msg = "A bankszámlájáról " +str(szamocska)+"Ft került levonásra. Köszönjük, hogy nálunk parkolt."
            server.sendmail("parkolohaz2022@gmail.com", emailcim,msg.encode("utf-8"))
            server.quit()
            print("Email cím sikeresen elküldve, viszont látásra.")
            
            
            t[35] = black
            for i in range(59,54,-1):
                sleep(0.5)
                    
                if i != 55 and i > 55:
                    t[i] = red
                    
                if i < 59 or i == 54:
                    t[i+1] = black
                             
                sense.set_pixels(t),kiirSorompo()
                
        
        hely1 = False
        hely2 = False
        hely3 = False
        hely4 = False
        hely5 = False
        hely11 = False
        hely12 = False
        hely13 = False
        hely14 = False
        hely15 = False
        if sense.get_pixel(0,0) == [248,0,0]:
            hely11 = True
        if sense.get_pixel(7,0) == [248,0,0]:
            hely12 = True
        if sense.get_pixel(7,2) == [248,0,0]:
            hely13 = True
        if sense.get_pixel(0,4) == [248,0,0]:
            hely14 = True
        if sense.get_pixel(7,4) == [248,0,0]:
            hely15 = True
        
    autoszam = autoszam - 1
     
    if ujvmeglev == 3:
        print("Kilépés...")
        sleep(3)
        sense.clear()
        quit()
    
sleep(3)
sense.clear()
quit()
