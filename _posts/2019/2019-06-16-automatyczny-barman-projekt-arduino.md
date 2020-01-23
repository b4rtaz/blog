---
layout: post
title: "Automatyczny barman - projekt Arduino"
author: "b4rtaz"
image: "images/2019/2019-06-16-automatyczny-barman-cover.jpg"
tags: polish
---

Zawsze chciałem zrealizować jakiś projekt, który byłby trochę "bliżej metalu" w porównaniu z tym co robię na co dzień. Pewnego razu na domówce zaświtała mi idea stworzenia maszyny, która nalewa drinki. Spodziewam się, że na domówkach są różne polityki nalewania napojów. Goście polewają sobie sami, goście polewają między sobą. Jednak w sytuacji gdy to jedna osoba jest „barmanem” – czyli najczęściej gospodarz, to w przypadku już niewielkiej ilości gości jest to stanowisko bardzo absorbujące.

W sieci zrealizowanych przez pasjonatów DIY automatycznych bartenderów jest sporo, różnią się pod wieloma względami. Przejrzałem wiele z nich i postanowiłem wybrać kilka cech jakie oczekuje od przyszłego urządzenia. Moje wymagania były następujące:

- urządzenia musi potrafić miksować co najmniej dwa rodzaje drinków, np. wódka z colą albo wódka z sokiem pomarańczowym,
- po wybraniu drinka wszystko musi się dziać automatycznie,
- można dolać sobie do gotowego drinka większą ilość soku,
- konfiguracja drinków powinna odbywać się w samej maszynie,
- wymiana napojów powinna być szybka.

### Rezultat

Cały projekt zajął około 2 miesiące, przy czym najdłużej trwało kompletowanie potrzebnych części.

<div class="video">
	<iframe src="https://www.youtube.com/embed/cL-5Fz6_c98" frameborder="0" allowfullscreen></iframe>
</div>

### Koszty części

Poniżej przedstawiam poniesione koszty zakupowe za elementy potrzebne do zrealizowania projektu. Poniższy spis nie uwzględnia kosztów kabli, śrubek, materiałów potrzebnych do lutowania, kosztów przesyłek oraz kilku “drobnych” zakupów.

- płytka z mikrokontrolerem Arduino UNO - **17,80 zł**,
- zasilacz 12V - **11,60 zł**,
- belka tensometryczna NA27 1kg - **12,90 zł**,
- moduł wagi HX711 - **4,40 zł**,
- sterowniki silnika L293D - **2 x 2,60 zł**,
- korek gumowy karbowany - **1,59 zł**,
- wąż gumowy - **9,98 zł**,
- rezystory - **1,60 zł**,
- przyciski tact - **1,20 zł**,
- wyświetlacz OLED SSD1306 - **18,40 zł**,
- pompa membranowa 12V - **3 x 14,90 zł**,
- płyta MDF z wycięciem kształtów - **125,66 zł**,
- emaila do drewna (dwa kolory) - **8,98 zł + 9,98 zł**.

W sumie **273,99 zł**.