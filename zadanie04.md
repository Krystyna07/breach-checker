zadanie 1

Opdpowiedz na health przegladarki:
{"status":"ok"}

linia z docker logs:
172.18.0.1 - - [12/Nov/2026 07:38:43] "GET /health HTTP/1.1" 200

zadanie 2



zadanie 3

Po restarcie:
PS C:\Users\krysia\metody_wirtualizacji_laby\projekt\breach-checker> docker exec backend cat /tmp/notatka.txt
notatka

Po run + rm:
PS C:\Users\krysia\metody_wirtualizacji_laby\projekt\breach-checker> docker exec backend cat /tmp/notatka.txt
cat: /tmp/notatka.txt: No such file or directory

Zawartośc historia txt:
PS C:\Users\krysia\metody_wirtualizacji_laby\projekt\breach-checker> docker run --rm -v breach-dane:/dane alpine sh -c "date >> /dane/historia.txt; cat /dane/historia.txt"
Thu Nov 12 07:47:04 UTC 2026
Thu Nov 12 07:47:14 UTC 2026

Dlaczego plik w /tmp przetrwał restart, ale nie rm?
Docker restart zachowuje warstwę zapisywalną, z kolei docker rm ją kasuje 

Dlaczego historia.txt przetrwała, choć oba kontenery zostały usunięte; 
Ponieważ dane, które miały prztrzetrwać zostały zapisane w wolumenie, który to umożliwia.

Czy lista wycieków przetrwałaby docker rm i dlaczego?
Nie - jak powyżej lista wycieków zapisana wyłącznie wewnątrz kontenera nie przetrwa polecenia docker rm, chyba że została zapisana na zewnętrznym wolumenie.