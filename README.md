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
