## **Berlin Group Payment Initiation v1.3.6 Sandbox API** 
****
### **Introduction to the API**
This API helps you perform a Domestic or International Payment. You may perform an immediate payment, schedule a future payment or even schedule a Standing Order.
The api follows the Berlin Group Specification v1.3.6.

### **Real Life Use Case Scenario**
Imagine you want to perform a Payment using your own application. What can you do about it? Just use this api to make a payment, in any platform you prefer.

### **Create Sandbox**
Your first job is to create a sandbox and save your **sandbox-id** in order to be able to **"play"** with the api.

We will create our sandbox by making an **HTTP POST** request to the following URL:
> https://apis.nbg.gr/sandbox/bg.openbanking.payments/oauth2/v1/sandbox

Request Body:
```json
 {
   "sandbox-id": "my-payments-sandbox"
 }
``` 

**Note: Remember to store *sandbox-id* somewhere in your application, because you will need to provide it as a header
in each api call. Also remember to use the *Client-Id* provided when you create your application in the portal.**

When you create the sandbox application it has some default data.
## **Request Headers**
The following headers are required for every call. In postman they are in the appropriate environment variables.

**Request Headers**:
```
   'accept: application/json'
   'X-Request-ID: {{$guid}}
   'sandbox-id: {{sandboxId}}'  
   'Client-Id: {{clientId}}'

``` 
## **Scenario Request**
You send **/v1/payments/sepa-credit-transfers** request to make an immediate SEPA Credit Transfer.
> https://apis.nbg.gr/sandbox/bg.openbanking.payments/oauth2/v1/payments/sepa-credit-transfers

**Request**
```json
{
    "endToEndIdentification": "endToEndIdentification",
    "debtorAccount": {
        "iban": "GR3201106970000069774934603",
        "currency": "EUR"
    },
    "instructedAmount": {
        "currency": "EUR",
        "amount": "1010"
    },
    "creditorAccount": {
        "iban": "GR0601100400000004001504283",
        "currency": "EUR"
    },
    "creditorName": "CREDITOR NAME",
    "remittanceInformationUnstructured": "Some unstructed information",
    "chargeBearer": "Shared",
    "priorityCode": "Normal"
}
``` 

**Response** (Contains information about the available accounts (e.g. currency, type, description)):
```json
{
    "paymentId": "88fc8c50-252d-4aa6-a83b-21e1ba8a3cc0",
    "transactionStatus": "PDNG",
    "endToEndIdentification": "endToEndIdentification",
    "debtorAccount": {
        "iban": "GR3201106970000069774934603",
        "currency": "EUR"
    },
    "instructedAmount": {
        "currency": "EUR",
        "amount": "1010.00"
    },
    "transactionFees": {
        "currency": "EUR",
        "amount": "0.00"
    },
    "estimatedTotalAmount": {
        "currency": "EUR",
        "amount": "1010.00"
    },
    "creditorAccount": {
        "iban": "GR0601100400000004001504283"
    },
    "creditorName": "CREDITOR NAME",
    "creditorAgent": "ETHNGRAA",
    "remittanceInformationUnstructured": "Some unstructed information",
    "chargeBearer": "Shared",
    "_links": {
        "scaRedirect": "https://microsites.nbg.gr/bg.ob.pisp.sandbox/payments/authorize?payment_id=88fc8c50-252d-4aa6-a83b-21e1ba8a3cc0",
        "self": "https://apis.nbg.gr/sandbox/bg.openbanking.payments/oauth2/v1/payments/sepa-credit-transfers/88fc8c50-252d-4aa6-a83b-21e1ba8a3cc0",
        "status": "https://apis.nbg.gr/sandbox/bg.openbanking.payments/oauth2/v1/payments/sepa-credit-transfers/88fc8c50-252d-4aa6-a83b-21e1ba8a3cc0/status"
    }
}

``` 


Created by **NBG**.\
See more at https://developer.nbg.gr/