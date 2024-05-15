---
id: 2726
title: '7 kits de développement PHP pour accepter les paiements en ligne sur votre e-commerce'
date: '2016-11-10T10:30:29+01:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=2726'
permalink: /blog/developpement-php/7-kits-de-developpement-php-pour-accepter-les-paiements-en-ligne-sur-votre-e-commerce/
dsq_thread_id:
    - '5293065655'
image: /wp-content/uploads/2016/11/paiment-php-sdk-ecommerce-700x525.png
categories:
    - 'PHP'
tags:
    - e-Commerce
    - 'Paiements en ligne'
    - PHP
---

Il y a quelques jours, je vous listais des [fournisseurs de services de paiement (PSP)](https://www.nicolashachet.com/blog/e-commerce/quels-systemes-de-paiement-psp-projet-web/) permettant d’accepter les paiements en ligne sur votre boutique e-commerce. Je continue sur le même sujet en vous présentant quelques kits de développements PHP pour gérer les paiements. J’ai retenu 7 prestataires de paiement :

- PayPal
- MangoPay
- Stripe
- Payline
- BitPay
- Simplify
- Authorize.Net

Ces SDK permettent de gérer des paiements coté serveur en allant interroger une API REST sécurisée. C’est ainsi que vous passez les ordres (de tokenization, de capture ou autre) sur la plateforme du prestataire que vous aurez retenu. Vous aurez à minima besoin d’une clef API que vous récupérez lors de la création de votre compte sur l’une de ces plateformes.

Globalement, les process de paiement des PSP sont généralement identiques et suivent le workflow suivant :

1. création d’une notion d’ordre de paiement (généralement un token) ;
2. validation du paiement (soit via l’envoi de données de carte, soit via la validation manuelle du paiement par l’utilisateur) ;
3. actions en cas de succès ou d’échec (généralement des URLs de callback ou de notifications selon les cas).

Vous devrez maîtriser ce process pour bien implémenter votre paiement en ligne.

Allez, c’est parti pour cette **sélection de kits de développement PHP pour faire du paiement en ligne** !

## PayPal PHP SDK

Le SDK Paypal : <https://paypal.github.io/PayPal-PHP-SDK/>

{% highlight php linenos %}  
$payer = new Payer();  
$payer->setPaymentMethod("paypal");

$amount = new Amount();  
$amount->setCurrency("USD")  
 ->setTotal(20)  
 ->setDetails($details);

$transaction = new Transaction();  
$transaction->setAmount($amount)  
 ->setItemList($itemList)  
 ->setDescription("Payment description")  
 ->setInvoiceNumber(uniqid());

$baseUrl = getBaseUrl();  
$redirectUrls = new RedirectUrls();  
$redirectUrls->setReturnUrl("$baseUrl/ExecutePayment.php?success=true")  
 ->setCancelUrl("$baseUrl/ExecutePayment.php?success=false");

$payment = new Payment();  
$payment->setIntent("sale")  
 ->setPayer($payer)  
 ->setRedirectUrls($redirectUrls)  
 ->setTransactions(array($transaction));  
{% endhighlight %}

## MangoPay PHP SDK

Le SDK Mangopay : <https://github.com/Mangopay/mangopay2-php-sdk>

{% highlight php linenos %}  
// register card  
$cardRegister = new \\MangoPay\\CardRegistration();  
$cardRegister->UserId = $createdUser->Id;  
$cardRegister->Currency = ‘EUR’;  
$createdCardRegister = $mangoPayApi->CardRegistrations->Create($cardRegister);

// build the return URL to capture token response  
$returnUrl = ‘http’ . ( isset($_SERVER[‘HTTPS’]) ? ‘s’ :" ) . ‘://’ . $_SERVER[‘HTTP_HOST’];  
$returnUrl .= substr($_SERVER[‘REQUEST_URI’], 0, strripos($_SERVER[‘REQUEST_URI’], ‘/’) + 1);  
$returnUrl .= ‘payment.php’;

<form action="<?php print $createdCardRegister->CardRegistrationURL; ?>" method="post">  
 <input type="hidden" name="data" value="<?php print $createdCardRegister->PreregistrationData; ?>" />  
 <input type="hidden" name="accessKeyRef" value="<?php print $createdCardRegister->AccessKey; ?>" />  
 <input type="hidden" name="returnURL" value="<?php print $returnUrl; ?>" />

 <label for="cardNumber">Card Number</label>  
 <input type="text" name="cardNumber" value="" />  
 <div class="clear"></div>

 <label for="cardExpirationDate">Expiration Date</label>  
 <input type="text" name="cardExpirationDate" value="" />  
 <div class="clear"></div>

 <label for="cardCvx">CVV</label>  
 <input type="text" name="cardCvx" value="" />  
 <div class="clear"></div>

 <input type="submit" value="Pay" />  
</form>  
{% endhighlight %}

## Stripe PHP SDK

Le SDK Stripe : <https://github.com/stripe/stripe-php>

{% highlight php linenos %}  
\\Stripe\\Stripe::setApiKey(‘d8e8fca2dc0f896fd7cb4cb0031ba249’);  
$myCard = array(‘number’ => ‘4242424242424242’, ‘exp_month’ => 8, ‘exp_year’ => 2018);  
$charge = \\Stripe\\Charge::create(array(‘card’ => $myCard, ‘amount’ => 2000, ‘currency’ => ‘usd’));  
{% endhighlight %}

## Payline By Monext PHP SDK

Le SDK Payline : <https://github.com/PaylineByMonext/payline-php-samples>

{% highlight php linenos %}  
$array[‘version’] = $_POST[‘version’];  
$array[‘transactionID’] = $_POST[‘transactionID’];  
$array[‘sequenceNumber’] = $_POST[‘sequenceNumber’];  
$array[‘media’] = $_POST[‘media’];

$response = $payline->doCapture($array);

if(isset($response[‘transaction’][‘id’])){  
 $res = insertTransactionData(  
 $array[‘payment’][‘contractNumber’],  
",  
 $response[‘transaction’][‘id’],  
 $array[‘payment’][‘action’],  
 $array[‘payment’][‘amount’],  
 $array[‘payment’][‘currency’],  
 $response[‘result’][‘code’]  
 );  
}

{% endhighlight %}

## BitPay PHP SDK

Le SDK BitPay : <https://github.com/bitpay/php-bitpay-client>

{% highlight php linenos %}  
$token = new \\Bitpay\\Token();  
$token->setToken($tokenString);  
/*\*  
 \* Code that makes the invoice  
 \*/  
$invoice = new \\Bitpay\\Invoice();  
$item = new \\Bitpay\\Item();  
$item  
 ->setCode(‘skuNumber’)  
 ->setDescription(‘General Description of Item’)  
 ->setPrice(‘1.99’);  
$invoice->setCurrency(new \\Bitpay\\Currency(‘USD’));  
$invoice->setItem($item);  
$client = $bitpay->get(‘client’);  
$client->setToken($token);  
try {  
 $client->createInvoice($invoice);  
} catch (\\Exception $e) {  
 $request = $client->getRequest();  
 $response = $client->getResponse();  
 echo (string) $request.PHP_EOL.PHP_EOL.PHP_EOL;  
 echo (string) $response.PHP_EOL.PHP_EOL;  
 exit(1); // We do not want to continue if something went wrong  
}  
{% endhighlight %}

## Simplify PHP SDK

Le SDK Simplify : <https://www.simplify.com/commerce/docs/sdk/php>

{% highlight php linenos %}  
 require_once("./lib/Simplify.php");  
 Simplify::$publicKey = ‘YOUR_PUBLIC_API_KEY’;  
 Simplify::$privateKey = ‘YOUR_PRIVATE_API_KEY’;  
 $token = $_POST[‘simplifyToken’];  
 $payment = Simplify_Payment::createPayment(array(  
 ‘amount’ => ‘1000’,  
 ‘token’ => $token,  
 ‘description’ => ‘prod description’,  
 ‘currency’ => ‘USD’  
 ));  
 if ($payment->paymentStatus == ‘APPROVED’) {  
 echo "Payment approved\\n";  
 }  
{% endhighlight %}

## Authorize.Net PHP SDK

Le SDK Authorize.Net : [https://developer.authorize.net/hello_world/](https://developer.authorize.net/hello_world/)

{% highlight php linenos %}  
// Create the payment data for a credit card  
 $creditCard = new AnetAPI\\CreditCardType();  
 $creditCard->setCardNumber("4111111111111111" );  
 $creditCard->setExpirationDate( "2038-12");  
 $paymentOne = new AnetAPI\\PaymentType();  
 $paymentOne->setCreditCard($creditCard);

// Create a transaction  
 $transactionRequestType = new AnetAPI\\TransactionRequestType();  
 $transactionRequestType->setTransactionType("authCaptureTransaction");  
 $transactionRequestType->setAmount(151.51);  
 $transactionRequestType->setPayment($paymentOne);  
 $request = new AnetAPI\\CreateTransactionRequest();  
 $request->setMerchantAuthentication($merchantAuthentication);  
 $request->setRefId( $refId);  
 $request->setTransactionRequest($transactionRequestType);  
 $controller = new AnetController\\CreateTransactionController($request);  
 $response = $controller->executeWithApiResponse(\\net\\authorize\\api\\constants\\ANetEnvironment::SANDBOX);  
{% endhighlight %}

C’est terminé ! J’espère que vous y voyez plus clair sur l’implémentation du paiement en ligne coté serveur sur votre site de vente en ligne.
