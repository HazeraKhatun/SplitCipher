### **<p align = center>🏫HAJEE MOHAMMAD DANESH SCIENCE AND TECHNOLOGY UNIVERSITY, DINAJPUR-5200</p>**

### 📖 Course Information
**Course Title:** Mathematical Analysis for Computer Science <br>
**Course Code:** CSE 361

### 🧑‍🎓 Submitted By:
**Student ID:** 2102001 <br>
**Student Name:** Hazera Khatun <br>
**Level:** 3  
**Semester:** II <br>
**Department:** Computer Science and Engineering <br>

### 👨‍🏫 Submitted To:
**Pankaj Bhowmik** <br>
Lecturer <br>
Department of Computer Science and Engineering <br>
Hajee Mohammad Danesh Science and Technology University <br>
<hr>

# **<p align = center>Proposed Cryptographic Algorithm</p>**
## Algorithm Name: SplitCipher  
**A Cipher with 'Separate, Disorderly Join and then Hide' Technique** <br>
## Introduction
*SplitCipher* is a cryptographic algorithm that
1. Adds extra characters with the message to make its **size divisible by 'key'**.
2. Divides the message in **'Message_Size / key'** number of **blocks**.
3. Creates primary cipher-text taking characters from the blocks in **disorderly manner**.
4. Then uses **Caesar Cipher with some modifications** to get final cipher text.
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
## Example Test Case
### Encryption 
**Input:**  
k = 4  
Text = Welcome  
So, Text_size = 7  
#### 1. Make Text_size divisible by **k**
  Adding **k-(Text_size %k)** = 4-(7%4) = 1 '[' at the end of the text. <br>
  
