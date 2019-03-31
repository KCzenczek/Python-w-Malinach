---
title: "Return of Red Button"
date: 2019-02-28T21:52:36+01:00
---
# Start with off, czyli zaczynamy od końca


Pomimo wielu zalet jakie posiada Malinka, można znaleźć jedną wadę, taką tycią. W sumie to nie należy rozważać w kategoriach wady lecz wyzwania jakie Malinka stawia przed nami :). 
Otóż chodzi o mały, jak wszystko  w RPi, ale całkiem przydatny guzik a w zasadzie jego brak. Zewnętrzny przycisk dzięki, któremu będzie można w sposób bezpieczny wyłączyć Malinkę. Teraz oczywiście też można zamknąć system za pomocą przycisku <strong>shutdown</strong>
lub komendy w terminalu <code>sudo shutdown -h now</code>. A co gdyby Malinka miała taki magiczny guzik, po naciśnięciu którego nastąpiłoby poprawne zamknięcie systemu? Nic prostrzego, można wykorztać stary dobry czerwony guzik :)
 

<strong>Czego potrzebuję?</strong>

Wszystko to, co jest niezbędne w poście [Red Switch](https://kczenczek.github.io/Python-w-Malinach/post/red-switch/)

<strong>Schemat podpięcia</strong>

Jest on niemal identyczny, dla urozmaicenia zmieniamy PIN sygnału na PIN 7, czyli GPIO 4.

<strong>Tak naprawdę teraz zaczyna się cała zabawa :)</strong>


Załóżmy, że mamy gotowy skrypt. Normalnie odpalamy go z linii komend. I dzieje się to co ma się zadziać, coś zaświeci, coś się 'wyprintuje', gdzieś pstryknie fotka itp. W tym przypadku dążymy do tego aby nasz skrypt był uruchamiany ze startem Malinki.
W sieci możemy znaleść kilka podpowiedzi jak to zrobić. W tym [artykule] (https://www.dexterindustries.com/howto/run-a-program-on-your-raspberry-pi-at-startup/) opisanych jest pięć sposobów.
Wybrałam opcję trzecią, czyli zamieszczenie naszego skrytpu o nazwie <code>power_OFF.py</code> w specjalnym folderze o nazwie <strong>init.d</strong>

Nie ma sensu aby się powtarzać, więc zachęcam do przeczytania. 
W skrócie przygotowany skrypt (o samym kodzie później)  [link do kodu] (https://github.com/KCzenczek/RPi-code/blob/master/Sensors_and_switches/power_OFF.py) 
należy umieścić w <code>/etc/init.d/</code>.
Nastepnie rozszerzyć uprawnienia <code>sudo chmod +x power_OFF.py</code>, później <code>sudo update-rc.d power_OFF.py defaults</code>komenda aktualizacji dowiązania do skrytpów startowych [więcej tu] (http://manpages.ubuntu.com/manpages/bionic/pl/man8/update-rc.d.8.html).Na koniec sugeruję ponownie uruchomiść Malinkę i ...można już wyłączać ją przyciskiem 

Jak wczejśniej wspomniałam, w kodzie znajdują się dwa rozwiązania, obydwa działają; w zależnożność które komu będzie bardziej odpowiadało.
Więcej info na temat zastosowanych metod z modułu RPi.GPIO [można przeczytać tu] (https://sourceforge.net/p/raspberry-gpio-python/wiki/Inputs/)


Hint: Na początek, żeby nie katować Malinki milionem prób ON/OFF i niepotrzebną frustracją, że coś nie działą, proponuję zbudować zwykły układ dla buttona; z prostym kodem - zamiast subprocess.call można użyć opcji <code>print 'Button works!' i wywołać plik jak do tej pory z linii komendy. I na zasadzie małych kroczków, jak coś działa dodawać kolejny element.


