after opening file in `DNSPY` i notice a function called btnCheck_click so besically its check a serial key and compare with some text 

![image](https://user-images.githubusercontent.com/37813830/121816205-eb9d1380-cc97-11eb-9b21-9aa3933096ef.png)

you can see that its compare a serial key with value and value is combination of text3 , text , text4 and text5 
so i check that function and i found that text3, text4 and text5 is besically a Product ID that showen in application 

![image](https://user-images.githubusercontent.com/37813830/121816247-2901a100-cc98-11eb-9f56-e778daf3e2a1.png)


```
string value = text3 + text + text4 + text5;
```

serial key is combination of Name and Product id we can clear see that our text contain our username and its only access (0, 4) substrings in upper case so 

```serial key =  X398{Name}33CEA639```

![image](https://user-images.githubusercontent.com/37813830/121816314-7e3db280-cc98-11eb-8972-13bd93ff9514.png)
