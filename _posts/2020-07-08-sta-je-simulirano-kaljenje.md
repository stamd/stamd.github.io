---
layout: post
title: Šta je simulirano kaljenje?
subtitle : Kaljenjem čelika se taj metal greje, a zatim pušta kroz strogo kontrolisani proces postepenog hlađenja, čime se on oplemenjuje i čini se čvršćim. Sličan princip se može primeniti i na optimizaciju algoritama!
tags: [MATF, Racunarska Inteligencija]
author: Dimitrije Stamenić
comments : True
---

Postepeno hlađenje se u algoritmu simuliranog kaljenja tumači kao postepeno smanjivanje verovatnoće da se loše rešenje problema prihvati, kako se prostor rešenja istražuje. To znači da se daljom pretragom prostora rešenja dolazi do sve optimalnijeg rešenja.
Simulirano kaljenje se može prikazati sledećim pseudokodom:
(1) Generisati pocetno resenje s
(2) Inicijalizovati vrednost najboljeg resenja f* = f(s)
(3) Dok nije ispunjen uslov zaustavljanja, ponavljaj:
    (3a) Izabrati proizvoljno resenje s' u okolini resenja s
    (3b) Ako je f(s') < f(s), onda je s = s'
    (3c) Ako je f(s') >= f(s), onda:
        (3c1) Azurirati vrednost opadajuce funkcije p
        (3c2) Izabrati proizvoljno q iz intervala [0,1]
        (3c3) Ako je p > q, onda s = s'
    (3d) Ako je  f(s') < f*, onda je f* = f(s')
(4) Ispisati vrednost resenja f*
Pojašnjenja pseudokoda
Funkcija f() - funkcija cilja, što je manja vrednost, to bolje.
Funkcija p() - unapred definisana funkcija, opadajuća na (0,1). Označava verovatnoću pomeranja ka lošijem rešenju. Služi da bi se omogućilo i povremeno prihvatanje rešenja čija vrednost nije bolja od vrednosti trenutnog. Time se osigurava valjanost konačnog rešenja, smanjuje se verovatnoća da se kaljenjem pronađe samo lokalni (a ne globalni) optimum. Svakom iteracijom se smanjuje verovatnoća da se lošije rešenje uzme kao konačno (funkcija p opada, od verovatnoće 1, do 0). U slučaju da se nikada ne prihvataju lošija rešenja, algoritam bi postao lokalna pretraga sa velikom verovatnoćom da se zaglavi u lokalnom optimumu.
Vrednost funkcije p() birmao tako da bude pogodno, u zavisnosti od prirode problema. Na primer p=ln⁡2/ln⁡(1+i), p=1/sqrt(i)… Gde je i trenutni broj iteracija.
Kriterijum zaustavljanja - dostignut maksimalni broj iteracija, dostignut maksimalan broj ponavljanja istog najboljeg rešenja, ukupno vreme izvršavanja…
Simulirano i pravo kaljenje
Na osnovu prethodnog možemo da zaključimo kako funkcioniše algoritam simuliranog kaljenja i kako se može napraviti analogija sa kaljenjem čelika.
Na početku uzimamo nasumično rešenje, grejemo čelik do zadate temperature. Zatim polako kontrolisano ispitujemo kvalitet okolnih rešenja.
Logično bi bilo da samo bolja okolna rešenja prihvatamo kao konačna, ali tada ne bismo dobli traženo svojstvo, da se pronađe globalno optimalno rešenje.
Zato omogućavamo da se u početku, dok je temperatura još uvek visoka (p ima vrednost blisku jedinici), kao trenutna rešenja uzimaju i rešenja koja nisu najbolja, da bismo proširili prostor pretrage i da se ne bismo zaglavili u lokalnom optimumu.
Kako vreme odmiče, temperatura polakao opada, vrednost funkicje p je sve bliža nuli i verovatnoća da se lošije rešenje uzme u obzir kao konačno se smanjuje sve do nule.
Na kraju smo sigurni da smo pronašli globalno optimalno rešenje, da naš čelik ima željena svojstva!
Izvori:
