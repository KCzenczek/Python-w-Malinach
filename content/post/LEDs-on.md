---
title: "Niech stanie się Jasność"
date: 2017-10-11T18:17:54+02:00
---

# LED's On

Zaczniemy od najważniejszego czyli komunikacji z Malinką. Jak sama nazwa wskazuje port GPIO czyli General Purpose Input Output umożliwia Malince komunikację na dwa sposoby.

W moim tłumaczeniu:
- input - czyli wszystko to co jest sczytywane/odbierane ze świata zewnętrznego przez Malinkę, inaczej dane które do niej 'wpadają' np. rozmaite informacje z czujników czy wciskany w danym momencie przez nas guziki, najczęściej czerwone (i nie mam pojęcia dlaczego najczęściej w tym kolorze).
- output - czyli to co chcemy aby 'wyszło' poprzez Malinkę do świata zewnętrznego, chcemy aby coś zadziało się poprzez Malinkę, np. nagle coś zaświeciło, nagle coś pojechało do przodu lub w bok.

Tak więc klasyczne zapalanie diody LED będzie przykładem wykorzystania GPIO jako outputu.
   
1. Czego potrzebuję?

Poza naszym komputerkiem, dobrze mieć:
- 1 x płytka stykowa - moja wygląda prawie dokładnie jak ta, którą namalowałam w schemacie. Prawie, ponieważ moja jest przeźroczysta, co doprowadza mnie do oczopląsu podczas podłączania. Serio! Zdecydowanie odradzam używanie przeźroczystej płytki stykowej.
- 2 x dioda LED - nie powinnam pisać, że kolor nie ma znaczenia, gdyż ma. Chodzi o napięcie jakie odkłada się na diodzie. Wystarczy sprawdzić specyfikację diody, rzecz jasna jeśli producent dołączył. Jeśli nie mamy dostępu do tej informacji, bardzo bezpieczne okaże się użycie rezystora 470 Om, dla dowolnego koloru diody LED. 
- 2 x rezystor - wspomniany powyżej 470 Om. Tak naprawdę dla tej diody wystarczy rezystor powyżej 50 Om. Zainteresowanym metodą doboru odpowiedniego rezystora polecam [Jak dobrać rezytor do diody](https://forbot.pl/blog/jak-dobrac-rezystor-do-diody-rozne-metody-zasilania-led-id14482)
- 3 x kabelek męsko-żeński

2. Schemat podpięcia jest następujący:

![schemat](/img/connection_base_two_red.png)

PIN 6, czyli uziemienie (GND) czarnym kabelkiem (tu kolor kabli zupełnie nie ma znaczenia, kwestia czytelności schematu) wpinam w drugi rząd (czyli "-"). Co do "+" i "-" są to rzędy, których wejścia są połączone w PIONIE, co w naszym przypadku oznacza, że GND mamy teraz w całym drugim rzędzie.

W dowolne wejście drugiego rzędu wpinam jedną nóżkę rezystora, a drugą w wejście np. a4. W tym samym tj. 4 wierszu wpinam KRÓTSZĄ nóżkę diody np. d4, a dłuższą w sąsiednim wierszu np. d3.

Drugim kabelkiem (różowym) zamykam obwód pierwszej diody czyli jedną końcówkę wpinam w a3 na płytce, a drugi koniec w PIN 7 czyli GPIO 4 (na schemacie opisana w skrócie GP04). Analogicznie podpinam drugą diodę zaczynając od rzędu z uziemieniem, a kończąc na niebieskim kabelkiem w GP17.

Co do zasady mamy do dyspozycji wszystkie PIN-y oznaczone GP, co jest skrótem od GPIO. 

Ale jak widać niektóre GP są zielone inne różowe czy niebieskie. Otóż wszystkie GP poza kolorem zielonym mają jeszcze dodatkowe funkcje. Wychodzę z założenia, że lepiej nauczyć się używać w pierwszej kolejności tych GP, które mają jedno przeznaczenie jako INPUT/OUTPUT, czyli w tym przypadku oznaczone są kolorem zielonym. Jak widać jest ich sporo więc nie powinno braknąć. 

3. Trochę kodu

Po uruchomieniu Malinki, wchodzimy do terminala, wpisujemy $ IDLE3, aby uruchomić Pythona 3 (bez 3 uruchomimy, rzecz jasna wersję 2).

Tworzymy nowy plik, a w nim piszemy:

import RPi.GPIO as GPIO
import time


GPIO.setmode(GPIO.BOARD)
chan_list = [7, 11]
GPIO.setup(chan_list, GPIO.OUT)

for x in range(0, 10):
    GPIO.output(chan_list, (GPIO.HIGH, GPIO.LOW))
    time.sleep(.5)
    GPIO.output(chan_list, (GPIO.LOW, GPIO.HIGH))
    time.sleep(.5)

GPIO.cleanup()


4. Jak 'odpalić' plik?

Zapisujemy plik i odpalamy F5.
Taaadaaa!!!

Dla chętnych: dokładając trzecią diodę LED zieloną, a druga czerwoną zamieniając na żółtą i dodając parę linijek w kodzie można zbudować sobie sygnalizacje świetlną :)
