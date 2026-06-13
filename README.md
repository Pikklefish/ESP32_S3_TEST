# ESP32_S3_TEST

## WIFI on ESP32 (Station vs AP)
### Station Mode
![station wifi mode](/esp_wifi_station.png)

***Station*** means ESP32 board is connected to an Access Point (e.g. home router)
In this example we use IPv4 (old version)

***IPv4***
IPv4 format: xxx.xxx.xxx.xxx (numbers range from 1-255)
Subnet: sets the guideline for what is considered locl network.
For example: If local network is 192.193.343.xxx and subnet is 255.255.255.0 it means the first 3 numbers should be same and the last number can be unique to be considered local network (if it is different it will direct it to the internet) 
Gateway: the gateway to the internet (router gateway ie 192.193.343.1), all Ipv4 address not 192.193.343.xxx is routed to this gateway to be connected to the internet.


~~~
#include <WiFi.h>

const char *ssid_STA    = "*****"; //Enter the home wifi router name
const char *password_STA = "******"; //Enter the home wifi router password

IPAddress local_IP(10,0,0,123);//Set the IP address of ESP32 itself (must be within my router range 1-254, IPv4)
IPAddress gateway(10,0,0,1);   //Set the gateway 
IPAddress subnet(255,255,255,0);  //Set the subnet mask (255 means locked, 0 means unique)


void setup() {
  Serial.begin(115200);
  delay(2000);

  Serial.println("Connecting to WiFi router...");

  WiFi.disconnect();
  WiFi.mode(WIFI_STA);

  if (!WiFi.config(local_IP, gateway, subnet)) {
    Serial.println("Static IP configuration failed");
  }

  WiFi.begin(ssid_STA, password_STA);

  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }

  Serial.println();
  Serial.println("Connected to router!");
  Serial.print("ESP32 IP address = ");
  Serial.println(WiFi.localIP());

  Serial.print("MAC address = ");
  Serial.println(WiFi.macAddress());

  Serial.println("Setup End");
}

void loop() {
}
~~~
