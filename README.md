import sys
import Adafruit_DHT // เพื่อใช้งาน sensor DHT11
import paho.mqtt.publish as publish //เพื่อใช้งาน mqtt
import time
hostname = "127.0.1.1" // วิธีเซ็คคือ พิมพ์ hostname บน cmd ของตัว subscribe
port = 1883
auth = {
 'username':'ummqtt', // username ที่เราสร้าง
 'password':'123456789' // password ที่ตั้งไว้
}
sensor = 11
pin = 4 
while True:
    humidity, temperature = Adafruit_DHT.read_retry(sensor, pin)
    if humidity is not None and temperature is not None:
    print("Sending...")
    publish.single('testmqtt','Temperature = {0:0.1f}*  Humidity = {1:0.1f}%'.format(temperature, humidity), hostname=hostname, port=port, auth=auth)
    time.sleep(2)
