1. Opening an app and resolving its address:

When you tap an installed app such as Jio Hotstar, the operating system starts its process and
brings the required code and data into memory. The app checks connectivity and may display
cached content while it waits for the network. To fetch a home feed, the client prepares an API
request to the service hostname  

App ka poora code aur saara data (images, videos, saari screens) storage (phone ki memory/disk) mein installed rehta hai. Jab tum app tap karte ho, OS sirf zaroori hissa RAM mein laata hai:
App ka main code (jo abhi chalna hai)
Pehli screen ka UI
Thoda sa data jo abhi chahiye
Baaki cheezein tab load hoti hain jab zaroorat padti hai (lazy loading). Jaise tum Settings screen kholo, tabhi uska code/data RAM mein aayega.


app tap kiya → OS ne app start kiya → app ko server ka IP chahiye → DNS ne diya.

Tum browser mein hotstar.com type karte ho:
Browser poochta hai: “hotstar.com ka IP kya hai?”
DNS jawab deta hai: “IP hai x.x.x.x”
Browser us IP pe jaake website maangta hai

DNS Lookup kaise hoga :  
Chalo hotstar.com ka example lekar step-by-step dekhte hain ki IP address kaise milta hai.

Steps

Step 1: Browser cache check
Browser pehle apni memory dekhta hai: “kya maine hotstar.com ka IP pehle se save kiya hai?” Mil gaya toh kaam khatam.

Step 2: OS cache aur hosts file check
Browser mein nahi mila, toh operating system apna DNS cache aur hosts file dekhta hai. Mil gaya toh yahin se answer.

Step 3: Recursive resolver ko request
Kahin nahi mila, toh request Recursive Resolver ko jaati hai (usually tumhare ISP ka, ya Google ka 8.8.8.8). Resolver apna cache dekhta hai. Mil gaya toh answer wapas.

Step 4: Root server se poochna
Resolver ke paas bhi nahi hai, toh woh Root server se poochta hai: “hotstar.com ka IP kya hai?”
Root bolta hai: “Mujhe IP nahi pata, par .com ka TLD server yeh hai, wahan jao.”

Step 5: TLD server se poochna
Resolver .com TLD server se poochta hai.
TLD bolta hai: “IP nahi pata, par hotstar.com ka Authoritative server yeh hai, wahan jao.”

Step 6: Authoritative server se poochna
Resolver Authoritative server se poochta hai.
Yeh bolta hai: “Haan, hotstar.com ka IP x.x.x.x hai.”




1. Shuruaat: app tap karna

Tum Jio Hotstar jaisi app tap karte ho. OS app ka process start karta hai aur sirf zaroori code aur data RAM mein laata hai (poora app nahi). Baaki cheezein tab load hoti hain jab zaroorat padti hai (lazy loading).

Analogy: badi library (storage) se sirf 2-3 kitabein desk (RAM) pe aati hain.

2. App network pe kya karti hai

App start hote hi:

Connectivity check karti hai (internet hai ya nahi)
Agar network slow ya nahi hai toh cached content dikha sakti hai (purana saved home feed)
Fresh home feed ke liye API request ki taiyari karti hai, service ke hostname ko target karke (jaise api.hotstar.com)
3. Problem: hostname se kaam nahi chalega

Network sirf IP address samajhta hai, naam nahi.

IPv4: 32 bit
IPv6: 128 bit

Isliye hostname ko IP mein convert karna padta hai. Yeh DNS karta hai, aur yeh HTTP request se pehle hota hai.

Jo IP milta hai woh aksar edge service ya load balancer ka hota hai, seedha application server ka nahi.

4. DNS lookup: steps
Cache check: browser/app cache, phir OS cache (aur hosts file). Mil gaya toh lookup khatam.
Recursive resolver ko request: ISP ka (Jio, Airtel) ya public resolver (Google 8.8.8.8, Cloudflare 1.1.1.1). Resolver apna cache dekhta hai.
Root server: IP nahi deta, sirf bolta hai “.com TLD server yeh hai” (referral).
TLD server: IP nahi deta, bolta hai “domain ka Authoritative server yeh hai” (referral).
Authoritative server: final IP deta hai.
Caching: resolver IP ko TTL tak cache karta hai aur client ko bhejta hai. OS aur browser bhi cache kar lete hain.

5. IP milne ke baad

Client TLS connection banata hai (HTTPS ke liye) aur phir API request bhejta hai:



CDN : Content Delivery Network 
CDN = duniya bhar mein phaile edge servers ka network, jo content ki copies user ke paas rakhte hain, taaki fast delivery ho aur origin pe load kam pade.
Origin server = Hotstar ka asli server (data center ke andar)

Load Balancer : origin se edge servers pe (not by LB1 ye toh direct dns hi bta dega)
phir har locn pe : api gatway for diff services and for particular service LB2 ki konse server ko load dena this is also done by algos

**DNS se edge server ya LB1 ka address milta hai**


