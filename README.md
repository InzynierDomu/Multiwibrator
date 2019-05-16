# Multiwibrator

Pod wpisem o multiwibratorze na https://www.facebook.com/InzynierDomu/ pojawił się komentarz Pana Pawła Sujko. Z powodu ważnych informacji jakie były tam zawarte dorzucam jako ciekawą informacje.

"Ten multiwibrator jest pozornie prosty szczególnie w zakresie wzorów podawanych w literaturze, które są prawdziwe tylko dla bardzo konkretnych warunków pracy.
Po pierwsze, to oprócz tolerancji wartości rezystorów, na czas trwania danej fazy ma też wpływ tolerancja wartości pojemności C1 i C2, która dla nowszych kondensatorów może wynosić +/-20% wartości nominalnej, a w gorszych przypadkach nawet od -10 do +50% wartości wydrukowanej na obudowie.
Po drugie wzory na czas danej fazy pracy, tj. 
t1 ~ 0.7*C2*R3, t2 ~ 0.7*R2*C1
są dużym przybliżeniem rzeczywistości pod następującymi warunkami:
1) Napięcie zasilania układu jest dużo większe od napięcia przewodzenia złącza baza-emiter tranzystora aktualnie przewodzącego, tj. Ube
2) w obwodzie kolektorów tranzystorów są TYLKO rezystory, a nie ma ŻADNYCH diod (LED czy innych)
3) prąd przewodzenia włączonego tranzystora jest na tyle mały, że można zaniedbać jego napięcie przewodzenia (Uce_sat)
W innych przypadkach, tj. małe napięcie zasilania, dodatkowe diody w obwodzie kolektora czy w obwodzie bazy, mnożnik we wzorze na czas trwania danej fazy pracy będzie bardzo różny od 0.7.
W przypadku podstawowym (bez diod w kolektorach), gdy dany tranzystor nie przewodzi, to kondensator w danej gałęzi ładuje się przez rezystor kolektorowy do napięcia Uc=Ucc-Ube i osiąga tę wartość z dużą dokładnością gdy stała czasowa ładowania, przykładowo R4*C2 jest co najmniej 4.6 raza większa od stałej rozładowania R3*C2. Gdy następuje przełączenie, to napięcie na kolektorze tranzystora Q2 spada prawie do zera, a dokładniej do wartości napięcia nasycenia tranzystora zależnej od jego prądu kolektora, a ponieważ C2 jest naładowany, to napięcie na bazie Q1, tuż po przełączeniu wynosi:
Ub1 = Uce2sat-Ucc+Ube
co powoduje głębokie zatkanie tranzystora T1.
Kondensator C2 zaczyna się przeładowywać w obwodzie Ucc, R3 i przewodzący tranzystor Q2. Gdy napięcie na bazie Q1 osiągnie poziom przewodzenia, tj. ~Ube, to tranzystor Q1 zaczyna przewodzić i w układzie następuje przerzut do drugiego stanu.
Rzeczywisty czas przeładowywania C3 jest opisany "prostym" wzorem ;)
t1=R3*C2*ln ((2*Ucc-Ube-Ucesat) / (Ucc-Ube))
Z tego widać, że jeżeli napięcie Ucc jest dużo większe od Ube (i Ucesat), to Ube i Ucesat we wzorze można pominąć i wzór upraszcza się do postaci:
t1=R3*C2*ln(2*Ucc/Ucc)=R3*C2*ln(2) ~ 0.693*R3*C2 ~0.7*R3*C2
czyli tak jak podają książki. 
Jeżeli jednak Ucc jest małe, np. 3V, to współczynnik zaczyna się zmieniać:
k = ln ((2*3V-0.7V-0,1V) / (3V-0.7V)) = 0.816 > 0.7
Gdy bateria się rozładuje do 2.5V, to współczynnik k wzrośnie do 0.847.
W układzie z diodami LED w kolektorach, kondensatory ładują się do napięcia niższego niż to wcześniej podane czyli do:
Uc = Ucc-Uled-Ube
a więc po przerzucie czas przeładowania kondensatora do napięcia Ube będzie krótszy, bo kondensator zaczyna przeładowanie od mniejszego napięcia. Wzór na mnożnik czasu się zmienia:
k =ln ((2*Ucc-Uled-Ube-Ucesat) / (Ucc-Ube))
i np. przy Ucc=3V, Uled=2V, Ube=0.7V, Ucesat=0,1V
k = ln (2*3V-2V-0.7V-0.1V)/(3V-0.7V) = 0.33 czyli ponad 2 razy mniej niż 0.7 podawane w wersji uproszczonej.
Ważnym czynnikiem jaki należy uwzględnić przy użytkowaniu takich multiwibratorów jest napięcie ich zasilania, które nie tylko wpływa na częstotliwość ich pracy ale też na ... TRWAŁOŚĆ układu.
W stanie zatkania tranzystora, ma on na bazie duże napięcie ujemne. Dokąd to napięcie jest niższe niż napięcie przebicia złącza baza emiter odwrotnie spolaryzowanego, to układ jest bezpieczny. Jeżeli jednak jest większe, to złącze BE zachowuje się jak dioda Zenera o napięciu przewodzenia ok. 5 do 7V i przez tranzystor niby spolaryzowany zaporowo zaczyna płynąć spory prąd, który może uszkodzić tranzystor (odpala połączenie baza emiter).
Tak więc w układach zasilanych z większych napięć, tj, powyżej 7V należy do układu dodać dwie diody, np. typu 1N4148, włączone szeregowo z bazami tranzystorów, które zapobiegną przebiciu złącz baza-emiter tranzystorów)."
