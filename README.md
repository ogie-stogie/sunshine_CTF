# sunshine_CTF
[Write Up Link](https://github.com/tbart27/sunshine_CTF/blob/main/README.md)

### Team: 466 Crew
Taylor Bart<br>
Kamal Nadesan<br>
Matt Evans<br>
John Tiffany<br>
<br>
For this ctf, we were able to get 7 flags as a team (2 pegasus, 2 speedruns, 1 web and 2 misc)<br>
I personally contributed to the web flag and spent the rest of my time focused on a crpto challenge and speedrun #3.<br>
<br>
###web: Password Pandemonimum
To begin this CTF, I immediately tackled the web challenge for this CTF. When opening this challenge, you are greeted with an airline login where the username can be anything but the password has to meet a set of challenging criteria.<br>
<br>
Going through the challenge, here are all the criteria that I came across:<br>
- must include equal number of lowercase and uppercase<br>
  - simply count the letters
- must include prime number of numbers<br>
  - simply count the numbers
- must include emoji<br>
  - I used this [link](https://www.kirupa.com/html5/emoji.htm) to obtain this emoji 🍔. Which would be correctly interpreted in the form input.
- must include more than 2 special characters<br>
  - I included // which would be useful for later criteria below
- must be valid javascript that evaluates to true<br>
  - For this, I originally tried a statement where you try to find an equivalent string. However, as more criteria came in I realized that isNan with comments after would be more conducive for completing the challenge reasonably.<br>
- must have a md5 hash that starts with a number<br>
  - I used this [link](https://www.md5hashgenerator.com/) to test various passwords and their hashes
- must be a palindrome<br>
  - I used this [link](https://onlinetexttools.com/create-text-palindrome) to obtain a quick palindrome for the password.
- password length limited<br>
  - I don't remember the exact length, but this forced me into using isNan vs using == in the JS criteria<br>
After meeting all the criteria, I produced this string:<br>

username: isNaN('🍔DEd2')//)'2dED🍔'(NaNsi<br>

password: isNaN('🍔DEd2')//)'2dED🍔'(NaNsi<br>

I was finally given access and obtained the flag:<br>
sun{Pal1ndr0m1c_EcMaScRiPt}<br>
<br>
### Crypto: Magically Delicious
This was another emoji challenge where you are given this:<br>
![](https://github.com/tbart27/sunshine_CTF/blob/main/crypto1.PNG)<br>
I identified 7 unique emojis and believe they correspond to numbers such that if we decode the hex to ascii (or via a different decryption/decoding) I would obtain the message. 7 unique characters wasn't something I expected to see in a message though and I had trouble figuring out if maybe only a subset of decimal/hexadecimal values were being used.<br>
### Speedrun 02
By using binary ninja, I was able to see that this was very similar to overflow challenges that we had seen in our class! There was even a vuln() and win() functions!<br>
After having some trouble initially, Kamal joined and we were able to debug the local and successfully redirect control flow to the win() function! We immediately checked that the binary was 32-bit and in the execution, there is an fgets where we fed it a 19 byte buffer. With gdb.attach and some breakpoints, we then reached the next user input section where we entered cyclic(75) to determine that we needed 61 bytes in the second buffer before sending the win() address that would overwrite the return address.<br>
On the local download, we were successful with the basic gist being these commands:<br>
<br>
r.send(cyclic(19))<br>
r.send(cyclic(61)+p32(win_addr))<br>
Proof of local success can be seen in this picture of gdb:<br>
<br>
![](https://github.com/tbart27/sunshine_CTF/blob/main/speedrun1.png)<br>
<br>
However, you could easily determine that there was a difference between the lcoal and remote challenge code based solely on that the loacl needed two "enter" key presses before terminating, whereas the remote needed to receive 3! Kamal and I were unable to use gdb on the remote and were stuck until the conclusion of the CTF.<br>
<br>
### Conclusion
This was a fun CTF that used a lot of emojis and had a set of speedruns that were similar to what we have came across in some of our 466 modules. I'm curious how others debugged speedrun2 to obtain the correct buffer lengths though.
