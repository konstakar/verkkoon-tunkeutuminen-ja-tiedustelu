# x) Lue ja tiivistä

  Tiivistelmä 1. Wireshark - Getting started
- wireshark on johtava tietoverkkojen sniffaaja ja analysoija
- sillä voi kaapata liikennettä ja seurata statistiikkoja, ja suodattimien avulla seuratusta liikenteestä voi poimia esim. DNS-kyselyjä ja HTTP-verkkosurffausta
- todella hyödyllinen työkalu
  Lähde: https://terokarvinen.com/wireshark-getting-started/

 Tiivistelmä 2. Network Interface Names on Linux
- verkkorajapinta (=network interface) on melkein kuin verkkokortti, mutta se ei ole fyysinen kortti
- esim. wlp4s ja enp1s0 ovat verkkorajapintojen nimiä Linuxissa
- nimen alku identifioi rajapinnan tyypin, en=wired ethernet, wl = WLAN, lo = loopback adapter
  Lähde: https://terokarvinen.com/network-interface-linux/
  
# a) Linux
Ladattu. 

<img width="496" height="502" alt="image" src="https://github.com/user-attachments/assets/77053429-0aae-4013-b7ee-785c8446ba7f" />

# b) Ei voi kalastaa

Internet ei toimi.
<img width="1013" height="645" alt="image" src="https://github.com/user-attachments/assets/cef0fe03-b848-418d-b469-48addc604c6c" />

Internet toimii.
<img width="961" height="342" alt="image" src="https://github.com/user-attachments/assets/49b4aab6-9cc2-4171-9a7f-b98359896d83" />

# c) Wireshark

Unohdin ottaa screenshotit lataamisesta, mutta Wireshark on ladattu ja auki.

<img width="989" height="585" alt="image" src="https://github.com/user-attachments/assets/c3bed093-4515-46d8-85e0-8787e19059f6" />

Tässä liikennettä.

<img width="750" height="576" alt="image" src="https://github.com/user-attachments/assets/5268fb2b-f83b-430d-a041-ef806aa6d85a" />

# d) Oikeesti TCP/IP

<img width="923" height="353" alt="image" src="https://github.com/user-attachments/assets/31ba079c-6320-473d-8162-7f91762bf1a7" />

Kuvakaappauksen "Packet 562" on valitsemani paketti. TCP/IP-mallin neljä kerrosta ovat ethernet II (linkkikerros), internet protocol version (verkkokerros, osoittaa IP:t), User Datagram Protocol (UDP, kuljetuskerros) ja Domain Name System (DNS, sovelluskerros).

# e) Mitäs tuli surffattua?

Avasin surfing-secure.pcap:n.

<img width="997" height="731" alt="image" src="https://github.com/user-attachments/assets/81092964-bf21-4bee-9b4c-ff463ddf62c1" />

Kaappauksessa näkyy useampi kone, useampi eri "destination" joista silmään pistään terokarvinen.com tietysti ja myös se, että osa niistä on "Protected Payload"

Paketteja on 283 ja kaappaus kesti n. 7.5 sekuntia (Time: 7.534680)

# g) Minkä merkkinen verkkokortti käyttäjällä on?

Avasin heti ekan paketin ja sieltä ethernet II alta löytyy lähteen MAC-osoite.

<img width="657" height="423" alt="image" src="https://github.com/user-attachments/assets/de76033e-f198-4c22-be4a-26f87e426024" />

Verkkokortin merkki selviää MAC-osoitteen 3-ensimmäisestä tavusta (52:54:00). Yritin kattoa OUI/MAC lookup työkaluilla, mutta ei antanut vastausta joten googlasin vaan. 52:54:00 on virtuaalikone/QEMU. Merkki on "Red Hat Inc."

# h) Millä weppipalvelimella käyttäjä on surffaillut? 

En tiedä. Näen infoista google.com ja terokarvinen.com, mutta en tiedä onko kumpikaan se vastaus jota tässä haetaan.

<img width="609" height="342" alt="image" src="https://github.com/user-attachments/assets/11f062e4-cec5-412e-be41-b356b9235fd5" />

# i) Analyysi.

<img width="1072" height="603" alt="image" src="https://github.com/user-attachments/assets/e25f464d-3672-44b8-a594-d49d055f69b9" />

Alkaa sillä, että minä (kone 10.0.2.15) avaa HTTPS-yhteyden palvelimeen ja kysyy DNS:llä osoitetta gstatic.comille. Sitten minun kone aloittaa TCP yhteyden ja palvelin vastaa "server hello" ja yhteydestä tulee salattu (näkyy vain Application Data)

-------------------------------------
Tehtäviin meni n. 2,5h alusta loppuun (Debianin uudelleenlataus jne)

Lähteet:

Karvinen Tero, 2025: Wireshark - Getting Started. https://terokarvinen.com/wireshark-getting-started/

Karvinen, Tero, 2025: Network Interface Names on Linux. https://terokarvinen.com/network-interface-linux/
