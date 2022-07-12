*This will be my 1st "write-up", and I appreciate everyone for taking time to read it. I am new to contributing content of any type, and would appreciate any suggestions, advice, or guidance if you see something I should be aware of -- please notify me. Thank you.*


Let’s begin by introducing myself and to add some clarification on how this came about. I prefer to call myself **JuanitoVerde**, someone who has always been interested in how things work; throughout the years this has caused me to break many things beyond repair. 
One lovely thing about API’s , they’re usually not going to break or become damaged physically after I’m done with it, I hope. Secondly, at least you can patch code — you can’t patch circuit boards after you give them to me. 

Now let’s discuss the moments that lead up to my addiction of abusing API’s. There I was at the infamous Target Store, wondering why my darling Fry’s Electronics left me; leaving a hole in my heart needing to be filled. Also, I needed phone service, I got tired of paying 80$ a month so target has some great affordable month-to-month options. While browsing the Phone Card section one day, I saw 7 Day Trials for Mint Mobile for 2$. *“Hmm 4weeks x 2dollars = 8$ a month”*, I thought to myself. I grabbed the last remaining ones, happily went to checkout and thought life couldn’t be sweeter. 80$ a month to 8$ a month, *haha! I feel like I’m finally beating the system.* 

Now here comes where the fun stuff begins. I’m there on Mint Mobiles website per instruction of the cards I had just purchased. 

https://my.mintmobile.com/activation

Being the person I am, we know I just like to know how things work. *What do I do?* I obviously do everything in my power to break this thing, just kidding. **I decide to inspect the page** source and look at the html source code, see what files are being linked, what resources are being used, where these files are located, and mentally mapping the file folder system and keeping mental notes of things that look interesting. I feel like a kid in a candy store, but no candy… where is my act code being sent to? 

I sometimes have bad vision staring at a screen so often, I probably over looked it. So let’s make things easier, ***right click > inspect*** (this is where the fun really starts. Hold on tight )

It’s such a lovely thing, isn’t it ? Organized and full of interesting things to question — something we don’t have in common, but they do say opposites attract .

I enter 11 random numbers as the ACT code, I watch it appear in the panel as a request being made to... another site? What’s this. 

https://w3b-api.ultramobile.com/v2/mint/sims?actCode=12345678901

and for reference, what a valid response looks like

https://w3b-api.ultramobile.com/v2/mint/sims?actCode=DDEJC317JEF

**{"deliveryType":"PHYSICAL","id":"890126089711559827","masterAgent":745,"distributor":837,"initialProductId":7000239,"productType":"ECOMM","token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJnZW4zVG9rZW4iOiJleUpoYkdjaU9pSlNVekkxTmlJc0luUjVjQ0k2SWtwWFZDSjkuZXlKaWNtRnVaQ0k2SWsxSlRsUWlMQ0ppY21GdVpGUjVjR1VpT2lKSlRsUkZVazVCVENJc0ltVjRjQ0k2TVRZMU56WXpOVFV3Tml3aWFXUnpJanA3SWpjME16Z3dOelVpT25zaVpuVnNiQ0k2ZEhKMVpYMTlMQ0p1WW1ZaU9qRTJOVGMyTXpFMk1EWXNJbTl5YVdkcGJpSTZOelF6T0RBM05Td2lkWE5sY2tWdWRpSTZJbEJTVDBRaWZRLlJtZG55Mzd1MmZ1N09rSlRMeHJhX1IwXzQxLWFFckJNYnNxQWpackhDVzAtRWZVOWxKOUkzOUY4c3ktejM2aVE4cERTdXhJcnJQS3BFTkRCOXhXNGRUWDIxM3ZlZHN5WWNaOFBjUHBBbkFnb1VOcXQ0a3hnVjJkMm5JQmFsTVdQWEdjV3dVQ0k4ekJPeEVTZmtHMmh1UnZ0X2RPM1J0VFBKcHZUaGNieDRsNUwzaVZxMzIwQkh5cHZaT2RaUFlreHkxN3lqekhFeVhOX2xLYVJ0MG9NSV9JbzdiZ21jWE5zRXBMYVZMZEQyODh3anMzM2pkclNWU2RmUV9fNDU3ZlM0TU1YRnZodUE3RHlDdnNNNXpicUJ4Sy15U1VLWU9fZ184X0gyUi1SN29aYXpySzBhTldqeWk3SHBxOF8yMXl5Y1RJTEtPOGZsT1FfT292eGFtMzVudyIsInVzZXJJZCI6NzQzODA3NSwiSUNDSUQiOiI4OTAxMjYwODk3MTE1NTk4MjciLCJicmFuZCI6Im1pbnQiLCJpcCI6IjE3Mi4yNDguNDYuMTgiLCJpYXQiOjE2NTc2MzE5MDYsIm5iZiI6MTY1NzYzMTkwNiwiZXhwIjoxNjU3NjMyODA2LCJpc3MiOiJVTFRSQSJ9.bZbhC_kQGftQ5v1Qilu6oCytNcJISOEsSns1lZnijLw","userId":"7438075","status":"neutral"}**

