in this crackme our goal is find username and Password
so for saving my time i do dynamic analysis that come very handy when you know that code is decrypting specif value at some point and comapre that value with 
your input 

```c#
string text = "BananaIsGood";
			Program.CryptedWord[] array = new Program.CryptedWord[5];
			Program.CryptedWord[] array2 = new Program.CryptedWord[5];
			array[0] = new Program.CryptedWord("Vbzzl", text.Length);
			array[1] = new Program.CryptedWord("Thynqegb", text.Length);
			array[2] = new Program.CryptedWord("Mfgbxrb", text.Length);
			array[3] = new Program.CryptedWord("VmwqCmhx", text.Length);
			array[4] = new Program.CryptedWord("YmelVmzq", text.Length);
			array2[0] = new Program.CryptedWord("Nmzmzm", text.Length);
			array2[1] = new Program.CryptedWord("UxuwqEuoq", text.Length);
			array2[2] = new Program.CryptedWord("EuoqUfGemft", text.Length);
			array2[3] = new Program.CryptedWord("RxbeqfgBrFhuoupq", text.Length);
			array2[4] = new Program.CryptedWord("FcupqeYmz", text.Length);
			bool flag = false;
```
in this section of code we can clearly see that there is 2 array one is contain username and other one is contain password so you just need to set brackpoint and
comparesion point and analysis with what value its comapre our username and password


![image](https://user-images.githubusercontent.com/37813830/121817233-bb587380-cc9d-11eb-94df-78995e44c07d.png)

if you check here that decrypt username and compare that username with your input 

![image](https://user-images.githubusercontent.com/37813830/121817317-49ccf500-cc9e-11eb-93e7-e4467d5f7bb1.png)

when i start execution of program its hit brackpoint and i can clearly see that its decode ``Vbzzl`` to ``jonny`` and i got username now lets start execution again and set
brackpoint at password compare, after input right user name Jonny and wrong password when i hit my brackpoint i found password `Banana` 
we can also analysis same things for other username and password you just need to step over decrypto function and its decrpt every username and compare with our input 
```
name:Jonny - pass: Banana
name:Humberto - pass: IlikeRice
name:Astolfo - pass: RiceIsTrash
name:JakePaul - pass: FlorestOfSuicide
name:MaryJan - pass: SpiderMan
```



![image](https://user-images.githubusercontent.com/37813830/121817489-5e5dbd00-cc9f-11eb-93bb-2be1d8102b90.png)
