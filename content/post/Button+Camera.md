---
title: "Button+Camera"
date: 2019-01-13T18:26:19+01:00
draft: true
---

# Press the button and 'say cheese'

A co gdybyśmy chcieli zrobić zdjęcie osobie, która odwiedza nas kiedy nie ma nas w domu, uparcie dzwoniąc do drzwi? Z rozwiązaniem może przyjśc Malinka. 
Poniżej opiszę jak możemy zaiprowizować rozwiązanie. Wyobraźmy sobie, że nasz dzwonek to nic innego jak zwykły przełącznik ON-OFF, najlepiej ten czerwony ;) Do tego będziemy jeszcze potrzebować kamery. 
W ninijeszym poście nie podejmuję się opisywania instalacji rozwiązania w 'ścianie'. W takim przypadku dobrze byłoby zasięgnąć rady zaprzyjaźnionego elektryka.

<strong>Czego potrzebuję?</strong>

- [To co jest potrzebne tu] (https://kczenczek.github.io/Python-w-Malinach/post/red-switch/)
- kamerka RPi - dla przykładu [Raspberry Pi Camera] (https://botland.com.pl/pl/kamery-dla-raspberry-pi-i-akcesoria/6124-raspberry-pi-camera-hd-v2-8mpx-oryginalna-kamera-dla-raspberry-pi-6405227108814.html) 

<strong>Schemat podpięcia</strong>

Jeśli chodzi o przełącznik, jest on analogiczny jak w poście 'Red switch'
W kwesti podpięcia kamerki, a może to być nieco triki, proponuję [krótką instrukcję] (https://www.youtube.com/watch?v=zFAX4pH1BPA)
I dobra rada uważajcie na delikatne, czarne 'mocowanie' kamerki przy Malince. U mnie 'samo' zepsuło się już przy dwóch Mainkach. Jak później czytałam w necie, jeśli coś się psuje w kamerce to na 80% ten czarny 'dings'.
 
<strong>Trochę kodu</strong>

[Link do kodu - python] (https://github.com/KCzenczek/RPi-code/blob/master/Camera/button_camera.py)

[Link do kodu - bash] (https://github.com/KCzenczek/RPi-code/blob/master/Camera/photo.sh)

Kilka słów o pliku .sh Jest to skrytp bashowy, który będzie wywowływany jako subproces w naszych głównym pliku pythonowym. Za pomocą komendy <code>raspistill -o photo_name.jpg</code> robione jest zdjęcie. Dla przetestowania działania samej kamery możemy ją wpisać w terminalu. Możemy również podać dokładne miejsce zapisywania zdjęć, podając pełną ścieżkę np. <code>/home/pi/Desctop/projects/photo.jpg</code>. Jeśli chodzi o parametry <code>-vf</code> oraz <code></code> są opcjonalne. Oznaczają vertical flip (obrót pionowy) i horizontal flip (obrót poziomy) i zależą wyłącznie od fizycznego ustawienia kamerki.
Ponieważ każde zdjęcie będzie miało w nazwie datę i czas tzw.timestamp, o ile w ciągu tej samej minuty nie będziemy chcieli zrobić więcej niż jendnego zdjęcia (pliki zostaną nadpisane - w skrócie starsze zostanie zastąpione nowszym), każde zdjęcie zostanie zapisane we wskazanym przez nas folderze na Malince.
Jeszcze jedna ważna info. Musimy zmienić uprawnienia dla tego pliku, aby można było go uruchomić wpisując komendę <code>$ chmod +x photo.sh</code>.
Więcej informacji o [prawie dostępu] (https://pl.wikipedia.org/wiki/Prawa_dost%C4%99pu) oraz [poleceniu chomd] (https://pl.wikipedia.org/wiki/Chmod)
Jeżeli chcielibyśmy sprawdzić poprawność pliku bashowego możemy uruchomić komendą <code>$./ file_name.sh</code> (będąc w konsoli w folderze z tym plikiem).

Następnie plik .py uruchamiam analogicznie jak w poprzednich postach. I możemy 'pstrykać' fotki. 

