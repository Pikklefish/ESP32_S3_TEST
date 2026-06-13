# ESP32_S3_TEST

## Wifi ESP 32 as Station 
![station wifi mode](/esp_wifi_station.png)

Station means ESP32 board is connected to the home router
IPv4 (old version) now we use IPv6

IPv4 format: xxx.xxx.xxx.xxx (numbers range from 1-255)
Subnet: sets the guideline for what is considered locl network.
For example: If local network is 192.193.343.xxx and subnet is 255.255.255.0 it means the first 3 numbers should be same and the last number can be unique to be considered local network (if it is different it will direct it to the internet) 
Gateway: the gateway to the internet (router gateway ie 192.193.343.1), all Ipv4 address not 192.193.343.xxx is routed to this gateway to be connected to the internet.
