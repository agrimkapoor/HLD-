Web infrastructure = Load Balancing (traffic baantna) + CDN (content paas se) + Proxies (middleman) + TLS (secure connection) + Caching (fast reads), jo milke website ko fast, scalable aur secure banate hain.

Web infrastructure = woh saari hardware, software aur network ki cheezein jo ek website/app ko internet pe chalane aur users tak pahunchane ke liye chahiye hoti hain.


1.Load Balancer

Load balancer (LB) ek aisa server/software hai jo aane wali requests ko multiple servers mein baant deta hai, taaki koi ek server overload na ho.

kaise decide karta hai = koi algorithm -- 
(i) Round Robin
(ii) Normal Hashing
(iii) Consistent Hashing 


Edge server (Delhi PoP)
      ↓
LB1  (origin ka entry point)
      ↓
Gateway Instance 1 / 2 / 3 / 4  (koi ek)
      ↓
LB2 → Service server
