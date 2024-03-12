# Forensics Category:

### > Colored Squares challenge :

In this challenge, we received a PCAP file.
Upon analyzing it, we found what appears to be an obfuscated PowerShell script, and indeed it is.

![](https://media.discordapp.net/attachments/1067452256686981161/1216987290522615828/Screen_Shot_2024-03-12_at_5.52.47_AM.png?ex=660262bc&is=65efedbc&hm=178c3bb53583251160c354b60184f9c655d4120b8cd780ab9a125cbfa1ad0bd0&=&format=webp&quality=lossless&width=2588&height=1390)

Haha, it seems the script is indeed a fake Discord Nitro generator. (LOL)

![](https://cdn.discordapp.com/attachments/1067452256686981161/1216988581785243768/Screen_Shot_2024-03-12_at_5.57.58_AM.png?ex=660263f0&is=65efeef0&hm=208b065190814959e9bee46c8a7ad5859905a68b8d232eb1ed5a5a4c5e17400b&)

We have reversed and base64-encoded content, so I deobfuscated it using CyberChef.

![](https://cdn.discordapp.com/attachments/1067452256686981161/1216991046588694558/Screen_Shot_2024-03-12_at_6.06.36_AM.png?ex=6602663c&is=65eff13c&hm=f7d751bf125983aa3f978aab35bc217fd343c0796d1d013aa7bbc4113abd8c79&)

Analyzing the code, there is a variable named part1:

`$part1 = "SFRCe2ZyMzNfTjE3cjBHM25fM3hwMDUzZCFf"`

Decoding it from base64, we got the first part of the flag: HTB{fr33_N17r0G3n_3xp053d!_

Then, we have a function that encrypts a string with AES encryption, and we have the key.

`$AES_KEY = "Y1dwaHJOVGs5d2dXWjkzdDE5amF5cW5sYUR1SWVGS2k="`

So, in the PCAP file, in the last stream, we have an encrypted text, so it's the one that was encrypted.

![](https://cdn.discordapp.com/attachments/1067452256686981161/1216995646272307290/Screen_Shot_2024-03-12_at_6.26.00_AM.png?ex=66026a84&is=65eff584&hm=71db743d36dbd80688b4cbdf378ee36695b78fd0e95c45b525f2088d086e60d2&)


Decoding it with the key (which must be decoded from base64).

![](https://cdn.discordapp.com/attachments/1067452256686981161/1216996486710169700/Screen_Shot_2024-03-12_at_6.29.23_AM.png?ex=66026b4d&is=65eff64d&hm=1549568030c32c51b3344485aa5294f1dc4a745cb696d558ddc6a98aba9cf255&)

We received a Base64-encoded string which, when decoded, provided us with JSON data. 

![](https://cdn.discordapp.com/attachments/1067452256686981161/1216996918878801920/Screen_Shot_2024-03-12_at_6.30.46_AM.png?ex=66026bb4&is=65eff6b4&hm=56f3a879528e635e0af93490514bf0b28f84cb1dfb9f5a456763eb025fb5e06d&)

Decoding the email field from this JSON data using Base64 yielded the last part of the flag.

![](https://cdn.discordapp.com/attachments/1067452256686981161/1216997788395634698/Screen_Shot_2024-03-12_at_6.34.32_AM.png?ex=66026c83&is=65eff783&hm=d973855b3537d24c0160a46b308ee71470b9e9fba0dc8b0cd3b4f51ae32b2f6d&)

FLAG : 
> HTB{fr33_N17r0G3n_3xp053d!_b3W4r3_0f_T00_g00d_2_b3_7ru3_0ff3r5}
