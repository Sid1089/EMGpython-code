# EMGpython-code
# my mini project based on electromyoelectic sensor's python code 
import urllib.request
import requests
import threading
import json
import time
import random
import serial

ser = serial.Serial(
                 'COM7',
                   baudrate = 9600,
                    parity=serial.PARITY_NONE,
                   stopbits=serial.STOPBITS_ONE,
                   bytesize=serial.EIGHTBITS,
 #                   )
                    timeout=1 # must use when using data.readline()
                    )
Bicep=0
Squat=0
Dumble=0
def thingspeak_post():
    global Bicep
    global Squat
    global Dumble
##    threading.Timer(15,thingspeak_post).start()
    data = ser.readline().decode("utf-8").strip()
   # data = ser.readline()
    print("Rece char", data)
    if "E" in data:
        Bicep=data[2]
##    if "S" in data:
##        Squat=data[2]
##    if "D" in data:
##        Dumble=data[2]
    
   # print("Received data {}: {}".format(Bicep,Squat))
 
   
##    val1=random.randint(60,560)
##    val2=random.randint(46,50)
##    val3=random.randint(50,55)
##    val4=random.randint(37,50)
##    val5=random.randint(20,180)
##    val6=random.randint(40,45)
##    val7=random.randint(46,50)
##    URl='https://api.thingspeak.com/update?api_key=4YSF6M6ZCRGYIE02&field1=10&field2=20&field3=30&field4=40&field5=50&field6=60&field7=70'
##    KEY='AV67VKI5EDYROW58'
##    HEADER='&field1={}&field2={}&field3={}&field4={}&field5={}&field6={}&field7={}'.format(val1,val2,val3,val4,val5,val6,val7)
##    NEW_URL = URl+KEY+HEADER
##    print(NEW_URL)
##    data=urllib.request.urlopen(NEW_URL)
##    print(data)

    URl='https://api.thingspeak.com/update?api_key=4NC9SZ71TJN1L5Q2&field1=10&field2=20&field3=30'
    KEY='4NC9SZ71TJN1L5Q2'
    #HEADER='&field1={}&field2={}&field3={}'.format(Bicep,Squat,Dumble)
    HEADER='&field1={}'.format(Bicep)
    NEW_URL = URl+KEY+HEADER
    print(NEW_URL)
    data=urllib.request.urlopen(NEW_URL)
        
if __name__ == '__main__':
    while True:
        thingspeak_post()
        time.sleep(1)

