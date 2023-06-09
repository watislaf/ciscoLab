# ciscoLab
Osoby:
* Hubixo
* Remigiusz
* VladKoz
* wojexe

## Opis
Zadanie powinno byc zrobione w pakiet tracerze, plik znajduje sie w folderze.

![img.png](img.png)
 
 
## Rozwiazania
 #### 1. Adresacja sieci IPv4 z najmniejszej liczby adresow IP 10 [VladKoz] ✅
Adresacja sieci z najmniejsza liczba adresow:
przerabiamy algorytm z cwiczen, czyli bierzemy ilosc urzadzen+2 po czym liczymy minimalna potege dwojki i z tego dostajemy maske.
```
Siec Customer A:
    Podsiec 1.0.1.0 ma 2 urzadzenia  Maska 255.255.255.252 = /30
    Podsiec 1.0.2.0 ma 3 urzadzenia  Maska 255.255.255.248 = /29
    Podsiec 1.0.3.0 ma 2 urzadzenia  Maska 255.255.255.252 = /30
    Podsiec 1.0.4.0 ma 2 urzadzenia  Maska 255.255.255.252 = /30
    Podsiec 1.0.5.0 ma 2 urzadzenia  Maska 255.255.255.252 = /30
    Podsiec 1.0.6.0 ma 2 urzadzenia  Maska 255.255.255.252 = /30

Siec Customer B:
    11 urzadzen. 
    2.0.0.0 - siec. Maska 255.255.255.240 = /28

Siec Customer C:
    2 urzadzenia. 
    3.0.0.0 - siec. Maska 255.255.255.252 = /30

Siec Customer D:
    2 urzadzenia. 
    4.0.0.0 - siec. Maska 255.255.255.252 = /30
    
Klasa A
    podsiec 
    Podsiec 5.0.1.0 ma 2 urzadzenia  Maska 255.255.255.252 = /30
    ...
    Podsiec 5.0.15.0 ma 2 urzadzenia  Maska 255.255.255.252 = /30

```
Po tych zmianach kazdy sieciowy interfejsc (poza interfejsami switczow bo nie potrzebuja) ma swoj IP. 
#### 2. Routing z BGP 10  [_VladKoz_]❌


Dla wszystkich routerow w AS z numerem D:
```
enable
config terminal
router eigrp D
network X1
network X2...
[X1,X2 - sieci sasiedzi]
exit
[ tylko dla routerow ktore maja bezposrednie polaczenie ale sa w innych AS
router bgp [as-swoj]
neighbor [ip-sasiada] remote-as [as-sasiada]
network T1 mask MaskT1
network T2...
    T1,T2 to sa wszystkie sieci ktore naleza do innego AS oraz maski
]
[ tylko dla routerow ktore nie maja polaczenia z innym AS
 ip route A B C
 A - inna siec
 B - maska 
 C - next hop
]
exit
```
Po tych zmianach urzadzenia z sieci klasy A (AS 100) moga sie komunikowac z urzadzeniami sieci klasy C (AS 200) za pomoca BGP.


#### 3. VLAN'y 5 (minimum 4 vlany) [_Hubixo_] ❌

#### 4. Etherchannel 5 [] ❌(nie ma zaleznosci?) 

#### 5. Redystrybucja 5 (z wersja BGP 10) [] (zalezy od 2.) ❌

#### 6. NAT 10 []❌ (nie ma zaleznosci?)

#### 7. DHCP 10 [] ❌ (nie ma zaleznosci?)

#### 8. Ekstra fiber links w ISP 2 [] ❌ (nie ma zaleznosci?)
    Dla ISP dobrac siec publiczna z klasy A dla Klienta A siec publiczna z  klasy C


#### 9. ACL for WWW,SMTP 5 []❌ (zalezy od 3.)
    Strony WWW (obu klientow) maja być dostępne ze wszystkich PC  Dla Klienta B dobrać alokacje VLAN'ów.

#### 10. Mail serwer 3 [] ❌ (nie ma zaleznosci?)

### Komentarze od prowadzacego
 Dla klientów bez podanych sieci trzeba dobrać siec z puli adresów prywatnych. (co ????)
