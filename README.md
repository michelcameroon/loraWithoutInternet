# loraWithoutInternet
we want a loraa system, which work without internet.
see 
https://github.com/antirez/freakwan


Install

follow the installation in https://github.com/antirez/freakwan

Installation

    Install MicroPython on your device. NOTE: MicroPython versions > 1.19.1 have buggy bluetooth stack with certain devices, so before they fix it, it's better to stick to version 1.19.1. However your device may not have a working 1.19.1 version (it's the case with certain ESP32 S3 devices like the Lilygo t-watch S3): in this case you need to disable BLE manually, editing wan_config.py and setting ble_enabled to False.

    Clone this repository, and edit wan_config.py to set your nickname and status message, set the frequency according to your device. Warning: make sure to set the right frequency based on the LoRa module you own, and make sure your antenna is already installed before using the software, or you may damage your hardware.

    Copy one of the files inside the devices folder in the main folder as device_config.py, for instance if I have a T3 v2 1.6 device, I will do:

    cp devices/device_config.t3_v2_1.6.py ./device_config.py

    Transfer all the .py files in the root directory of this project in your device. To transfer the files, you can use mpremote (pip3 install mpremote should be enough), or an alternative tool that we wrote, and is conceptually part of the FreakWAN effort, called talk32. Talk32 is not as fast as mpremote at transferring files, but sometimes mpremote does not work with certain devices and talk32 does (and the other way around).

    mpremote cp *.py :

or

talk32 /dev/tty.usbserial001 put *.py

Please note that you don't need both the command lines. Just one depending on the tool you use.

    Restart your device: you can either power it off/on, or use mpremote repl and hit Ctrl_D to trigger a soft reset. Sometimes devices also have a reset button. If everything is fine you will see the splash screen and then the program version.
    If you are using a T-WATCH S3, or other recent Lyligo devices based on ESP32-S3, and your splash screen freezes (the waves should move and then the splash screen should disappear, if everything works well), please try to disable BLE from wan_config.py.






history

 1934  esptool.py -p /dev/ttyACM0 flash_id
 
 1935  esptool.py --chip esp32 --port /dev/ttyACM0 erase_flash

 1944  esptool.py --chip esp32 --port /dev/ttyACM0 --baud 460800 write_flash -z 0x1000 LILYGO_TTGO_LORA32-20240105-v1.22.1.bin
 1945  talk32 /dev/ttyACM0 repl
 testen if machine can be imported
 
 1947  pyserial-miniterm /dev/ttyACM0 115200

 1950  cd freakwan/
 
 1951  talk32 /dev/ttyACM0 put *.py
 
 1952  pyserial-miniterm /dev/ttyACM0 115200

cp devices/device_config.t3_v2_1.6.py ./device_config.py


adapt wan_config.py 
put nickname michel and chris

and it works


Usage

1982  pyserial-miniterm /dev/ttyACM0 115200
better than screen, because we can go out in screen i dont know how to go out

when the computer is switch on, it starts with the main.py


in our application, it makes a lot of commands, HELO to control if all clients in the netword are still there, ...


test an python script

you can do it with the command

talk32 run <python.script.py>

Sensor
we can read the result of sensor

test with DHT11 sensor (temprature and himidity)

first we must adapt the sensor file (it is done for DHT22 and we have DHT11) 

after we must adapt 

wan_config.py 
and put the following lines at the end of wan_config.py

     config['sensor'] = {
        'enabled': True,
        'type': 'DHT11',
        'dht_pin': 25,
        'period': 30000, # In milliseconds
        'key_name': "sensor_key", # Encryption key for sensor data
        'key_secret': "123456",
    }



so the temperature and humidity will appear om the oled display of the both computer

todo 
test other sensors

ble 
with a phone which has blueroothm 





 
