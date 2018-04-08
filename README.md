# hostap：radius server #
radius server used hostapd cloned from hostap

* prepare hostapd compiled for radius server

      ./hostapd -ddd -t -K hostapd_win.conf

* certificate retrieve (self-signed)


       1.1   private key       
       openssl genrsa -out ca/ca-key.pem 1024       
       1.2   certificate request       
       openssl req -new -out ca/ca-req.csr -key ca/ca-key.pem       
       1.3   sign certificate       
       openssl x509 -req -in ca/ca-req.csr -out ca/ca-cert.pem -signkey ca/ca-key.pem -days 3650

       2.1   private key
       openssl genrsa -out server/server-key.pem 1024
       2.2   certificate request
       openssl req -new -out server/server-req.csr -key server/server-key.pem
       2.3   sign with CA Root Certificate
       openssl x509 -req -in server/server-req.csr -out server/server-cert.pem -signkey server/server-key.pem -CA ca/ca-cert.pem -CAkey ca/ca-key.pem -CAcreateserial -days 3650
  
       3.1   private key
        openssl genrsa -out client/client-key.pem 1024
       3.2   certificate request
        openssl req -new -out client/client-req.csr -key client/client-key.pem
       3.3 sign with CA Root Certificate
        openssl x509 -req -in client/client-req.csr -out client/client-cert.pem -signkey client/client-key.pem -CA ca/ca-cert.pem -CAkey ca/ca-key.pem -CAcreateserial -days 3650
 
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
