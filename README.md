# sunshine_CTF
[Write Up Link](https://github.com/tbart27/sunshine_CTF/blob/main/README.md)

Team: 466 Crew
Taylor Bart
Haytham Mouti
Matt Evans
John Tiffany
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
