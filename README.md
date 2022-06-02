# Practica-3 WIFI Y BLUETOOTH

En aquesta pràctica aprendrem el funcionament del WIFI i del Bluetooth, és per això que realitzarem una pràctica on generarem una web utilitzant le ESP32 i una 
comunicació sèrie amb una aplicació d'un mòbil amb bluetooth.

# Material
- ESP32
- Telèfon Mòbil

# Funcionament

Començem amb els includes i una funció per a fer el log in a la xarxa wifi desitjada

```c++
#include <WiFi.h>
#include <WebServer.h>
// SSID & Password
const char* ssid = "*****"; // Enter your SSID here
const char* password = "*****"; //Enter your Password here
WebServer server(80); // Object of WebServer(HTTP port, 80 is defult)
```

COmençem el setup, inicialtizem el port sèrie i ens connectem a la xarxa wifi desitjada, un cop realitzat això, haurem d'nicialitzar el server.

```c++
void setup() {
Serial.begin(115200);
Serial.println("Try Connecting to ");
Serial.println(ssid);
// Connect to your wi-fi modem
WiFi.begin(ssid, password);
// Check wi-fi is connected to wi-fi network
while (WiFi.status() != WL_CONNECTED) {
delay(1000);
Serial.print(".");
}
Serial.println("");
Serial.println("WiFi connected successfully");
Serial.print("Got IP: ");
Serial.println(WiFi.localIP()); //Show ESP32 IP on serial
server.on("/", handle_root);
server.begin();
Serial.println("HTTP server started");
delay(100);
}
```

Un cop fet això, entrem al loop.
Dins d'aquest creem la pàgina web i escrivim els continguts que volem que surtin pel display a la web del servidor.

```c++
void loop() {
server.handleClient();
}
// HTML & CSS contents which display on web server
String HTML = "<!DOCTYPE html>\
<html>\
<body>\
<h1>My Primera Pagina con ESP32 - Station Mode &#128522;</h1>\
</body>\
</html>";
// Handle root url (/)
void handle_root() {
server.send(200, "text/html", HTML);
}
```



https://user-images.githubusercontent.com/101885469/171612234-59a084b6-94ea-4d9d-bb08-7521119d3db5.mp4


