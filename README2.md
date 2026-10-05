# ESPHome dla JSDSolar J4000E (wersja Direct TTL)

Projekt bezprzewodowej integracji falownika hybrydowego **JSDSolar J4000E** z Home Assistant przy użyciu ESPHome. 

## Status projektu: BAZA URUCHOMIONA 🚀
* **Autor:** hentto-oss
* **Sukces:** Udało się uruchomić stabilną komunikację Modbus bezpośrednio po Wi-Fi na działającym inwerterze i wyciągnąć pierwsze dwie konfiguracje.
* **Zadanie dla społeczności:** Projekt zostaje otwarty dla innych. Potrzebne jest dalsze mapowanie kolejnych rejestrów (holding/input registers) dla napięć, prądów i stanu baterii.

## Podłączenie sprzętowe (Pinout)
Komunikacja odbywa się bezpośrednio na poziomach logicznych TTL (3,3 V) z pominięciem jakichkolwiek konwerterów RS485 czy RS232. Poniższe zdjęcie przedstawia dokładne punkty lutownicze na płycie falownika:

![Pinout falownika](pinout.png)

### Schemat połączenia z zewnętrznym ESP32:
* **Pin 1 (GPIO39 jako TX)** -> podłącz do pinu **TX** (np. GPIO16) w ESP32
* **Pin 2 (GPIO38 jako RX)** -> podłącz do pinu **RX** (np. GPIO17) in ESP32
* **Pin 3 (VCC 3.3V)** -> opcjonalne zasilanie układu
* **Pin 5 (GND)** -> podłącz do pinu **GND** w ESP32 (**WYMAGANE!**)

## Bezpieczny kod bazowy YAML
W pliku `jsdsolar_j4000e.yaml` znajduje się gotowa konfiguracja. Zaimplementowano w niej zabezpieczenia dla pracującego inwertera (wyłączone logowanie po porcie szeregowym `baud_rate: 0`, aby ESP32 nie śmieciło w procesor falownika, oraz wyłączony reboot pętli Wi-Fi).

---
*Jeżeli uda Ci się zmapować kolejne rejestry tego falownika, śmiało twórz Pull Request! Niech ten projekt służy wszystkim.*
