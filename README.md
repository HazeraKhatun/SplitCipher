### **<p align = center>🏫HAJEE MOHAMMAD DANESH SCIENCE AND TECHNOLOGY UNIVERSITY, DINAJPUR-5200</p>**

### 📖 Course Information
**Course Title:** Mathematical Analysis for Computer Science <br>
**Course Code:** CSE 361

### 🧑‍🎓 Submitted By:
**Student ID:** 2102001 <br>
**Student Name:** Hazera Khatun <br>
**Level:** 3  **Semester:** I <br>
**Department:** Computer Science and Engineering <br>

### 👨‍🏫 Submitted To:
**Pankaj Bhowmik** <br>
Lecturer <br>
Department of Computer Science and Engineering <br>
Hajee Mohammad Danesh Science and Technology University <br>
<hr>

# **<p align = center>Proposed Cryptographic Algorithm</p>**
## Algorithm Name: SplitCipher: 
**A Cipher with 'Separate, Disorderly Join and then Hide' Technique** <br>
## Introduction
*SplitCipher* is a cryptographic algorithm that
1. Adds extra characters with the message to make its size divisible by 'key'.
2. Divides the message in 'message_size / key' number of blocks.
3. Creates primary cipher-text taking characters from the blocks in disorderly manner.
4. Then uses caesar cipher with some modifications to get final cipher text.
5. Decryption is done reversely from encryption by re-organizing the characters.
## Encryption Algorithm
1. Get input TEXT and KEY.
2. To make the size of the TEXT divisible by KEY, <br>
add **(KEY - (TEXT_SIZE % KEY))** number of **'['** character at the end of the messaage.
3.  Repeat for **i = 0 to KEY - 1**  
    - Repeat for each block: **j = 0 to TEXT_SIZE / KEY - 1**
    - Take one character, CH, from each block at a time
      - For even numbered block: start from leftmost character.
      - For odd numbered block: start from rightmost character.
    - Apply Caesar Cipher with some modification.
      - If character is **alphabet** or '**[**'
        - If character is **uppercase** (CH < 'a')
          - Add KEY. If result exceeds '[', subtract 27. (one extra character for padding)
        - Else (character is **lowercase**)
          - Add KEY. If result exceeds 'z', subtract 26.
     - Add the character to ENCRYPTED message.
4. Print the **ENCRYPTED** message.
## Decryption Algorithm
1. Get ENCRYPTED message and KEY.
2. Create a string DECRYPTED with same size as ENCRYPTED.
3. Set m = 0 and n = KEY - 1.
4.  Repeat for **i = 0 to KEY - 1**  
    - Repeat for each block: **j = 0 to TEXT_SIZE / KEY - 1**
    - For each character, find its appropriate position in the original message.
      - Set INDEX = KEY * j.
      - For even numbered block (j%2==0)
        - INDEX = INDEX + m.
        - m = m + 1.
      - For odd numbered block
        - INDEX = INDEX + n.
        - m = n - 1.
    - Apply Caesar Cipher with some modification.
      - If character is **alphabet** or '**[**'
        - If character is **uppercase** (CH < 'a')
          - Subtract KEY. If result precedes 'A', add 27.
        - Else (character is **lowercase**)
          - Subtract KEY. If result precedes 'a', add 26.
     - Place the character to the INDEX position in DECRYPTED message.
5. Print the **DECRYPTED** message.
## Flow charts
## Example Test Case
## Code

