# hostap：radius server #
radius server used hostapd cloned from hostap

* prepare hostapd compiled for radius server

      ./hostapd -ddd -t -K hostapd_win.conf

* config wpa_supplicant

 ![eap-tls](https://github.com/bigfeng12/hostap-radius/blob/master/pcshow/eap-tls.png)
 
 ![eap-wfa-unauth](https://github.com/bigfeng12/hostap-radius/blob/master/pcshow/wfa-unauth-hs20-osen.png)
# wlantest: tool used to data frame decrytion #

* CCMP/TKIP

      ○ wlantest -T PTK.txt -r encrypted.pcap -w decrypted.pcap
      
      ○ wlantest -dd -T PTK.txt -r encrypted.pcap -w decrypted.pcap
      
      ○ wlantest -f PSK.txt -r encrypted.pcap -w decrypted.pcap
      
* WEP

      ○ wlantest -W 3132333435 -r encrypted.pcap -w decrypted.pcap
