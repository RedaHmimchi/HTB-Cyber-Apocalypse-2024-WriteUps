# Forensics Category:

### > Colored Squares challenge :

In this challenge, we received a PCAP file.
Upon analyzing it, we found what appears to be an obfuscated PowerShell script, and indeed it is.

![](https://cdn.discordapp.xyz/attachments/1067452256686981161/1216987290522615828/Screen_Shot_2024-03-12_at_5.52.47_AM.png)

Haha, it seems the script is indeed a fake Discord Nitro generator. (LOL)

![](https://cdn.discordapp.xyz/attachments/1067452256686981161/1216988581785243768/Screen_Shot_2024-03-12_at_5.57.58_AM.png)

We have reversed and base64-encoded content, so I deobfuscated it using CyberChef.

![](https://cdn.discordapp.xyz/attachments/1067452256686981161/1216991046588694558/Screen_Shot_2024-03-12_at_6.06.36_AM.png)

Analyzing the code, there is a variable named part1:

`$part1 = "SFRCe2ZyMzNfTjE3cjBHM25fM3hwMDUzZCFf"`

Decoding it from base64, we got the first part of the flag: HTB{fr33_N17r0G3n_3xp053d!_

Then, we have a function that encrypts a string with AES encryption, and we have the key.

`$AES_KEY = "Y1dwaHJOVGs5d2dXWjkzdDE5amF5cW5sYUR1SWVGS2k="`

So, in the PCAP file, in the last stream, we have an encrypted text, so it's the one that was encrypted.

![](https://cdn.discordapp.xyz/attachments/1067452256686981161/1216995646272307290/Screen_Shot_2024-03-12_at_6.26.00_AM.png)


Decoding it with the key (which must be decoded from base64).

![](https://cdn.discordapp.xyz/attachments/1067452256686981161/1216996486710169700/Screen_Shot_2024-03-12_at_6.29.23_AM.png)

We received a Base64-encoded string which, when decoded, provided us with JSON data. 

![](https://cdn.discordapp.xyz/attachments/1067452256686981161/1216996918878801920/Screen_Shot_2024-03-12_at_6.30.46_AM.png)

Decoding the email field from this JSON data using Base64 yielded the last part of the flag.

![](https://cdn.discordapp.xyz/attachments/1067452256686981161/1216997788395634698/Screen_Shot_2024-03-12_at_6.34.32_AM.png)

FLAG : 
> HTB{fr33_N17r0G3n_3xp053d!_b3W4r3_0f_T00_g00d_2_b3_7ru3_0ff3r5}
