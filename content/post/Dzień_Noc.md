---
title: "Dzień_Noc"
date: 2018-01-13T20:00:30+01:00
---

# Czy ktoś widział kotecka? - zapytał Tweety

Kolejny projekt chciałam aby był z gatunku praktycznych, lub prawie praktycznych. Wyobraźmy sobie, jest noc i coś się kręci pod oknami. Co zrobić? Najlepiej zaświecić światło i sprawdzić. 

Można też zaopatrzeć się w lampę z czujnikiem ruchu, tzw. 'fotokomórka' lub... można zbudować ją samemu :)

<strong>Co się przyda?</strong>

Dla większej przejrzystości podzielę sobie wszystkie elementy na dwa 'zespoły' czujników:
1. <b>Czujnik PIR</b> - czyli wszystko to, z czego korzytałam w ostatnim projekcie:
- 1 x płytka stykowa
- 2 x dioda LED - zielona i oczywiście czerwona
- 2 x rezystor - dla każdej z diod np. wcześniej już wykorzystywany 470 Om.
- 1 x czujnik ruchu PIR - z poprzedniego projektu 
- 4 x kabelki męsko-żeńskie
- 2 x kabelki żeńsko-żeńskie

2. <b>Czujnik 'odbiciowy' IR</b> - czyli ang. [Reflective IR Sensor] (https://www.adafruit.com/product/2349); więcej info w wersji [PL] (https://botland.com.pl/transoptory-odbiciowe/52-czujnik-transoptor-odbiciowy-cny70.html)
- 2 x dioda LED - raz jeszcze zielona i oczywiście czerwona
- 3 x rezystor 470 Om - dwa dla dwóch diod LED + jeden dla czujnika IR, a w zasadzie dla diody tam się znajdującej
- 1 x rezystor 10 kOm
- 1 x rezystor 330 Om
Żeby się nie pogubić w kolorach pasków, mam mocno pomocną stronkę [Rezystor - kod kod paskowy] (http://serwis-tv.com/opornik.html)
- 1 x czujnik 'odbiciowy' IR 
- 5 x kabelków męsko-żeńskie
- 1 x kabelek męsko-męski

<strong>Schemat podpięcia przedstawia się następująco:</strong>

![schemat](/img/connection_IR_PIR_LEDs.png)

<strong>Kod</strong>

[Link do kodu] (https://github.com/KCzenczek/RPi-code/blob/master/Sensors_and_switches/IR_PIR_LEDs.py)

Cel jaki sobie postawiłam to zbudowanie modułu wykrywającego ruch w nocy.
Po uruchomieniu programu zakładamy, że jest "dzień", co potwierdzi świecąca się czerwo dioda z teamu IR. Aby uaktywnić zieloną, muszę zasłonić czujnik IR kartką papieru pomalowaną na czarno (2cm x 2cm wystarczy; czasem lecz nie zawsze działa nawet zasłonięcie czujnika palcem). Po zaświeceniu się zielonej, przechodzę do drugiego teamu. Tutaj od początku świeci się zielona, co oznacza, że nasz czujnik działa i jest gotowy na wykrycie ruchu. Jeśli teraz jakiś długopis czy np. kot przebiegnie przed czunikiem PIR, zgaśnie zielona i zaalarmuje nas czerwona dioda. Po kilku sekundach czerwona zgaśnie i ponownie zaświeci się zielona.
Jeśli z czujnika IR zdejmiemy czarną od spodu kartkę, będzie to oznaczało, że jest dzień i czujnik PIR nie będzie aktywowany.

