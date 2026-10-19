**TLS** 

HTTPS = HTTP + TLS   
TLS = transport layer security  

Problem:
Tum hotstar.com kholte ho. Do darr hain:    
1.Beech mein koi tumhara data padh na le (privacy)     
2.Tum fake Hotstar se baat na kar rahe ho (pehchaan)    

Client --- Server   

Client ki apni public and private key hoti  
Server ki apni public and private key hoti  

Server (hotstar) ke paas apna certificate jisme likha ki :  
1.ye hotstar.com hai  
2.aur ye hotstar ki public key hai   

this certificate is signed by trusted CA (certificate authority)  
Browser mein pehle se trusted CAs ki list hoti hai.   

certificate data  se hash calculate kardo : 

Hash ki 2 khaas baatein:  
Data mein ek letter bhi badla toh fingerprint poora alag aayega  
Fingerprint se wapas original data nahi nikal sakte   

CA apni private key se sign karta hai  
Fingerprint (a8f3c9...)  +  CA ki PRIVATE key  →  Signature (x7k2p...)  
Ab certificate ke saath yeh signature chipka diya jaata hai.  
ham encrypt nhi kar rhe  

Browser verify karta hai  

Browser ke paas certificate aaya. Woh do cheezein nikalta hai aur compare karta hai:  

Raasta A: Certificate data ka hash khud nikalo          →  a8f3c9...  
Raasta B: Signature ko CA ki PUBLIC key se kholo         →  a8f3c9...  

A == B  →  ✓ Asli aur badla nahi gaya  
A != B  →  ✗ Reject   

Agar hacker certificate mein kuch badle (jaise apni public key daale), toh hash badal jaayega, aur purani signature se match nahi hoga. Pakda jaayega.
