# ESP32_S3_TEST

## WIFI on ESP32 (Station vs AP)
### Station Mode
![station wifi mode](/esp_wifi_station.png)

***Station*** means ESP32 board is connected to an Access Point (e.g. home router)

In this example we use IPv4 (old version)

***IPv4***

IPv4 format: xxx.xxx.xxx.xxx (numbers range from 0~255)

***Subnetwork*** (subnet): logical subdivision of an IP network that defines which devices can communicate directly without needing a router.

For example: If the local network uses 192.168.34.xxx and the subnet mask is 255.255.255.0, it means the first 3 numbers must be exactly the same for devices to be on the same local network. The last number must be unique to each device. If a device tries to reach an address where the first three numbers are different, the traffic is directed out to a router (and usually the internet).

***Default Gateway***: The router IP address (e.g., 192.168.1.1) that acts as an exit point for a local network. Any traffic destined for an IPv4 address outside the local 192.168.1.xxx subnet is sent to this gateway, which routes it to its next destination, such as another internal corporate network or the internet.

Below is a sample code to run Station mode on ESP32 S3 Wroom
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

Should expect output on serial monitor
~~~
Connected to router!
ESP32 IP address = 10.0.0.123
MAC address = 1C:DB:D4:56:FA:AC
Setup End
~~~