So let's just see whats going on here..

***"deliveryType": "PHYSICAL", ## I'm sure this means physical card...
   "id": "890126089711559827", ## The '89' tells me it's the SIM's IMEI # .. Which may be helpful.
   "masterAgent": 745, ## Unsure.. Maybe the Warehouse Code or Main Seller? I don't know. 
   "distributor": 837, ## Target? Or The Store I got the code from.
   "initialProductId": 7000239, ## "Product ID" not sure what "initial" is suppose to be refering to..
   "productType": "ECOMM" ## I wonder what otehr types they have? ECOMM = Ecommerece I'm guessing aswell. ***
  
Im going to assume that the long token is base64. I hope I'm right.
***"token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJnZW4zVG9rZW4iOiJleUpoYkdjaU9pSlNVekkxTmlJc0luUjVjQ0k2SWtwWFZDSjkuZXlKaWNtRnVaQ0k2SWsxSlRsUWlMQ0ppY21GdVpGUjVjR1VpT2lKSlRsUkZVazVCVENJc0ltVjRjQ0k2TVRZMU56WXpOVFV3Tml3aWFXUnpJanA3SWpjME16Z3dOelVpT25zaVpuVnNiQ0k2ZEhKMVpYMTlMQ0p1WW1ZaU9qRTJOVGMyTXpFMk1EWXNJbTl5YVdkcGJpSTZOelF6T0RBM05Td2lkWE5sY2tWdWRpSTZJbEJTVDBRaWZRLlJtZG55Mzd1MmZ1N09rSlRMeHJhX1IwXzQxLWFFckJNYnNxQWpackhDVzAtRWZVOWxKOUkzOUY4c3ktejM2aVE4cERTdXhJcnJQS3BFTkRCOXhXNGRUWDIxM3ZlZHN5WWNaOFBjUHBBbkFnb1VOcXQ0a3hnVjJkMm5JQmFsTVdQWEdjV3dVQ0k4ekJPeEVTZmtHMmh1UnZ0X2RPM1J0VFBKcHZUaGNieDRsNUwzaVZxMzIwQkh5cHZaT2RaUFlreHkxN3lqekhFeVhOX2xLYVJ0MG9NSV9JbzdiZ21jWE5zRXBMYVZMZEQyODh3anMzM2pkclNWU2RmUV9fNDU3ZlM0TU1YRnZodUE3RHlDdnNNNXpicUJ4Sy15U1VLWU9fZ184X0gyUi1SN29aYXpySzBhTldqeWk3SHBxOF8yMXl5Y1RJTEtPOGZsT1FfT292eGFtMzVudyIsInVzZXJJZCI6NzQzODA3NSwiSUNDSUQiOiI4OTAxMjYwODk3MTE1NTk4MjciLCJicmFuZCI6Im1pbnQiLCJpcCI6IjE3Mi4yNDguNDYuMTgiLCJpYXQiOjE2NTc2MzE5MDYsIm5iZiI6MTY1NzYzMTkwNiwiZXhwIjoxNjU3NjMyODA2LCJpc3MiOiJVTFRSQSJ9.bZbhC_kQGftQ5v1Qilu6oCytNcJISOEsSns1lZnijLw"***

**eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJicmFuZCI6Ik1JTlQiLCJicmFuZFR5cGUiOiJJTlRFUk5BTCIsImV4cCI6MTY1NzYzNjIzMSwiaWRzIjp7Ijc0MzgwNzUiOnsiZnVsbCI6dHJ1ZX19LCJuYmYiOjE2NTc2MzIzMzEsIm9yaWdpbiI6NzQzODA3NSwidXNlckVudiI6IlBST0QifQ**

Well, Now I’m curious. Why? So I pop open my cellular device, tell Siri to ring up my good old pal Ryan Reynolds and see what’s going on here. Well unfortunately, Siri doesn’t have that contact in my phone book and Ryan Reynolds probably doesn’t even know who I am. Not yet at least. *if you’re reading this Mr. Reynolds, I appreciate you. You’re awesome. I don’t mean any harm or intend for any disrespect. Thank you!*

So now just form assumptions. We know T-Mobile and these providers have smaller companies such as Mint and Ultra and others we don’t need to name, that for a lack of better terms, “piggy back” off there network and cell towers. These companies can provide us quality service at better rates , and In reality the only difference it seems to me is sacrificing “priority” of service. Meaning, tor 80$ a month, you get to load YouTube videos faster then me at the airport. Not a problem, I don’t have money to fly anywhere anyways. 

So I’m assuming mint is doing the same or has a contract with ultra ? It looks like the sites damn near operate the same or have the same developers. Maybe they just use there developers and this was a productive and cost efficient way of handling the web aspect of things. I don’t know. 

We can now blame ultra mobile and not Deadpool for what’s about to come, right? We can blame the awesome information that is given upon the right code being supplied. What a nice detailed xml report. 
