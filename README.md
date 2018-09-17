# imepaySDK_iOS

## IME PAY MERCHANT PAYMENT SDK FOR iOS

Receive payment from your customer through IME Pay Wallet.

 ## Overview

- Introduction
- SDK Feature
- SDK Initialization
- Authenticate Merchant
- Get Transaction Token
- Perform Payment
- Validate Payment
- Response Codes

The IME Pay Payment SDK for iOS gives access to merchants to receive payment from IME Pay customers through their native iOS application.

## SDK Features

IME Pay iOS Merchant Payment SDK enables merchants to receive payments from IME pay customes through their native application. The SDK performs the payment and returns transaction details after transaction succeeds or fails or cancelled with proper error message.

## SDK Installation

Cocoapods, iOS 8+

```use frameworks!```

```pod 'IMEPay'``` 

uncomment use frameworks in your pod file in case of swift projects.

## Authenticate Merchant / Get Transaction Token

The merchant is verified using the merchant code, merchant username, merchant password, module which will be provided by the IME Pay Support to applicable merchants.

## Perform Payment:

###### Objective C:

  ``` 
  IMPPaymentManager *manager = [[IMPPaymentManager alloc]initWithEnvironment:Live]; // For Production
  
  IMPPaymentManager *manager = [[IMPPaymentManager alloc]initWithEnvironment:Test]; // For Test
    
   [manager payWithUsername:@"username" password:@"password" merchantCode:@"merchantCode" merchantName:@"merchantName" merchantUrl:@"merchantUrl" amount:@"amount" referenceId:@"referenceId" module:@"module" success:^(IMPTransactionInfo *transactionInfo) {
        
        // You can extract the following info from transactionInfo
        
        transactionInfo.responseCode; 
        
        // Response Code 100:- Transaction successful.
        // Response Code 101:- Transaction failed.
        
        transactionInfo.responseDescription; // ResponseDescription, message sent from server
        transactionInfo.transactionId; // Transaction Id, Unique ID generated from IME Pay system.
        transctionInfo.customerMsisdn; // Customer mobile number (IME Pay wallet ID)
        transctionInfo.amount; // Payment Amount
        transactionInfo.referenceId; // Reference Value
 
    } failure:^(IMPTransactionInfo *transactionInfo, errorMessage) {
         // Transaction Failure
    }];

  ``` 

###### Swift:

  ``` 
  let manager = IMPPaymentManager(environment: Live) // For production
  
  let manager = IMPPaymentManager(environment: Test) // For Test
  
 manager?.pay(withUsername: "username" , password: "password", merchantCode: "merchantCode", merchantName: "merchantName",    merchantUrl: "merchantUrl", amount: "amount", referenceId: "referenceId", module: "module", success: { (transactionInfo) in
  
        // You can extract the following info from transactionInfo
        
        transactionInfo.responseCode 
        
        // Response Code 100:- Transaction successful.
        // Response Code 101:- Transaction failed.
        
        transactionInfo.responseDescription // ResponseDescription, message sent from server
        transactionInfo.transactionId // Transaction Id, Unique ID generated from IME Pay system.
        transctionInfo.customerMsisdn // Customer mobile number (IME Pay wallet ID)
        transctionInfo.amount // Payment Amount
        transactionInfo.referenceId // Reference Value
 
  }, failure: { (transactionInfo, errorMessage) in
         // Transaction Failure
   })
 ``` 

###### Note: You can use transaction info passed in success and failure blocks, you shouldnt present any alert when success or failure block is called.

## Response Codes

These response codes mentioned below are handled by the SDK itself.

**403** : Application unauthorized to use the service.

**500** : Your request cannot be processed at the moment

**401** : Application request cannot be processed at the moment



