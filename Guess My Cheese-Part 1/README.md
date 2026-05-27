Try to decrypt the secret cheese password to prove you’re not the imposter!

Additional details will be available after launching your challenge instance.

This challenge comes under the Cryptography category.

<img width="922" height="792" alt="1_UBMxT_JdW-pQx68ROARfuQ" src="https://github.com/user-attachments/assets/0ed364a4-f7e0-493a-bb02-203ce2377396" />

At first login to the netcat of the picoCTF and this will be interface.

<img width="1100" height="262" alt="1_iDh5nZGIaNQm1zpUgQeA5A" src="https://github.com/user-attachments/assets/4c98a7e0-5826-4ef1-8631-94626575e3b0" />

At first i read the description in the terminal for longer time to understand what the challenge is about, but nothing was understood at first. It has two options,

(g)uess
(e)ncrypt
At first thought that i would give use the encrypt option and give some random wordings to find the encryption logic. But it didn’t work…

<img width="1100" height="178" alt="1_Ydw7--drYibo0N67lwZcpQ" src="https://github.com/user-attachments/assets/c3f99525-d38d-4099-ae45-c33c708cbfff" />

I tried all the possibilities but nothing worked, then tried all the words and then by reading the description once again, i got strike to use the Cheese names, then googled the popular cheese names and tried to encrypt and it worked, it gave the encrypted ciphertext.

We have only 3 chance for to find the encryption logic, so i tried the popular 2 cheese,

CHEDDAR → QVSRROF
MOZZARELLA → ACNNOFSZZO
The cheese’s CHEDDAR, MOZZARELLA got converted to the following the ciphertext QVSRROF, ACNNOFSZZO.

<img width="1100" height="190" alt="1_XUtOYPIKpPqK9DCObdksZA" src="https://github.com/user-attachments/assets/eb682fa6-a45f-45e4-b938-cdbbfb42a3e9" />

<img width="1100" height="156" alt="1_yweANK8kzgq4wfr9GcKXFQ" src="https://github.com/user-attachments/assets/1bae63da-78fb-49ab-a066-20cfdfc3e225" />

Then by using the chatgpt asked the key logic and it got worked and cracked the challenge.

<img width="1100" height="559" alt="1_M9YawNLDslkRgBN_DGplOw" src="https://github.com/user-attachments/assets/110e4fbf-f281-4a40-884e-ff4feab19025" />

<img width="1100" height="731" alt="1_KIvN5c-clpsTMGlOmbKf0g" src="https://github.com/user-attachments/assets/dcfb8166-4869-4c4a-8155-a203abf9d6ef" />

The encryption key logic changes everytime, so by using the 2 chances to encrypt the the cheese, and the at the 3rd attempt use the guess option to get the cheese name,

Decrypted text →GASTANBERRAGDG

So finally i got the flag🎉🎉🎉🎉

Knowledge learnt:

Read the description as many times as you can, even though you thought that you have understood the question. You’ll find something every time you read the description.
— Tamil Arasan S
