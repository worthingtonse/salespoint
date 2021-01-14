# SALES POINT
Allows People to Sell CloudCoins
The Sales Point will allow buyers to purchase and receive CloudCoins using multiple payment methods. 

The program will be written in PHP so that in the future it can be put on webservers running on hosted systems and desktops. 

## Components of the Sales Point:
1. Configuration File
2. Inventory Scanner
3. Price Finder
4. Buyer's Coin Selection Form
5. Payment System Form Array 
6. Payment System Webhooks Array
7. Logger. 
8. Email Alerter
9. Coin Delivery
--Send to buyer's Skywallet
--Send to buyer's Email with message, links to cloudCoins.
--Down as stack file.
10. Thank you page.
11. Upsale?? (Try RAIDA Mail)


## 1. Configuration File

This is called "config.php"
It allows the user to customize some settings
```php
declare( PATH_TO_SKYWALLET_ID = "/opt/sales_point/id/me.skywallet.cc.stack" );
declare( PATH_TO_BANK = "/opt/sales_point/bank/" ); // Coin Storage Folder
declare( PATH_TO_LOG = "/opt/sales_point/logs/" );
declare( MIN_COINS = 1000 ); // The minum amount of coins the buyer must buy
declare( MAX_COINS = 100000 ); // The maxium number of coins a buyer can buy
declare( ALLOW_CHANGE = false ); // Can force purchase of only coins the have
declare( MINIMUM_PRICE = .01 ); //Dollars per coin from the bitcoin.com exchange.
declare( GET_PRICE_DYNAMICALLY = true); 
declare( CONVENIENCE_FEE = .24); // How much over the discovered price that should be charged. 
declare( EXCHANGE_DATA_URL = "https://bitcoin.com/cce/feed" );
declare( SUPPORT_EMAIL = "me@gmail.com");
declare( SUPPORT_PHONE = "530-784-9933");
declare( SMTP_USERNAME = "dfkjs" ); //To send customers coins

/* Payment System API Info*/
declare( PAYPAL_KEY = "dfkjs" ); 
declare( STRIPE_KEY = "dfkjs" ); 
declare( OMNI_PAY_KEY = "dfkjs" ); 
```
## 2. Inventory Scanner
The program will not allow the seller to sell more coins then they have. The seller may have coins in their skywallet or their local bank folder. 
When a person goes to the buy page, the program counts the coins in the bank folder and calls the Skywallet balance for sale service. 
The bank folder can be scaned by the php before the page is delivered and the skywallet can be checked by javascrpt when the page loads. 

## 3. Price Finder
If the page is configured to find the price dynaomically, the page will query the bitcoin.com exchange to learn the currency exchange price. Convieints fee will be then added to diplay the fee. The default value of the price will be "Determining Price".

 ## 4. Buyer's Coin Selection Form
 This is a form that allows the buyer to specify how many coins they want to buy. The page gives them the total sales price. 
 This page also gives them info that they may need before they can make a purchase decision. This page could also allow buyers to specity how they want the coins delivered (Skywallet or download).
 Lastly, this page allows the user to choose the payment method. 
 
 Support information should be included on this page. 

## 5. Payment System Form Array 
Once the person chooses payment system, they may be directed to a page that is specifically for the payment systemed specified. Since there are many possible payment systems, there maybe many possible pages. 

## 6. Payment System Webhooks Array
Each Payment System may call back to this webserver in a differant way and require a different URL to handle the response. Thus we may need a different webhook for each payment system. 

## 7. Logger. 
All sales should be logged in the Sales log. All errors should be put in the error log. We may also want to track our own anylitics so we do not need to use Google Anylitics. We could track when pages are opened and by what IP address. 

## 8. Email Alerter
Every time a sale is made, an email should be sent to the seller. The email should tell the seller:
	* How many dollars the sales was for
	* How many Cloudcoins are still on their Sales Point
	* WARN if the CloudCoins are running low. 
	* Email of the person who made the purchase.
	* Payment Method used (Like PayPal or Stripe)

## 9. Coin Delivery

If the coins are sent to the buyer's Skywallet:
The coins will then be delivered via Skywallet by calling the "Transfer" service. Or the can be sent from the bank folder by using the "Send" service. The memo should start with at GUID.

If the coins are sent to the buyer in the form of hyper links so they can download a stack file with the coins:
There will be an "orders" folder. In the Orders folder there will be a folder for every order. Each folder should be named after a unique identifier. And it is helpful to include the amount in the folder name. Each folder will hold all the stack of the users coins and have a random number in the file name so it cannot be guessed. These folders will not be browsable. 

## 10. Thank you page.
If the users elected to download their coins, then the "Thank You" page will send the user an email with links to their CloudCoins and also present them with links to their CloudCoins. 

If the user wanted the coins sent to their skywallet, then the user will be told to check their skywallet and given the guid that was included . 

Support information and direction on how to procceed should be included on this page. 
