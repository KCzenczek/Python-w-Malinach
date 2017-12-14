---
title: "Red Switch"
date: 2017-11-11T14:49:17+01:00
---

# Lord of the Red switch

Ostatnio omówiłam i przetestowałam sposób komunikowanie się Malinką za pomocą GPIO output, poprzez zaprogramowaną przez nas sekwencję zapalania się i gaśnięcia dwóch diod LED, rzecz jasna czerwonych ;)

Tym razem spróbuję wywołać zdarzenie w naszym, zewnętrznym świecie i zobaczymy jak na to zareaguje Malinka. Podepnę nic innego jak zwykły przełącznik chwilowy ON-OFF, koloru... czerwonego :)

<strong>Czego potrzebuję?</strong>

- 1 x płytka stykowa
- 1 x przełącznik chwilowy ON-OFF
- 2 x rezystor - jeden rezystor 10k Om oraz drugi wystarczy 1k Om. (Aczkolwiek, w moich zasobach był jedynie 1,2k Om. Też zadziałał, później wyjaśnię dlaczego i jak)
- 3 x kabelek męsko-żeński

<strong>Schemat podpięcia jest następujący:</strong>

![schemat](/img/connection_switch.png)

Zaczynamy od PIN 16 czyli zwykłego zielonego GPIO 23 (w skrócie GP23), który łączymy niebieskim kabelkiem z płytką stykową w a7. Teraz uwaga pierwszy rezystor :) Rzecz jasna z punktu widzenia poprawności budowanego obwodu nie jest on konieczny, a zatem jaką on ma pełnić funkcję? Otóż instalujemy go jako rodzaj zabezpieczenia. W momencie, gdy w naszym kodzie zamiast ustawić GPIO.setup na GPIO.IN, w wyniku choćby jakiegoś rozkojarzenia, ustawimy na GPIO.OUT to wcześniejszy montaż rezystora uchroni PIN a nawet całą Malinkę przed niechybnym uszkodzeniem.
Tak więc jedną nóżkę rezystora 1k Om wpinamy w c7, drugą w c4.
Wracając do wiersza 7 wpinamy w dowolne miejsce np. d7 jedną nóżkę drugiego rezystora 10k Om, tzw. 'rezystora obniżającego' (za chwilkę wyjaśnię), a drugą w nowy wiersz np. d11. W tym samym wierszu np. w a11 czarnym kabelkiem łączymy z PIN 25 czyli GND.
PIN 1, czyli źródło zasilania 3,3V wpinamy zielonym kabelkiem w a1. Następnie w tym samym wierszu wpinamy np. e1 jedną nóżkę przełącznika ON-OFF, a drugą wpinamy w wiersz 4 np. w e4. W ten sposób wróciliśmy do wiersza, w którym podpięta jest druga nóżka 'małego rezystora'. Obwód zamknięty.
Teraz krótkie wyjaśnienie, o co chodzi z rezystorem obniżającym - otóż PIN 16 w powyższym układzie, znajduje się w stanie niskim z powodu podłączenia właśnie tego rezystora do GND. Gdybyśmy rezystor 10k Om podpięli do PIN 1 czyli 3,3V a przełącznik chwilowy ON-OFF do GND, wówczas PIN 16 znajdowałby się w stanie wysokim a rezystor 10k nazwany by został rezystorem podciągającym, z powodu podciągania do źródła zasilania 3,3V. Wówczas PIN znajdowałby się w stanie wysokim, a po naciśnięciu przełącznika przeszedłby do stanu niskiego. 

Wracając jednak do naszego schematu z rezystorem obniżającym wygląda to tak, w momencie 'nie-naciśnięcia' przycisku obwód jest uziemiony, w momencie naciśnięcia, przechodzi w stan wysoki (zaczyna płynąć prąd). 
O tej właśnie zmianie (tzn. o przyciśnięciu guzika) informujemy Malinkę za pomocą PIN 16, a programem sterujemy co wówczas ma się zadziać.
 
<strong>Trochę kodu</strong>

[Link do kodu] (https://github.com/KCzenczek/RPi-code/blob/master/Sensors_and_switches/switch.py)

Plik uruchamiam analogicznie jak w poprzednim poście. I taadaa! Działa! 

Na ekranie mamy wyświetlajęcy się pierwszy komunikat. Po wciśnięciu guzika, komunikat zmienia się na drugi. Ile razy możemy wcisnąć guzik? Tyle razy na ile mamy ochotę :)
Ponieważ zastosowaliśmy pętlę while True bez ograniczenia, kod będzie działał dopóki nie włączymy Ctrl + C. 


Dla zaciekawionych:<br>
No dobrze był stan niski oraz stan wysoki. A czy może być 'nijaki'? Otóż tak :) Z tym, że nazywa się troszkę inaczej. W ang. jest na to określenie 'floating', po polsku możemy opisać ten stan jako PIN niepodpięty, czyli nie możemy jednoznacznie określić jego logicznej wartości 0 czy 1. Chociaż nie polecam takich zabaw, to żeby osiągnąć ‘floating’ trzeba podpiąć PIN 16 - przełącznik ON-OFF - 3.3V, czyli bez GND.
Podczas przygotowania tego materiału przypadkiem udało mi się osiągnąć, ten stan gdyż mając wszystko podpięte zgodnie z naszym schematem (co ważne miałam podpięte rezystory!!!) nie zauważyłam, że PIN GND wysunął mi się z Malinki - łobuz wyskoczył z gniazda. A co na to Python? Szalał pokazując na zmianę komunikaty z printów, bez mojego współudziału w postaci naciskania guzika, oczywiście czerwonego… 😊.
