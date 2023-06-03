# Aussie-phone-number-picker
Wanna have a cool phone number?
## AIM  
It's time to have a coooooooooool Aussie phone number! There are some mobile service provider allow customer to pick their own phone number. Let's make a crawler and fetch all the cool phone numbers avaible for purchase!

## Step 1: crawl all the availble phone number  
### Amaysim  
[Amaysim](https://www.amaysim.com.au/mobile/cart/unlimited-4gb?promo=EOFY23) allow customer to pick the phone number online. It will be very ez to fetch all the phone numbers from the [API](https://api.amaysim.com.au/mobile/graphql).  
I use Fiddler to repeatly call the API without worrying about the header/payload of the http request. Then I save all the response into a text file, wash it with python scripts.
![image](https://github.com/lrlrlrlr/Aussie-phone-number-picker/assets/27357380/1ae4d7bc-206b-4c9b-86c9-f9b094e220df)

Here are the availble phonenumbers: https://github.com/lrlrlrlr/Aussie-phone-number-picker/amaysim.json  

## Step 2: List all the cool numbers
To list all the cool numbers, I use regex
```
import re # Regex

# Regex rules:
AAA= r"\d*(\d)\1{2,}\d*"   # e.g. 0410666184
AAAA = r"\d*(\d)\1{3,}\d*" # e.g. 04106666871
ABCCBA = r"(\d)(\d)(\d)\3\2\1" # e.g. 0410468864
ABCBA = r"(\d)(\d)(\d)\2\1" # e.g. 0410146864
AABB = r"(\d)\1(\d)\2" # e.g. 0411012233
AABBCC = r"(\d)\1(\d)\2(\d)\3" # e.g. 0411223341
AXAXAXAX = r"(\d)\d\1(\d)\1(\d)\1" # e.g. 041513141
INCREMENT = r"((?:0(?=1)|1(?=2)|2(?=3)|3(?=4)|4(?=5)|5(?=6)|6(?=7)|7(?=8)|8(?=9)|9(?=0)){4,}\d)" # e.g.  0412345678
DECREMENT = r"((?:0(?=9)|9(?=8)|8(?=7)|7(?=6)|6(?=5)|5(?=4)|4(?=3)|3(?=2)|2(?=1)|1(?=0)){4,}\d)" # e.g. 0476543210

# load the json file into here
all_phone_nums = ['0481312221', '0434348129', '0434073154',....]

# list the AAA numbers
print([phone for phone in all_phone_nums if re.search(AAA, phone)])
>>> ['0444425836', '0413111389', '0431666791', '0468433324', '0468341116'.....]

# list the AXAXAXAX numbers
print([phone for phone in all_phone_nums if re.search(AXAXAXAX, phone)])
>>> ['0468386265', '0434098197', '0435348206', '0466756865', '0434098359', .....]

```




## Step 3: pick your fav numbers, purchase it on the provider website

