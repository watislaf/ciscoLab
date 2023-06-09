# ciscoLab ![](https://geps.dev/progress/100) (70/70)

Osoby:

- Hubixo
- Remigiusz
- VladKoz
- wojexe

## Opis

Zadanie powinno byc zrobione w pakiet tracerze, plik znajduje sie w folderze.

![img.png](img.png)

## Rozwiazania

#### 1. Adresacja sieci IPv4 z najmniejszej liczby adresow IP 10 [VladKoz] ✅

Adresacja sieci z najmniejsza liczba adresow:
przerabiamy algorytm z cwiczen, czyli bierzemy ilosc urzadzen+2 po czym liczymy minimalna potege dwojki i z tego dostajemy maske.

```bash
Siec Customer A:
    Podsiec 1.0.1.0 ma 2 urzadzenia  Maska 255.255.255.252 = /30
    Podsiec 1.0.2.0 ma 30 urzadzen  Maska 255.255.255.224 = /27
    Podsiec 1.0.3.0 ma 2 urzadzenia  Maska 255.255.255.252 = /30
    Podsiec 1.0.4.0 ma 2 urzadzenia  Maska 255.255.255.252 = /30
    Podsiec 1.0.5.0 ma 2 urzadzenia  Maska 255.255.255.252 = /30
    Podsiec 1.0.6.0 ma 2 urzadzenia  Maska 255.255.255.252 = /30

Siec Customer C:
    32 urzadzenia.
    10.0.0.0 - siec. Maska 255.255.255.192 = /26

Siec Customer D:
    510 urzadzenia.
    10.0.0.0 - siec. Maska 255.255.254.0 = /23

Klasa A
    podsiec
    Podsiec 5.0.1.0 ma 2 urzadzenia  Maska 255.255.255.252 = /30
    ...
    Podsiec 5.0.17.0 ma 2 urzadzenia  Maska 255.255.255.252 = /30

```

Po tych zmianach kazdy sieciowy interfejsc (poza interfejsami switczow bo nie potrzebuja) ma swoj IP.

#### 2. Routing z BGP 10 [_VladKoz_]✅

Dla wszystkich routerow w AS z numerem D:

```bash
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

#### 3. VLAN'y 5 (4 vlany) [_VladKoz_] ✅

Wszystkie vlany sa wypisane dla kazdego switcha. Kazdy ip interface znajduje sie w jednym vlanie.
Po tych zmianach vlan X nie jest dostepny z Vlan Y.
Zmienic router: dodac wszystkie i ip addresy do routera w tych vlanach, tez podmienic default gateway
dla wszystkich urzadzen na ip routera w tym vlanie.

#### 4. Etherchannel 5 [_Hubixo_] ✅

Teraz 2 switchy sa ktore polaczone 2 przewodami. Tez wziety pod uwage vlan.

#### 5. Redystrybucja z wersja BGP 10 [_VladKoz_] ✅

Redystrybucja pozwala na wymiane routami pomiedzy roznymi sieciowymi protokolami. Po polaczeniu EIGRP i BGP kazde urzadzenie w sieci
eigrp ma dostep do sciezek z innego BGP.

#### 6. NAT 10 [_Hubixo_] ✅

Nat laczy 3 privatne sieci pomiedzy soba.

#### 7. DHCP 10 [_wojexe_] ✅

Dodane zostało automatyczne przydzielanie adresów IP dla komputerów w sieci Customer B.
Jeśli na urządzeniu zostanie wybrana opcja **DHCP** w sekcji _Desktop / IP Configuration_, DHCP serwer (u nas Router2_1) nada jeden z dostępnych adresów IP requestującemu urządzeniu.

#### 8. Ekstra fiber links w ISP 2 [_Remigiusz_] ✅

```
Dodane fiber linki w ISP
```

#### 9. ACL for WWW,SMTP 5 [_Remigiusz_]✅

```
Strony WWW (obu klientow) dostępne ze wszystkich PC, acl odrzuca pakiety inne niz www, smtp do serwera klienta A
```

#### 10. Mail serwer 3 [_VladKoz_] ✅

Teraz da sie wysylac maili za pomoca Server2_10 z komputera PC2_4 na PC2_4 na przyklad.

### Komentarze od prowadzacego

Dla klientów bez podanych sieci trzeba dobrać siec z puli adresów prywatnych. (co ????)
