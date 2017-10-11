---
title: "Pierwszy post"
date: 2017-09-08T20:02:43+02:00
---

# First thing first 

Chciałam rozpocząć od opisania prostego podpięcia diody LED, ale gdy zaczęłam wyliczać jakie elementy są do tego niezbędne, szybko uświadomiłam sobie, że dla takich osób jak ja, które naprawdę zaczynają od zera (czyli kliknięcia w guzik w sklepie internetowym z pierwszą Malinką w koszyku), ważne będzie porządne wprowadzenie, no i  postanowiłam zrobić jeszcze jeden krok w tył.

Tak więc:

1. Wybór Malinki i nie tylko

Tak jak wspomniałam, moją przygodę z Malinką zaczynam na Raspberry Pi Zero, ponieważ na dzień dobry nie potrzebuję dużej mocy. Jej mały procesor, mała prądożerność i małe gabaryty powodują, że będzie idealna do moich pierwszych małych projektów.

Prawda, jest jeden haczyk. Trzeba samemu wlutować gniazdo GPIO (General Purpose Input Output – którym zajmę się w dalszej części). Ostatnio jednak pojawiły się w sprzedaży Malinki z wlutowanym gniazdem, ale jeśli czynność ta nie jest dla Ciebie czymś odstraszającym lub masz 'starszego brata', który Ci pomoże to naprawdę warto. 

Oczywiście nie obeszło się bez wcześniejszego wygooglowania i sprawdzenia jak samemu się za to zabrać. Moja Malinka okazała się bardzo dzielnym pacjentem i przeżyła ten zabieg. 

Sama Malinka to nie wszystko. Jak przystało na porządny komputer potrzebujemy jeszcze monitora, klawiatury, myszki i całego okablowania.

Czy będzie to duży monitor, czy mały np. 5" ekranik dedykowany tym maleństwom, nie ma znaczenia. Co jest ważne, to żeby miał wbudowane wejście HDMI. Oczywiście niezbędna będzie przejściówka microHDMI – HDMI, gdyż jak to w Malince Zero wszystko jest micro.
Klawiatura najlepiej (ale niekoniecznie) z touchpadem. Dlaczego? Ponieważ RPi Zero ma tylko jedno microUSB. 

Skoro już jestem przy USB, zdecydowanie warto zaopatrzyć się w rozgałęziacz. Może to być od razu z wbudowaną przejściówką microUSB - USB.

No właśnie, kable i przejściówki.

Wydaje mi się, że warto pierwszą Malinkę kupić w zestawie, tzn. z zasilaczem, przejściówkami, różnymi wersjami gniazd GPIO czy obudową. Jasne, że można też oddzielnie, ale z ekonomicznego punktu widzenia to się raczej nie będzie kalkulować. 
Przy zakupie kolejnej Malinki, dokładnie Raspberry Pi Zero W, jak to było w moim przypadku, byłam już bardziej świadomym klientem i wiedziałam czego potrzebuję, co mi zostało z poprzedniego zestawu i co mogę wykorzystać jeszcze raz. 

Mój podstawowy zestaw do pracy:

- Malinka z [Raspberry Pi Zero All in One] (https://botland.com.pl/moduly-i-zestawy-raspberry-pi-zero/8755-zestaw-raspberry-pi-zero-all-in-one.html)
- Klawiatura z touchpadem - iPazzPort 
- Ekran dotykowy rezystancyjny LCD TFT 5'' 
- HUB Rozdzielacz HOST OTG Micro 3 x USB

Ciekawostka: Do testowania niektórych projektów na dwie Malinki wystarczy jeden zasilacz. Magia? Otóż nie, okazało się bowiem, że w niektórych przypadkach wystarczy Malinkę po prostu zasilić Power Bankiem :)  

2. Karta micro SD (+ adapter do karty)

Do wyboru do koloru, serio.

Ponieważ wiedziałam, że czeka mnie zabawa z osadzeniem Rasbiana i jak znam siebie, pewnie kliknę coś nie tak (i nie należy wykluczać „kabum”), dlatego postanowiłam zaopatrzyć się w najmniejszą i prawie najtańszą kartę 8GB - co by po kieszeni nie bolało. Dlaczego prawie? Ponieważ dobrze aby karta miała klasę 10. Jak na razie 8GB daje radę, nie narzekam (i tak, polecam od razu dwie, ale o tym za chwilę).

Jeden adapter w zupełności wystarczy, nawet gdy się będzie miało wiele kart dla kilku Malinek bądź wszystkie karty z różnymi projektami dla jednej Malinki - trochę relacjami bazodanowymi poleciało :)

3. System operacyjny

Generalnie, na stronie [Fundacji Raspberry] (https://www.raspberrypi.org/downloads/) znajdują się dwa systemy operacyjne. 

Nie ma sensu tworzyć kolejnej szczegółowej odsłony 'instalacji krok po kroku', 
dlatego polecam albo [oryginał] (https://www.raspberrypi.org/documentation/installation/installing-images/README.md)

albo wersję [pl] (http://malinowepi.pl/post/39744941523/instalacja-systemu)

Zdradzając jak to wyglądało u mnie, w skrócie:

1. Ściągnełam [Raspbiana] (https://www.raspberrypi.org/downloads/raspbian/)
2. Potem ściągnełam i zainstalowałam [Etchera] (do zapisywania zdjęć na karcie SD) (https://etcher.io/) 
2. Wsadziłam micro SD do adaptera, a to wszystko do laptopa
3. Odpaliłam Etchera i zgodnie z pojawiającymi się trzema komunikatami zrobiłam 'flasha' Raspbiana na micro SD.

Koniec 
 
Obie moje Malinki działają na Raspbianie i nie mam żadnych zastrzeżeń.


4. Odpalamy Malinkę

Przede wszystkim zwróćcie uwagę, że Malinki nie mają On/Off, czyli włączenie następuje poprzez zwykłe podpięcie do źródła prądu, czy to gniazdko czy też Power Bank.

Prąd płynie działa, nie płynie nie działa :)

W razie problemów polecam [Problemy z uruchomieniem RPi] (http://blog.r-pi.pl/2013/11/problemy-uruchomieniem-rpi/)

Piszę o tym wszystkim bo jak się okazało u mnie problem był nie z pierwszym, ale z drugim uruchomieniem !

Tak, zamykanie Malinki bywa triki, zwłaszcza gdy się ma nieprzeźroczystą obudowę i ciężko jest dostrzec migające w Malince na zielono małe światełko. Wszystko wskazuje na to, że za wcześnie wyjęłam wtyczkę z gniazda i uszkodziłam kartę SD. I właśnie w tym momencie z ratunkiem przyszła druga karta :)

Od tego czasu obie Malinki mają przeźroczystą obudowę, a po kliknięciu w 'Shotdown', nie spuszczam oka z zielonego światełka. Dopiero jak przestanie do mnie mrugać (plus dodatkowe 5 sekund dla pewności) wyciągam wtyczkę.


