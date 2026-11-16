# Dictionary-Attack-Lab-Unlocking-an-Encrypted-PDF-with-John-the-Ripper
“A hands on lab where I extract a crackable hash from a password protected PDF and recover the password using a dictionary attack with John the Ripper, verified both through a web based cracker and the Johnny GUI.”
# How I Cracked a Password Protected PDF in 91 Tries

## What This Lab Is About

I wanted to understand how password protected PDFs actually get broken, not just read about it. So I locked a PDF with a password, then tried to crack that password using the same method real tools like John the Ripper use. I did it two ways, once in a browser based tool so I could see every step clearly, and once locally using Johnny, which is the official GUI for John the Ripper, just to confirm the result was real and not just a simulation.

## Tools I Used

* Hash Calculator, to pull the hash out of the locked PDF
* Password Cracker, to run the actual attack
* Johnny (John the Ripper GUI), to double check the result on my own machine
* A PDF I locked myself for testing

## Step 1: Lock a PDF

I took a normal PDF and added a password to it. When I tried to open it, it asked for the password first, so the lock was working as expected.

## Step 2: Pull Out the Hash

A locked PDF does not actually store the password. It stores something called a hash, which is just a scrambled version of it used to check if the password you type in is correct. I uploaded the locked PDF to the Hash Calculator and it gave me that hash, something like this.

```
$pdf$4*4*128*-1060*1*16*55d1a5c14175da449753199e44971d32*32*777fd021a7f3c5ae598c0c6495c7f76e...
```

This is the exact same kind of hash that the real John the Ripper tool (pdf2john) would produce.

## Step 3: Crack It

Next I took that hash and put it into the Password Cracker. This tool tries one password at a time from a list, scrambles each one the same way the PDF does, and checks if it matches the hash. If it matches, the password is found.

I used a list of 100 common passwords. The tool went through them one by one, trying things like service, canada, hockey, and qwertyuiop, until it hit a match.

```
[+] MATCH password1
```

It took 91 tries out of 100. The password was password1, which is a good example of how weak a lot of real passwords still are.

## Step 4: Check It Locally

To make sure the browser tool was not just faking the result, I did the same thing on my own machine using Johnny. I loaded the same hash, ran the attack, and it cracked the password with a 100 percent success rate. Same answer, different tool, which told me the method actually works and is not just a trick.

## Step 5: Open the PDF

Last step was easy. I typed the cracked password into the locked PDF and it opened right away.

## Lessons Learned

* A password protected file does not store your actual password, it stores a hash of it
* A dictionary attack just means trying known or common passwords one by one until one matches
* How to pull a crackable hash out of a PDF
* Hands on use of John the Ripper through Johnny, not just reading about it
* Why simple passwords like password1 get cracked almost instantly

## Limitations

* The password was cracked using a small list of only 100 common passwords, so this only works if the real password happens to be on that list
* A longer or more random password, even something like a short random string, would not have been cracked this way and would need a much bigger wordlist or a brute force attack instead, which takes far more time
* This test used a PDF I locked myself, so I knew roughly what kind of password to expect. A real world file with an unknown password would be much harder to predict
* The speed shown here, about 9 passwords per second, is slow compared to what dedicated cracking hardware or GPU based tools can do, so results in a real attack could be faster or need a different approach entirely
* This lab focused on PDF encryption specifically. Other file types and systems use different hashing methods, so the exact steps here would not carry over without changes

## Why It Matters

A password on a file only protects it if the password itself is strong. This lab showed how fast a weak password can be broken, even with a small list of only 100 guesses. It's a good reminder that the lock is only as good as what you use to lock it.
