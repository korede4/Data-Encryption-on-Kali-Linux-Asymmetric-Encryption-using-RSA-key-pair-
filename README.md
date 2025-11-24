# Data-Encryption-on-Kali-Linux-Asymmetric-Encryption-using-RSA-key-pair
## Hands on Encryption and Decryption on Kali Linux using open SSL to explore data confidentiality and cryptography 

Lets make a proper defination and comprehension on Asymmetric Encryption.
Asymmetric Encryption (also called public key cryptography) is a method of encryption that uses two seperate keys:
* Public key-used to encrypt data, it can be shared freely with anyone
* Private key-used to decrypt data it must be kept secret
    The key principle is that anything encrypted with the public key can only be decrypted with the corresponding private key and vice versa

  ## Starting by creating a file, creating a text file that would serve as the message to protect
  <img width="383" height="25" alt="image" src="https://github.com/user-attachments/assets/90568aa4-922a-4c2e-91d3-be1ba63fd3c2" />
  
  quick explanation of the code:
  
  *The echo command prints text to the standard output(usually the terminal)
  
  *"This is a secret message" is the text that will be printed.
  
  * > This is the output redirection operator
    
     it takes the ouput of the command on the left (echo) and writes it to the file on the right (secret.txt)
    
     if the file secret.txt does not exist, it will be created
    
     if the file already exists, it content will be overwritten
    
  * secret.txt
    This is the name of the file where the message will be saved 

   This created a file called secret.txt, it looked harmless just a short message. But the goal is to make the text unreadable.

  ## Generating RSA key pair Next, generate a 2048-bit RSA private key. This key would later help to decrypt the data
  <img width="1334" height="151" alt="image" src="https://github.com/user-attachments/assets/a0233a50-ac0c-4033-8a73-b077c5b00a31" />
  
  quick explanation of the code:
  
  * Openssl genpkey- Genetrates a new private key
    
  * -algorithm RSA - Specifies the key type as RSA
    
  * -out private_key.pem- Saves the generated private key to a file named private_key.pem.
   
  * -aes256 - Encrypts the private key with AES-256 using a passphrase for extra security.
    
  after running this code, openSSL asked to set a passphrase for extra security.This is to realize how important it is to keep the private key safe.

   ## Extracting the public key with the private key created, the public is needed to encrypt the files
  <img width="530" height="51" alt="image" src="https://github.com/user-attachments/assets/38e39872-cc0a-4866-9812-cc2138eab61d" />
  
  quick explanation of the code:
  
  * openssl rsa → Manages RSA keys
    
  * -in private_key.pem → Reads the existing private key file
    
  *-pubout → Extracts the corresponding public key
  
  *-out public_key.pem → Saves the public key to a file named public_key.pem.
    
    Now the two keys is in hand , *private_key.pem; used to decrypt *public_key.pem; used to encrypt data , this clearly shows the idea of (asymmetric) one key locks, the other unlocks.

    ## Encrypting a file with a public key , using the public key to encrypt the file that was created earlier
    <img width="796" height="36" alt="image" src="https://github.com/user-attachments/assets/7a0ce315-ff67-4861-a7d8-414615985154" />
    <img width="1332" height="87" alt="image" src="https://github.com/user-attachments/assets/3bc7591d-5c93-4d28-94a0-4bfe10fd0d3b" />
    
  quick explanation of the code:
  
   * openssl pkeyutl → Utility for public/private key operations.
     
   * -encrypt → Encrypts the input data
     
  *-pubin → Specifies that the input key is a public key
  
  *-inkey public_key.pem → Uses public_key.pem to encrypt
  
  *-in secret.txt → The file containing the message to encrypt
  
  *-out secret.enc → Saves the encrypted output to secret.enc.

after ruuning it, secret.txt transformed into a new file called secret.enc, openining it , it was just a bunch of random symbols, completely unreachable 

## Decrypting the files with the private key to get the original text back, it used the private key to decrypt it 
<img width="689" height="33" alt="image" src="https://github.com/user-attachments/assets/78bc7b28-027a-4d37-9859-5066e445da2a" />
<img width="246" height="39" alt="image" src="https://github.com/user-attachments/assets/77e31685-196d-452f-b2df-23ac36f0a13d" />

 quick explanation of the code:
 
* -decrypt → Decrypts the data
  
*-inkey private_key.pem → Uses the private key to decrypt

*-in secret.enc → The encrypted file

*-out decrypt.txt → Saves the decrypted message.
  
 Opening decrypt.txt revealed the original text "This is a secret message"

 # Securing my private key finally, to make protect the private key from unauthorised access 
 <img width="324" height="28" alt="image" src="https://github.com/user-attachments/assets/9e29d5ea-2628-485c-b103-849e0582eb4e" />
 
 quick explanation : 
 
 *chmod 600 → Sets file permissions so only the owner can read and write.
 
 *private_key.pem → The file being protected.

Doing this restricts access so that only the authorised access can read nor write the file. it is simple but crucial step in maintaining key security. 

## Reflection this helped me to understand how RSA encryption works, the concept of having two keys one to lock and another to unlock, it is fascinating to think that the same process forms the backbone of secure system we use everyday, like HTTPS, SSH and DIGITAL CERTIFICATES.
 






  