| W | e | l | c | o | m | e | [ | 
| --- | --- | --- | --- | --- | --- | --- | --- |


here, Text_size = 8 is divisible by k = 4
#### 2. Divide Text into **(Text_size / k)** = 8/4 = 2 blocks. <br>
**Block 0:**
| W | e | l | c | 
| --- | --- | --- | --- |

**Block 1:**
| o | m | e | [ |
|--- | --- | --- | --- |

#### 3. Take one character from each block at a time consecutively until all characters are taken.  
  - For Block 0, block number is even. So, we start from leftmost character.
  - For Block 1, block number is odd. So, we start from rightmost character.

| W | [ | e | e | l | m | c | o | 
| --- | --- | --- | --- | --- | --- | --- | --- |

#### 4. Encrypt each character:

| Text | ASCII value <br> (decimal) | ASCII value + key | Cipher Text |
| ---- | ----------- | ----------------- | ----------- |
| W    | 87          | 91                | [           |
| [    | 91          | 95 > '[' <br> so, 95 - 27 = 68 | D          |
| e    | 101          | 105                | i           |
| e    | 101          | 105                | i           |
| l    | 108          | 112                | p           |
| m    | 109          | 113                | q           |
| c    | 99          | 103                | g           |
| o    | 111          | 115                | s           |

#### 5. So, Encrypted Text = [Diipqgs

### Decryption
**Input**
k = 4  
Cipher Text = [Diipqgs
#### 1. Divide Cipher_Text into **(Cipher_Text_size / k)** = 8/4 = 2 blocks.  
**Block 0:**
| [ | D | i | i | 
| --- | --- | --- | --- |

**Block 1:**
| p | q | g | s |
|--- | --- | --- | --- |

#### 2. Take characters from Cipher_Text one by one and place them block by block.  
- For even block number, start adding from left. (Block 0)
- For odd block number, start adding from right. (Block 1)  
So, the initial Decrypted text looks like this:
| [ | i | p | g | s | q | i | D | 
| --- | --- | --- | --- | --- | --- | --- | --- |

#### 3. Decrypt each character
| Text | ASCII value<br> (decimal) | ASCII value + key | Cipher Text |
| ---- | ----------- | ----------------- | ----------- |
| [    | 91          | 87                | W           |
| i    | 105          | 101              | e          |
| p    | 112          | 108                | l           |
| g    | 103          | 99                | c           |
| s    | 115          | 111                | o           |
| q    | 113          | 109                | m           |
| i    | 105          | 101                | e           |
| D    | 68          | 64 < 'A' <br> So, 64 + 27 = 91  | [           |

#### 4. Now, discard the padding character '['
#### 5. So, we get the Plain Text = Welcome

## Code
```C++
#include <bits/stdc++.h>
using namespace std;

void encrypt(string text, int k)
{
    //making input divisible by k

    int divisible = text.size() % k;
    // cout<<text.size();
    int l;
    if(divisible != 0)
    {
        for (l=0; l< k - divisible; l++)
        text += '[';
    }
    text += '\0';
    // cout<<text<<endl;

    //encryption
    int index, m=0, n=k-1;
    string encrypt = "";
    //divide the text into k blocks 
    for(int i=0; i<k; i++)
    {
        for(int j=0; j<text.size() / k; j++)
        { 
            // accessing j-th block
            index = k*j; //taking one letter at a time from each block
            if(j%2 == 0) //even numbered block: take letter from left to right
            index += m;
            else //odd numbered block: take letter from  right to left  
            index += n;

            //modified caesar cipher
            char ch = text[index];
            if(isalpha(ch) || ch == '[') //if alphabet of '['. '[' is added as padding
            {
                if(ch < 'a') //uppercase
                {
                   ch += k;
                if(ch > '[') 
                 ch -= 27;
                }
                else
                {
                   ch += k;
                   if(ch > 'z')
                    ch -= 26;  
                }
                
            }
            encrypt += ch;
            
        }
        m++;
        n--;
    }
    encrypt += '\0';
    cout<<"Encrypted message: " << encrypt;
}

void decrypt(string text, int k)
{
    int pos = 0;
    char decrypt[text.size()];
    int index, m=0, n=k-1;
    //divide the text into k blocks 
    for(int i=0; i<k; i++)
    {
        for(int j=0; j<text.size() / k; j++)
        {
            // finding appropriate position for each letter
            index = k*j; 
            if(j%2 == 0) 
            index += m;
            else 
            index += n;

            //modified caesar cipher decrypt
            char ch = text[pos++];
            // cout<<ch<<endl;
            if(isalpha(ch) || ch == '['  ) //if alphabet of '['. '[' is added as padding
            {
                if(ch < 'a') //uppercase
                {
                    ch -= k;
                    if(ch < 'A') ch += 27; //1 extra char as padding
                }
                else //lowercase
                {
                    ch -= k;
                    if(ch < 'a') ch += 26;
                }
                
               
            }
            decrypt[index] = ch;
        }
        m++;
        n--;
    }
    cout<<"Decrypted message: ";
    for(char ch: decrypt)
     {
        if(ch == '[') break; //excluding the extra characters added in encryption
        else cout<<ch;
     }

    cout<<endl;
}

int main()
{
    int choice,k;
    string text;
    
    cout<<"Enter choice: 1. Encode  2.Decode 0.Exit\n";
    cin>> choice;

    //invalid input
    if(choice!=1 && choice!=2){
        cout<<"Invalid Input\n";
        return 0;
    }

    //input text
    cout<<"Enter message: ";
    cin>> text;
    cout<<"Enter value of 'key': ";
    cin>>k;

    if(choice == 1)
    encrypt(text,k);
    else 
    decrypt(text,k);

}
```
### Sample Output-1
Enter choice: 1. Encode  2.Decode 0.Exit  
1  
Enter message: **Welcome**  
Enter value of 'key': **3**  
Encrypted message: **ZphhrCofC**  
### Sample Output-2
Enter choice: 1. Encode  2.Decode 0.Exit  
2  
Enter message: **ZphhrCofC**  
Enter value of 'key': **3**  
Decrypted message: **Welcome**  

## Update Plan
1. Use two keys.
   - Key1 to decide number of blocks to divide the message
   - Key2 to encrypt re-arranged text.
2. Relate Key1 with Key2 uniquely.
