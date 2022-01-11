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
