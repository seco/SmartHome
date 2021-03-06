# SmartHome: Casa domotica per ESP8266 basato sul protocollo MQTT.

Il progetto si divide in nodi: nodi tapparella, nodi temperatura e nodi interruttore.  
Ogni nodo comunica attraverso il protocollo MQTT con il broker, che puo' essere locale (LAN) o remoto (internet). Per interagire con i singoli nodi bisogna mandare specifici comandi al nodo (contraddistinto da un topic MQTT univoco).  
Inviando i comandi al nodo (topic), si interagisce con esso, facendogli fare delle operazioni o interrogandolo. Il nodo risponderà sul topic "ack".  
Nella cartella "Android" è presente un'app (ancora in versione beta) dalla quale di possono gestire i vari nodi.  
A breve sarà disponibile nel Google Play, se vuoi diventare un beta tester clicca [QUI](https://play.google.com/apps/testing/roncoa.SmartHome)  

## SmartHome tapparella V 1.0

Il nodo "tapparella" serve per comandare tapparelle o serrande.  
* 2 GPIO vengono usati per comandare 2 relè (1 di abilitazione e 1 di inversione del movimento) per il movimento della tapparella.  
* 2 GPIO vengono usati come ingressi fisici da pulsanti per comandare direttamente il movimento della tapparella.  

Comandi da inviare al topic "Tapparella_Topic":

    su            -> comando SU  
    giu           -> comando GIU  
    stop          -> comando STOP  
    t=XX o T=XX   -> XX Indica per quanto tempo la tapparella può restare in azione (in sec.)  
    stato         -> restituisce sul topic ACK lo stato dei relè e per quanto tempo la tapparella può restare in azione (in sec.)  
    reset         -> pulisce la memoria EEPROM e resetta l'ESP  

## SmartHome temperatura V 1.0

Il nodo "temperatura" serve per comandare apparecchiature per il riscaldamento.  
* 1 GPIO viene usato per la sonda di temperatura e umidità (DHT22).  
* 1 GPIO viene usato per comandare il relè termostato (se impostato in AUTO, funziona come un normale termostato, se impostato in MAN, lo si può commutare a piacere).  
* 1 GPIO viene usato per comandare un relè liberamente gestibile dall'utente.  
* 2 GPIO vengono usati per interfacciare un display I2C (SSD1306).  

Comandi da inviare al topic "Temperatura_Topic":

    man           -> Imposta il termostato in "manuale"
    auto          -> Imposta il termostato in "automatico"
    t=XX o T=XX   -> Imposta il termostato alla temperatura XX
    1on           -> Imposta il relè 1 a ON
    1off          -> Imposta il relè 1 a OFF
    2on           -> Imposta il relè 2 a ON
    2off          -> Imposta il relè 2 a OFF
    stato         -> restituisce sul topic ACK lo stato dei relè la temperatura impostata e lo stato del termostato
    read          -> legge la temperatura
    reset         -> pulisce la memoria EEPROM e resetta l'ESP

## SmartHome interruttore V 1.0

Il nodo "interruttore" serve per comandare luci o prese.  
* 2 GPIO vengono usati per comandare 2 relè liberamente gestibili dall'utente.  

Comandi da inviare al topic "Interruttore_Topic":

    1on           -> Imposta il relè 1 a ON  
    1off          -> Imposta il relè 1 a OFF  
    2on           -> Imposta il relè 2 a ON  
    2off          -> Imposta il relè 2 a OFF  
    stato         -> restituisce sul topic ACK lo stato dei relè  
    reset         -> pulisce la memoria EEPROM e resetta l'ESP  
