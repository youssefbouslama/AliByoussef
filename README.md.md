# TP: Cryptosystème de Vignère
- Youssef Bouslama WM
## Table of content
- Definition
- Objectif
- Chiffrement de Vigenère
- Déchiffrement de Vigenère
- Attaque par force brute
- Conclusion
## Definition
Le chiffrement de Vigenère est un cryptosystème symétrique, ce qui signifie qu'il utilise la même clé pour le chiffrement et le déchiffrement.
## Objectif 
  Le but de ce TP est de programmer les fonctions de chiffrement et déchiffrement du cryptosystème de Vigenère puis d’effectuer une attaque à force brute sur un texte chiffré.
## Chiffrement de Vigenère
Ecrire un programme qui permet de chiffrer un texte par le cryptosystème de Vigenère en utilisant un mot-clé.
```cpp
#include<iostream>
#include<string>
#include<cstring>
#include<algorithm>
#include<bits/stdc++.h>
using namespace std;

int getposition(const char *array, int size, char c)
{
    for (size_t i = 0; i < size; i++)
    {
        if (array[i] == c)
            return (int)i;
    }
    
}
int main() {
   string msg ;
   string key;
   cout << "msg :" << endl;
   getline(cin,msg);
   cout << "key :" << endl;
   getline(cin,key);
   msg.erase(std::remove (msg.begin(), msg.end(), ' '), msg.end());
   transform(msg.begin(), msg.end(), msg.begin(), ::toupper);
   transform(key.begin(), key.end(), key.begin(), ::toupper);

    char alphabet[26]={'A','B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R','S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z'};
    char msg_array[msg.length()];
    char key_array[key.length()];
    strcpy(msg_array, msg.c_str());
    strcpy(key_array, key.c_str());
    int outm_array[msg.length()];
    int outk_array[key.length()];
    for(int i=0;i<msg.length();i++)
        outm_array[i]=getposition(alphabet,26,msg_array[i]);
    for(int i=0;i<key.length();i++)
        outk_array[i]=getposition(alphabet,26,key_array[i]);
    int out_array[msg.length()];
    for(int i=0;i<msg.length();i++)
    	out_array[i]=((outm_array[i]+outk_array[(i+1)%key.length()])+26)%26;
	
        
   
	string o_array;
    for(int i=0;i<msg.length();i++)
        o_array+=alphabet[out_array[i]];
    
   cout << msg<<endl;
   cout << o_array;
  return 0;
}
```
## Déchiffrement de Vigenère
Ecrire une fonction Dechiffrer(Ciphertext , Keyword) qui prend en paramètre deux chaines de caractères Ciphertext et Keyword et qui renvoie le texte clair Plaintext.
```cpp
#include<iostream>
#include<string>
#include<cstring>
#include<algorithm>
#include<bits/stdc++.h>
using namespace std;

int getposition(const char *array, int size, char c)
{
    for (size_t i = 0; i < size; i++)
    {
        if (array[i] == c)
            return (int)i;
    }
    
}
int main() {
   string msg ;
   string key;
   cout << "msg a dechiffrer :" << endl;
   getline(cin,msg);
   cout << "key :" << endl;
   getline(cin,key);
   msg.erase(std::remove (msg.begin(), msg.end(), ' '), msg.end());
   transform(msg.begin(), msg.end(), msg.begin(), ::toupper);
   transform(key.begin(), key.end(), key.begin(), ::toupper);

    char alphabet[26]={'A','B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R','S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z'};
    char msg_array[msg.length()];
    char key_array[key.length()];
    strcpy(msg_array, msg.c_str());
    strcpy(key_array, key.c_str());
    int outm_array[msg.length()];
    int outk_array[key.length()];
    for(int i=0;i<msg.length();i++)
        outm_array[i]=getposition(alphabet,26,msg_array[i]);
    for(int i=0;i<key.length();i++)
        outk_array[i]=getposition(alphabet,26,key_array[i]);
    int out_array[msg.length()];
    for(int i=0;i<msg.length();i++)
    	out_array[i]=((outm_array[i]-outk_array[(i+1)%key.length()])+26)%26;
	
        
   
	string o_array;
    for(int i=0;i<msg.length();i++)
        o_array+=alphabet[out_array[i]];
    
   cout << msg<<endl;
   cout << o_array;
  return 0;
}
```
## Conclusion
Le chiffrement de Vigenère ressemble beaucoup au chiffrement de cezar, à la différence près qu'il utilise une clef plus longue afin de pallier le principal problème du chiffrement de César: le fait qu'une lettre puisse être codée d'une seule façon. Pour cela on utilise un mot clef au lieu d'un simple caractère.

 
