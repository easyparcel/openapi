# Easy Parcel API  <img src="pictures/EasyParcel-TransparentSquare-md.png" alt="Logo" style="width:65px; margin:0; padding:0;">


 
The EasyParcel API allows your application to access current data within EasyParcel. However, EasyParcel API is using RESTful with PHP concept to develop API for web based applications. Through the API, several common operations can be performed on EasyParcel objects.

**Links to our API**

All API URLs start with the following base part:

| API         | Link                               |
| ----------- | ---------------------------------- |
| Development | http://demo.connect.easyparcel.my/ |
| Production  | https://connect.easyparcel.my/     |


- Demo URL is only for testing purposes.

- Live URL is for real live transaction usage.



#### Follow the guide below to integrate with easy parcel api.
#### <u>[Get started with EASY PARCEL OPEN API](Get%20started%20with%20EASY%20PARCEL%20OPEN%20API.md)</u>



##### API Functions/Features:

**[Get Shipment Quotation](#Get-Shipment-Quotation)**

**[Get Insurance Quotation](#Get-Insurance-Quotation)**

**[Get Courier Dropoff point](#Get-Courier-Dropoff-point)**

**[Submit Shipment Orders](#Submit-Shipment-Orders)**

**[Get OnDemand Quotation](#Get-OnDemand-Quotation)**

**[Submit OnDemand Order](#Submit-OnDemand-Order)**

---

**[References](#References)**

---
<br>

### Get Shipment Quotation:
Get Shipment Quotation: This feature enables users to obtain shipment quotations from all courier companies available on the EasyParcel platform. Users need to provide sender and receiver addresses to check the shipment quotation.

<details id="Request"> 
  <summary><h5>Request:</h5></summary> 
 
##### Request

Parameters used:
L1

| Requested Parameters | Type        | Required | Description                                                 |
| -------------------- | ----------- | -------- | ----------------------------------------------------------- |
| from_postcode        | string(10)  | Yes      | Sender's postcode                                           |
| from_state           | string(35)  | Yes      | Sender's state (refer to [ISO_3166](#iso3166))              |
| from_country         | string(2)   | Yes      | Sender's country (refer to [country code](#country-code))   |
| to_postcode          | string(10)  | Yes      | Receiver's postcode                                         |
| to_state             | string(35)  | Yes      | Receiver's state (refer to [ISO_3166](#iso3166))            |
| to_country           | string(2)   | Yes      | Receiver's country (refer to [country code](#country-code)) |
| weight               | double(8,2) | Yes      | The weight of the parcel.                                   |


Request Sample Code:
```
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => 'https://developer.easyparcel.com/open_api/shipment/quotations',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS =>'{
  "list": [
    {
      "from_postcode": "09600",
      "from_state": "MY-02",
      "from_country": "my",
      "to_postcode": "11950",
      "to_state": "MY-07",
      "to_country": "my",
      "weight": 0.5
    }
       
  ]
}',
  CURLOPT_HTTPHEADER => array(
    'Content-Type: application/json'
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;

```
</details>


<details id="Return"> 
  <summary><h5>Return:</h5></summary>
 
##### Return

Returned Parameters:
L1

| Returned Parameters | Type       | Description                                                         |
| ------------------- | ---------- | ------------------------------------------------------------------- |
| from_postcode       | string(10) | Sender's postcode                                                   |
| from_state          | string     | Sender's state (refer to [ISO_3166](#iso3166))                      |
| from_country        | string     | Sender's country                                                    |
| to_postcode         | string     | Receiver's postcode                                                 |
| to_state            | string     | Receiver's state (refer to [ISO_3166](#iso3166))                    |
| to_country          | string     | Receiver's country                                                  |
| weight              | double     | parcel's weight                                                     |
| unit                | int        | unit of items                                                       |
| uuid                | string     | UUID of the Quotation                                               |
| quotations          | array      | Quotations / Service available (refer to [quotations](#quotations)) |

L2
###### quotations

| Returned Parameters        | Type    | Description                                                  |
| -------------------------- | ------- | ------------------------------------------------------------ |
| service_id                 | string  | service identification number                                |
| service_id2                | string  | service identification number 2                              |
| service_name               | string  | Service Name (method)                                        |
| courier_id                 | string  | Courier service identification number                        |
| courier_name               | string  | Courier service                                              |
| courier_uuid               | string  | UUID of the courier                                          |
| courier_image_fullpath     | string  | Image of the courier service                                 |
| courier_logo_fullpath      | string  | Logo of the courier service                                  |
| delivery_duration          | string  | Time take to delivery the parcel                             |
| price                      | double  | Price on the delivery                                        |
| price_currency             | string  | Currency of the delivery                                     |
| exchange_rate              | double  | Exchange rate of currency                                    |
| exchange_rate_id           | string  | Exchange rate identification number of currency              |
| cod_service_available      | boolean | Availability of the cash on delivery service                 |
| cod_service_min_cod_amount | double  | Minimum amount for the COD service                           |
| cod_service_max_cod_amount | double  | Max amount for the COD service                               |
| cod_charges_conditions     | string  | Conditions under which Cash on Delivery (COD) charges apply. |

Respond Sample:
```
{
    "status_code": 200,
    "message": "Success",
    "data": [
        {
            "from_postcode": "09600",
            "from_state": "MY-02",
            "from_country": "my",
            "to_postcode": "11950",
            "to_state": "MY-07",
            "to_country": "my",
            "weight": 0.5,
            "unit": "kg",
            "uuid": "1",
            "quotations": [
                {
                    "service_id": "EP-CS0IU",
                    "service_id2": 128,
                    "service_name": "Skynet (Drop-Off)",
                    "courier_id": "EP-CR0AY",
                    "courier_name": "Skynet Express (M) Sdn. Bhd.",
                    "courier_uuid": "1ca9ebbd-f3c7-4696-b232-39a448d7ae1c",
                    "courier_image_fullpath": "https://s3-ap-southeast-1.amazonaws.com/easyparcel-static/Public/source/general/img/couriers/Skynet.jpg",
                    "courier_logo_fullpath": "https://s3-ap-southeast-1.amazonaws.com/easyparcel-static/Public/source/general/img/couriers/SKYNET-EXPRESS.png",
                    "delivery_duration": null,
                    "price": "9.86",
                    "price_currency": "SGD",
                    "exchange_rate": "0.3023089000",
                    "exchange_rate_id": 94376,
                    "cod_service_available": false,
                    "cod_service_min_cod_amount": "",
                    "cod_service_max_cod_amount": "",
                    "cod_charges_conditions": ""
                },
                {
                    "service_id": "EP-CS0IK",
                    "service_id2": 129,
                    "service_name": "Skynet (Pick Up with min 4 parcel(s))",
                    "courier_id": "EP-CR0AY",
                    "courier_name": "Skynet Express (M) Sdn. Bhd.",
                    "courier_uuid": "1ca9ebbd-f3c7-4696-b232-39a448d7ae1c",
                    "courier_image_fullpath": "https://s3-ap-southeast-1.amazonaws.com/easyparcel-static/Public/source/general/img/couriers/Skynet.jpg",
                    "courier_logo_fullpath": "https://s3-ap-southeast-1.amazonaws.com/easyparcel-static/Public/source/general/img/couriers/SKYNET-EXPRESS.png",
                    "delivery_duration": null,
                    "price": "9.86",
                    "price_currency": "SGD",
                    "exchange_rate": "0.3023089000",
                    "exchange_rate_id": 94376,
                    "cod_service_available": false,
                    "cod_service_min_cod_amount": "",
                    "cod_service_max_cod_amount": "",
                    "cod_charges_conditions": ""
                },
                {
                    "service_id": "EP-CS0IN",
                    "service_id2": 119,
                    "service_name": "DHL eCommerce (Pick Up with min 3 parcel(s))",
                    "courier_id": "EP-CR0AW",
                    "courier_name": "DHL eCommerce",
                    "courier_uuid": "db129869-d2cd-474a-b3bf-9995a436ef85",
                    "courier_image_fullpath": "https://s3-ap-southeast-1.amazonaws.com/easyparcel-static/Public/source/general/img/couriers/DHLeC.jpg",
                    "courier_logo_fullpath": "https://s3-ap-southeast-1.amazonaws.com/easyparcel-static/Public/source/general/img/couriers/dhllogo.jpg",
                    "delivery_duration": null,
                    "price": "2.03",
                    "price_currency": "SGD",
                    "exchange_rate": "0.3023089000",
                    "exchange_rate_id": 94376,
                    "cod_service_available": false,
                    "cod_service_min_cod_amount": "",
                    "cod_service_max_cod_amount": "",
                    "cod_charges_conditions": ""
                },
                {
                    "service_id": "EP-CS0IW",
                    "service_id2": 120,
                    "service_name": "DHLeC (Drop-Off)",
                    "courier_id": "EP-CR0AW",
                    "courier_name": "DHL eCommerce",
                    "courier_uuid": "db129869-d2cd-474a-b3bf-9995a436ef85",
                    "courier_image_fullpath": "https://s3-ap-southeast-1.amazonaws.com/easyparcel-static/Public/source/general/img/couriers/DHLeC.jpg",
                    "courier_logo_fullpath": "https://s3-ap-southeast-1.amazonaws.com/easyparcel-static/Public/source/general/img/couriers/dhllogo.jpg",
                    "delivery_duration": null,
                    "price": "2.03",
                    "price_currency": "SGD",
                    "exchange_rate": "0.3023089000",
                    "exchange_rate_id": 94376,
                    "cod_service_available": false,
                    "cod_service_min_cod_amount": "",
                    "cod_service_max_cod_amount": "",
                    "cod_charges_conditions": ""
                },
                {
                    "service_id": "EP-CS0I6",
                    "service_id2": 132,
                    "service_name": "J&T Express (Pick Up with min 3 parcel(s))",
                    "courier_id": "EP-CR0AL",
                    "courier_name": "J&T Express (Malaysia) Sdn. Bhd.",
                    "courier_uuid": "09e87a98-4eef-4d11-8eff-d8d9c656f993",
                    "courier_image_fullpath": "https://s3-ap-southeast-1.amazonaws.com/easyparcel-static/Public/source/general/img/couriers/J&T_Express.jpg",
                    "courier_logo_fullpath": "https://s3-ap-southeast-1.amazonaws.com/easyparcel-static/Public/source/general/img/couriers/",
                    "delivery_duration": null,
                    "price": "2.05",
                    "price_currency": "SGD",
                    "exchange_rate": "0.3023089000",
                    "exchange_rate_id": 94376,
                    "cod_service_available": false,
                    "cod_service_min_cod_amount": "",
                    "cod_service_max_cod_amount": "",
                    "cod_charges_conditions": ""
                },
                {
                    "service_id": "EP-CS0IO",
                    "service_id2": 133,
                    "service_name": "J&T Express (Drop-Off)",
                    "courier_id": "EP-CR0AL",
                    "courier_name": "J&T Express (Malaysia) Sdn. Bhd.",
                    "courier_uuid": "09e87a98-4eef-4d11-8eff-d8d9c656f993",
                    "courier_image_fullpath": "https://s3-ap-southeast-1.amazonaws.com/easyparcel-static/Public/source/general/img/couriers/J&T_Express.jpg",
                    "courier_logo_fullpath": "https://s3-ap-southeast-1.amazonaws.com/easyparcel-static/Public/source/general/img/couriers/",
                    "delivery_duration": null,
                    "price": "2.05",
                    "price_currency": "SGD",
                    "exchange_rate": "0.3023089000",
                    "exchange_rate_id": 94376,
                    "cod_service_available": false,
                    "cod_service_min_cod_amount": "",
                    "cod_service_max_cod_amount": "",
                    "cod_charges_conditions": ""
                },
                {
                    "service_id": "EP-CS0IH",
                    "service_id2": 134,
                    "service_name": "Flash Express (Pick Up)",
                    "courier_id": "EP-CR0D0",
                    "courier_name": "Flash Malaysia Express Sdn. Bhd.",
                    "courier_uuid": "14d39386-d07a-4eb6-a488-2442d6f8fc07",
                    "courier_image_fullpath": "https://s3-ap-southeast-1.amazonaws.com/easyparcel-static/Public/source/general/img/couriers/Flash_Express.jpg",
                    "courier_logo_fullpath": "https://s3-ap-southeast-1.amazonaws.com/easyparcel-static/Public/source/general/img/couriers/",
                    "delivery_duration": null,
                    "price": "1.99",
                    "price_currency": "SGD",
                    "exchange_rate": "0.3023089000",
                    "exchange_rate_id": 94376,
                    "cod_service_available": false,
                    "cod_service_min_cod_amount": "",
                    "cod_service_max_cod_amount": "",
                    "cod_charges_conditions": ""
                },
                {
                    "service_id": "EP-CS0IV",
                    "service_id2": 136,
                    "service_name": "J&T Cargo (Pick Up)",
                    "courier_id": "EP-CR0DI",
                    "courier_name": "J&T Cargo (M) Sdn. Bhd.",
                    "courier_uuid": "f423bdac-4a35-4f55-934b-62b6bf26e78f",
                    "courier_image_fullpath": "https://s3-ap-southeast-1.amazonaws.com/easyparcel-static/Public/source/general/img/couriers/J&T_Cargo.jpg",
                    "courier_logo_fullpath": "https://s3-ap-southeast-1.amazonaws.com/easyparcel-static/Public/source/general/img/couriers/J&T_Cargo.jpg",
                    "delivery_duration": null,
                    "price": "2.30",
                    "price_currency": "SGD",
                    "exchange_rate": "0.3023089000",
                    "exchange_rate_id": 94376,
                    "cod_service_available": false,
                    "cod_service_min_cod_amount": "",
                    "cod_service_max_cod_amount": "",
                    "cod_charges_conditions": ""
                },
                {
                    "service_id": "EP-CS0IJ",
                    "service_id2": 137,
                    "service_name": "J&T Cargo (Drop-Off)",
                    "courier_id": "EP-CR0DI",
                    "courier_name": "J&T Cargo (M) Sdn. Bhd.",
                    "courier_uuid": "f423bdac-4a35-4f55-934b-62b6bf26e78f",
                    "courier_image_fullpath": "https://s3-ap-southeast-1.amazonaws.com/easyparcel-static/Public/source/general/img/couriers/J&T_Cargo.jpg",
                    "courier_logo_fullpath": "https://s3-ap-southeast-1.amazonaws.com/easyparcel-static/Public/source/general/img/couriers/J&T_Cargo.jpg",
                    "delivery_duration": null,
                    "price": "2.30",
                    "price_currency": "SGD",
                    "exchange_rate": "0.3023089000",
                    "exchange_rate_id": 94376,
                    "cod_service_available": false,
                    "cod_service_min_cod_amount": "",
                    "cod_service_max_cod_amount": "",
                    "cod_charges_conditions": ""
                },
                {
                    "service_id": "EP-CS0IT",
                    "service_id2": 138,
                    "service_name": "Best Express (Pick Up)",
                    "courier_id": "EP-CR0DF",
                    "courier_name": "Best Global Logistics Technology (Malaysia) Sdn. Bhd.",
                    "courier_uuid": "5e4ddd66-80f0-4a8c-a40c-6c029a015d86",
                    "courier_image_fullpath": "https://s3-ap-southeast-1.amazonaws.com/easyparcel-static/Public/source/general/img/couriers/Best_Express.jpg",
                    "courier_logo_fullpath": "https://s3-ap-southeast-1.amazonaws.com/easyparcel-static/Public/source/general/img/couriers/",
                    "delivery_duration": null,
                    "price": "2.26",
                    "price_currency": "SGD",
                    "exchange_rate": "0.3023089000",
                    "exchange_rate_id": 94376,
                    "cod_service_available": false,
                    "cod_service_min_cod_amount": "",
                    "cod_service_max_cod_amount": "",
                    "cod_charges_conditions": ""
                }
            ]
        }
    ]
}
```
</details>

---
<br>

### Get Insurance Quotation:
Get Insurance Quotation: This features enables users to check the insurance quotations from specific courier companies on the EasyParcel platform. Users are required to fill in the necessary fields to access the insurance rate information.

<details id="Request"> 
  <summary><h5>Request:</h5></summary> 
 
##### Request

L1

| Requested Parameters | Type        | Required | Description                                                      |
| -------------------- | ----------- | -------- | ---------------------------------------------------------------- |
| courier_id           | string(25)  | Yes      | Courier Identification number                                    |
| items                | array       | Yes      | Items to ship (refer to [items](#items))                         |
| currency_code        | string (3)  | Yes      | Country's currency                                               |
| shipment_weight      | double(8,2) | Yes      | Weight of the parcel                                             |
| shipment_width       | double(8,2) | Optional | Width of the parcel                                              |
| shipment_length      | double(8,2) | Optional | Length of the parcel                                             |
| shipment_height      | double(8,2) | Optional | Height of the parcel                                             |
| coll_postcode        | string(10)  | Yes      | Sender's post code                                               |
| coll_province_code   | string(35)  | Yes      | Sender's province code                                           |
| coll_country_code    | string(2)   | Yes      | Sender's country code (refer to [country code](#country-code))   |
| deli_postcode        | string(10)  | Yes      | Receiver's post code                                             |
| deli_province_code   | string(35)  | Yes      | Receiver's province code                                         |
| deli_country_code    | string(2)   | Yes      | Receiver's country code (refer to [country code](#country-code)) |
L2
###### Items

| Requested Parameters | Type     | Required | Description          |
| -------------------- | -------- | -------- | -------------------- |
| quantity             | int (10) | Yes      | Quantity of the item |
| value                | double   | Yes      | value of the item    |
Sample Code:
```
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => 'http://localhost:8023/open_api/shipment/insurance_quotations',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS =>'{

  "list": [
    {
      "courier_id": "EP-CR05",
      "items": [
        {
          "quantity": 2,
          "value": 100.50
        },
        {
          "quantity": 1,
          "value": 50.25
        }
      ],
      "currency_code": "MYR",
      "shipment_weight": 1.5,
      "shipment_length": 100,
      "shipment_width": 100,
      "shipment_height": 100,
      "coll_postcode": "11900",
      "coll_province_code": "MY-07",
      "coll_country_code": "MY",
      "deli_postcode": "11900",
      "deli_province_code": "MY-07",
      "deli_country_code": "MY"
    },
    {
      "courier_id": "EP-CR0A",
      "items": [
        {
          "quantity": 5,
          "value": 75.00
        }
      ],
      "currency_code": "MYR",
      "shipment_weight": 0.8,
      "shipment_length": 100,
      "shipment_width": 100,
      "shipment_height": 100,
      "coll_postcode": "11900",
      "coll_province_code": "MY-07",
      "coll_country_code": "MY",
      "deli_postcode": "11900",
      "deli_province_code": "MY-07",
      "deli_country_code": "MY"
    }
  ]
}',
  CURLOPT_HTTPHEADER => array(
    'Content-Type: application/json'
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;

```
</details>

<details id="Respond"> 
  <summary><h5>Respond:</h5></summary> 
 
##### Respond

Returned parameters

L1

| Returned Parameters  | Type       | Description                                                      |
| -------------------- | ---------- | ---------------------------------------------------------------- |
| currency_code        | string(25) | Courier Identification number                                    |
| shipment_weight      | double     | Weight of the parcel                                             |
| shipment_length      | double     | Length of the parcel                                             |
| shipment_width       | double     | Width of the parcel                                              |
| shipment_height      | double     | Height of the parcel                                             |
| coll_postcode        | string     | Sender's postcode                                                |
| coll_province_code   | string     | Sender's province code (refer to [ISO_3166](#iso3166))           |
| coll_country_code    | string     | Sender's country code (refer to [country code](#country-code))   |
| deli_postcode        | string     | Receiver's postcode                                              |
| deli_province_code   | string     | Receiver's province code (refer to [ISO_3166](#iso3166))         |
| deli_country_code    | string     | Receiver's country code (refer to [country code](#country-code)) |
| insurance_quotations | array      | (refer to [insurance_quotations](#insurance_quotations))         |

L2
###### insurance_quotations

| Returned Parameters | Type   | Description                                                               |
| ------------------- | ------ | ------------------------------------------------------------------------- |
| quantity            | int    | Courier Identification number                                             |
| value               | double | value of the insurance                                                    |
| insurance_list      | array  | List of available insurances (refer to [insurance_list](#insurance_list)) |

L3
###### insurance_list

| Returned Parameters   | Type   | Description                                    |
| --------------------- | ------ | ---------------------------------------------- |
| id                    | string | Unique id of the insurance quotation           |
| insurance_provider_id | string | Insurance provider unique id                   |
| supported_currency    | string | Supported currency for the insurance           |
| name                  | string | Name of the insurance provider                 |
| description           | string | Description on the insurance coverage          |
| rate                  | array  | Rate of the insurance (refer to [rate](#rate)) |
| price                 | double | Rrice of the insurance coverage                |

L4
###### rate

| Returned Parameters | Type   | Description                                              |
| ------------------- | ------ | -------------------------------------------------------- |
| max                 | double | Maximum charge or cost for the insurance service.        |
| min                 | double | Minimum charge or cost for the insurance service.        |
| rate                | double | Rate applied to the value of the insured parcel.         |
| max_coverage        | double | Maximum coverage amount that the insurance will provide. |

Respond Sample:
```
{
    "status_code": 200,
    "message": "Success",
    "data": [
        {
            "currency_code": "MYR",
            "shipment_weight": 1.5,
            "shipment_length": 100,
            "shipment_width": 100,
            "shipment_height": 100,
            "coll_postcode": "11900",
            "coll_province_code": "MY-07",
            "coll_country_code": "MY",
            "deli_postcode": "11900",
            "deli_province_code": "MY-07",
            "deli_country_code": "MY",
            "insurance_quotations": [
                {
                    "quantity": 2,
                    "value": 100.5,
                    "insurance_list": [
                        {
                            "id": 22,
                            "insurance_provider_id": 21,
                            "supported_currency": "MYR",
                            "name": "insurance test 15-1",
                            "description": "",
                            "rate": {
                                "max": 10,
                                "min": 10,
                                "rate": 0.2,
                                "max_coverage": 1000
                            },
                            "price": 10
                        },
                        {
                            "id": 23,
                            "insurance_provider_id": 21,
                            "supported_currency": "MYR",
                            "name": "insurance test 15",
                            "description": "",
                            "rate": {
                                "max": 5,
                                "min": 5,
                                "rate": 1,
                                "max_coverage": 1000
                            },
                            "price": 5
                        }
                    ]
                },
                {
                    "quantity": 1,
                    "value": 50.25,
                    "insurance_list": [
                        {
                            "id": 22,
                            "insurance_provider_id": 21,
                            "supported_currency": "MYR",
                            "name": "insurance test 15-1",
                            "description": "",
                            "rate": {
                                "max": 10,
                                "min": 10,
                                "rate": 0.2,
                                "max_coverage": 1000
                            },
                            "price": 10
                        },
                        {
                            "id": 23,
                            "insurance_provider_id": 21,
                            "supported_currency": "MYR",
                            "name": "insurance test 15",
                            "description": "",
                            "rate": {
                                "max": 5,
                                "min": 5,
                                "rate": 1,
                                "max_coverage": 1000
                            },
                            "price": 5
                        }
                    ]
                }
            ]
        },
    ]
}
```
</details>

---
<br>

### Get Courier Dropoff point
Get Courier Drop off point: This features enables users to check the available Drop off point for selected courier and zones. Users are required to fill in the necessary fields to access the insurance rate information.

<details id="Request"> 
  <summary><h5>Request:</h5></summary> 
 
##### Request

Parameters used:
L1

| Requested Parameters | Type       | Required | Description                                                           |
| -------------------- | ---------- | -------- | --------------------------------------------------------------------- |
| courier_id           | string(25) | Yes      | Courier identification number                                         |
| country_code         | string(2)  | Yes      | Dropoff point's country code (refer to [country code](#country-code)) |
| postcode             | string(10) | Yes      | Dropoff point's postcode                                              |
| city                 | string(35) | Yes      | Dropoff point's city                                                  |
| state_code           | string(35) | Yes      | Dropoff point's state_code                                            |

Sample Code:
```
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => 'http://localhost:8023/open_api/shipment/get_courier_dropoff_points',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS =>'{
    "courier_id": "EP-CR0A",
    "country_code": "MY",
    "postcode":"09600",
    "city":"Lunas",
    "state_code": "MY-02"
}',
  CURLOPT_HTTPHEADER => array(
    'Content-Type: application/json'
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;

```
</details>

<details id="Respond"> 
  <summary><h5>Respond:</h5></summary> 
 
##### Respond

Returned parameters

L1

| Returned Parameters | Type      | Description                                     |
| ------------------- | --------- | ----------------------------------------------- |
| point_code          | string    | The drop of point code                          |
| name                | string    | Name of the drop of point                       |
| address_1           | string    | Address 1 of the drop of point                  |
| address_2           | string    | Address 2 of the drop of point                  |
| address_3           | string    | Address 3 of the drop of point                  |
| address_4           | string    | Address 4 of the drop of point                  |
| postcode            | string    | Postcode of the drop of point                   |
| city                | string    | City of the drop of point                       |
| state               | string    | State of the drop of point                      |
| phone_number        | string    | Contact number of the drop of point             |
| info                | string    | Additional information of the drop of point     |
| image               | string    | Image path of the drop of point                 |
| start_time          | date/time | Opening time of the location                    |
| end_time            | date/time | Closing time of the location                    |
| latitude            | double    | Latitude of the location of the drop off point  |
| longitude           | double    | Longitude of the location of the drop off point |

Respond Sample:
```
{
    "status_code": 200,
    "message": "",
    "data": [
        {
            "point_code": "Pos Malaysia Lunas",
            "name": "Pos Malaysia Lunas",
            "address_1": "894",
            "address_2": "Taman Sejahtera",
            "address_3": "",
            "address_4": "",
            "postcode": "09600",
            "city": "Lunas",
            "state": "kdh",
            "phone_number": "04-484 4221",
            "info": "",
            "image": null,
            "start_time": "00:00:00",
            "end_time": "00:00:00",
            "latitude": null,
            "longitude": null
        }
    ],
    "rejected": null,
    "last_key": ""
}

```
</details>

---
<br>

### Submit Shipment Orders
Submit Shipment Orders: This features enables users to submit the shipment orders. Users are required to fill in the necessary fields to access the insurance rate information.

<details id="Request"> 
  <summary><h5>Request:</h5></summary> 
 
##### Request
Parameters used:

L1

| Requested Parameters | Type        | Required | Description                                  |
| -------------------- | ----------- | -------- | -------------------------------------------- |
| service_id           | string(10)  | Yes      | Service Identification number                |
| collection_date      | date        | Yes      | Date to collect the parcel                   |
| weight               | double(8,2) | Yes      | Weight of the parcel                         |
| height               | double(8,2) | Yes      | Height of the parcel                         |
| length               | double(8,2) | Yes      | Length of the parcel                         |
| width                | double(8,2) | Yes      | Width of the parcel                          |
| item                 | array       | Yes      | Item of the parcel (refer to [item](#items)) |

###### Origin

| Requested Parameters      | Type      | Required | Description                                        |
| ------------------------- | --------- | -------- | -------------------------------------------------- |
| name                      | string    | Yes      | Sender's Name                                      |
| company                   | string    | Yes      | Sender's Company                                   |
| phone_number_country_code | string    | Yes      | (refer to [country code](#country-code))           |
| phone_number              | string    | Yes      | Sender's phone number                              |
| email                     | string    | Yes      | Sender's email                                     |
| address_1                 | string    | Yes      | Sender's address                                   |
| address_2                 | string    | Yes      | Sender's address                                   |
| postcode                  | string    | Yes      | Sender's postcode                                  |
| town                      | string    | Yes      | Sender's town area                                 |
| province_code             | string    | Yes      | Sender's province (refer to [ISO- 3166](#iso3166)) |
| country_code              | string(2) | Yes      | (refer to [country code](#country-code))           |

###### Destination

| Requested Parameters      | Type      | Required | Description                                                                 |
| ------------------------- | --------- | -------- | --------------------------------------------------------------------------- |
| name                      | string    | Yes      | Name of the Receiver                                                        |
| company                   | string    | Yes      | Receiver's Company                                                          |
| phone_number_country_code | string    | Yes      | (refer to [country code](#country-code))                                    |
| phone_number              | string    | Yes      | Receiver's phone number                                                     |
| email                     | string    | Yes      | Receiver's email                                                            |
| address_1                 | string    | Yes      | Receiver's address                                                          |
| address_2                 | string    | Yes      | Receiver's address                                                          |
| postcode                  | string    | Yes      | Receiver's postcode                                                         |
| town                      | string    | Yes      | Receiver's town area                                                        |
| province_code             | string    | Yes      | Receiver's province (refer to [ISO- 3166](#iso3166))                        |
| country_code              | string(2) | Yes      | Receiver's country code(refer to [country code](#country-code))             |
| Notification              | array     | Yes      | Notifications of the parcel status (refer to [Notification](#Notification)) |


---
<br>

###### Airways Bills Branding

| Requested Parameters | Type    | Required | Description                                 |
| -------------------- | ------- | -------- | ------------------------------------------- |
| enable               | boolean | Yes      | To enable or disable Airways Bills Branding |


L2
###### Items

| Requested Parameters | Type        | Required | Description                                                                      |
| -------------------- | ----------- | -------- | -------------------------------------------------------------------------------- |
| content              | string      | Yes      | Description of the content                                                       |
| currency_code        | string (3)  | Yes      | The currency code of the parcel content.                                         |
| value                | double(8,2) | Yes      | Value of the parcel                                                              |
| quantity             | int         | Yes      | The parcel quantity                                                              |
| Insurance_purchase   | array       | Yes      | Purchased Insurance details (refer to [insurance purchase](#Insurance-purchase)) |

###### Notification

| Requested Parameters | Type    | Required | Description                                              |
| -------------------- | ------- | -------- | -------------------------------------------------------- |
| sms                  | boolean | Yes      | To enable or disable sms notification of the parcel      |
| email                | boolean | Yes      | To enable or disable email notification of the parcel    |
| whatsapp             | boolean | Yes      | To enable or disable whatsapp notification of the parcel |



L3
###### Insurance purchase
| Requested Parameters | Type   | Required | Description              |
| -------------------- | ------ | -------- | ------------------------ |
| insurance_service_id | string | Yes      | insurance service number |
| invoices             | string | Yes      | links to the invoices    |
| photos               | string | Yes      | Image location           |

Sample code:
```
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => 'https://developer.easyparcel.com/open_api/shipment/submit_orders',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS =>'{
  "list": [
    {
      "service_id": "EP-CS0IW",
      "collection_date": "2024-10-22",
       "weight": 0.5,
        "height": 10,
        "length": 10,
        "width": 10,
      "item": [
        {
          "content": "Electronics",
          "weight": 0.5,
          "height": 100,
          "length": 100,
          "width": 100,
          "currency_code": "MYR",
          "value": 200,
          "quantity": 1,
          "insurance_purchase":{
                "insurance_service_id":23,
                "invoices": "https://ep-website-media.s3.ap-southeast-1.amazonaws.com/my/wp-content/uploads/2024/02/sf-express-exd.webp",
                "photos": "https://s3-ap-southeast-1.amazonaws.com/easyparcel/Public/source/general/img/couriers/DHLeC.jpg"
            }
        },
        {
          "content": "Electronics 2",
          "weight": 0.7,
          "height": 120,
          "length": 100,
          "width": 100,
          "currency_code": "MYR",
          "value": 500,
          "quantity": 1,
          "insurance_purchase":{
                "insurance_service_id":23,
                "invoices": "https://ep-website-media.s3.ap-southeast-1.amazonaws.com/my/wp-content/uploads/2024/02/sf-express-exd.webp"
            }
        }

      ],
      
      "origin": {
        "name": "John Doe",
        "company": "ABC Corp",
        "phone_number_country_code": "+60",
        "phone_number": "1163642281",
        "email": "sample@easyparcel.com",
        "address_1": "123 Main St",
        "address_2": "Apt 4B",
        "postcode": "11900",
        "town": "Lunas",
        "province_code": "MY-07",
        "country_code": "MY"
      },
      "destination": {
        "name": "Jane Smith",
        "company": "XYZ Inc",
        "phone_number_country_code": "+60",
        "phone_number": "1163642281",
        "email": "sample@easyparcel.com",
        "address_1": "456 High St",
        "address_2": "Floor 2",
        "postcode": "11900",
        "town": "Bayan Lepas",
        "province_code": "MY-07",
        "country_code": "MY",
        "notification": {
          "sms": {
            "enable": true
          },
          "email": {
            "enable": true
          },
          "whatsapp": {
            "enable": true
          }
        }
      },
      "awb_branding": {
        "enable": true
      }
   
    }
  ]
}',
  CURLOPT_HTTPHEADER => array(
    'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJhcHAiOnsiY2xpZW50X2lkIjoiNjU3MzEyOTYtMzkzZi00MmJjLTllNTktY2E5NjcyYmViNmY2In0sInVzZXIiOnsiaWQiOiI0ZTAyMTA1YzQ2NmNmYzg4Y2U4MmQ2NTEwMGI0YzBhZEptbnJDT1hSNmV6UHRtSFUyWkNyYmc9PSIsImVhc3lfYWNjb3VudF9pZCI6IjA5ZjcxMjc5LTBjMGItNDcxOS05OTM5LWMwMzVjYWVlYzYxOSIsImFjY291bnRfaWQiOiI4NzIwNjYwIn0sImlhdCI6MTczMTg5OTM0MCwiaXNzIjoiZWFzeXBhcmNlbCIsImF1ZCI6ImVhc3lwYXJjZWwiLCJleHAiOjE3MzE5MzUzNDB9.S2yUdWfzIPZETtQhvc9dRmtVq8Wz_HBNDU5N-VJFblU',
    'Content-Type: application/json'
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;

```
</details>


<details id="Respond"> 
  <summary><h5>Respond:</h5></summary> 
 
##### Respond

Returned parameters

L1

| Returned Parameters        | Type       | Description                                                                                                    |
| -------------------------- | ---------- | -------------------------------------------------------------------------------------------------------------- |
| app_uuid                   | string(25) | Courier identification number                                                                                  |
| order_number               | string     | Order number of the Shipment                                                                                   |
| currency_code              | string     | Currency used for the shipment                                                                                 |
| total_amount               | double     | total cost of the shipment                                                                                     |
| credit_applied             | double     | credit applied on the shipment                                                                                 |
| free_credit_applied        | double     | free credit applied on the shipment                                                                            |
| tax_amount                 | double     | tax amount on the shipment                                                                                     |
| account_id                 | string     | account id used for the shipment                                                                               |
| shipments                  | array      | Shipments details (refer to [shipment](#shipments))                                                            |
| shipment_tracking_whatsapp | array      | Shipment notification details on whatsapp (refer to [shipment_tracking_whatsapp](#shipment_tracking_whatsapp)) |
| shipment_tracking_sms      | array      | Shipment notification details on sms                                                                           |
| shipment_tracking_email    | array      | Shipment notification details on email                                                                         |

L2

###### shipments

| Returned Parameters                          | Type       | Description                                                         |
| -------------------------------------------- | ---------- | ------------------------------------------------------------------- |
| uuid                                         | string(25) | Uuid of the shipment                                                |
| courier_service                              | string     | The courier service and type selected for the shipment              |
| courier                                      | string     | Name of the courier service                                         |
| currency_code                                | string     | Currency use for the shipment                                       |
| total_amount                                 | double     | The shipment amount / price of this particular shipments            |
| credit_applied                               | double     | Credit applied for this particular shipment                         |
| free_credit_applied                          | double     | Free credit applied for this particular shipment                    |
| shipment_price                               | double     | Price of this particular shipment                                   |
| tax_amount                                   | double     | Tax amount of this particular shipment                              |
| collection_date                              | date       | Collection date of the parcel                                       |
| tracking_status                              | int        | The tracking status of the parcel ()                                |
| awb_url                                      | string     | The url to access the airway bill                                   |
| awb_number                                   | string     | The airway bill number                                              |
| tracking_url                                 | string     | The url to tracking the parcel                                      |
| shipment_number                              | string     | The unique number of the shipment                                   |
| sender_point_code                            | string     |                                                                     |
| sender_name                                  | string     | Name of the sender                                                  |
| sender_phone_number_country_code             | string     | The country code of the phone of the sender                         |
| sender_phone_number                          | string     | Phone number of the sender                                          |
| sender_alternate_phone_number                | string     | Alternate phone number of the sender                                |
| sender_alternate_phone_number_country_code   | string     | Alternate the country code of the phone of the sender               |
| sender_email                                 | string     | Sender's Email                                                      |
| sender_company_name                          | string     | Sender's Company Name                                               |
| sender_address1                              | string     | Sender's Address 1                                                  |
| sender_address2                              | string     | Sender's Address 2                                                  |
| sender_city                                  | string     | Sender's city                                                       |
| sender_province_code                         | string     | Sender's province (refer to [ISO_3166](#iso3166))                   |
| sender_postcode                              | string     | Sender's post code                                                  |
| sender_country_code                          | string     | Sender's country code (refer to [country code](#country-code))      |
| receiver_point_code                          | string     |                                                                     |
| receiver_name                                | string     | Name of the receiver                                                |
| receiver_phone_number_country_code           | string     | The country code of the phone of the receiver                       |
| receiver_phone_number                        | string     | Phone number of the receiver                                        |
| receiver_alternate_phone_number              | string     | Alternate phone number of the receiver                              |
| receiver_alternate_phone_number_country_code | string     | Alternate the country code of the phone of the receiver             |
| receiver_email                               | string     | Receiver's Email                                                    |
| receiver_company_name                        | string     | Receiver's Company Name                                             |
| receiver_address1                            | string     | Receiver's Address 1                                                |
| receiver_address2                            | string     | Receiver's Address 2                                                |
| receiver_city                                | string     | Receiver's city                                                     |
| receiver_province_code                       | string     | Sender's province (refer to [ISO_3166](#iso3166))                   |
| receiver_postcode                            | string     | Sender's post code                                                  |
| receiver_country_code                        | string     | Sender's country code (refer to [country code](#country-code))      |
| cod                                          | string     | Cash on delivery status                                             |
| weight                                       | double     | Weight of the  shipment                                             |
| height                                       | double     | Height of the shipment parcels                                      |
| lenght                                       | double     | Lenght of the particular shipment                                   |
| width                                        | double     | Width of the particular shipment                                    |
| shipment_items                               | array      | Shipments items details (refer to [shipment items](#shipment-items) |


###### shipment_tracking_whatsapp
| Returned Parameters | Type   | Description                                                       |
| ------------------- | ------ | ----------------------------------------------------------------- |
| message             | string | Notifications message sent to whatsapp                            |
| total_amount        | double | Total amount of the shipment                                      |
| credit_applied      | double | Credit applied on the shipment                                    |
| free_credit_applied | double | Free credit applied on the shipment                               |
| price               | double | Price of the shipment                                             |
| tax_amount          | double | tax amount on the shipment                                        |
| currency_code       | string | currency used for the shipment                                    |
| phone_country_code  | string | country code for the phone of the whatsapp notifications receiver |
| phone_number        | string | Phone number of the whatsapp notifications receiver               |
| status              | string | status of whatsapp notifications                                  |
| email               | string | email of the whatsapp notifications receiver                      |

###### shipment_tracking_sms
| Returned Parameters | Type   | Description                                                  |
| ------------------- | ------ | ------------------------------------------------------------ |
| message             | string | Notifications message sent to sms                            |
| total_amount        | double | Total amount of the shipment                                 |
| credit_applied      | double | Credit applied on the shipment                               |
| free_credit_applied | double | Free credit applied on the shipment                          |
| price               | double | Price of the shipment                                        |
| tax_amount          | double | tax amount on the shipment                                   |
| currency_code       | string | currency used for the shipment                               |
| phone_country_code  | string | country code for the phone of the sms notifications receiver |
| phone_number        | string | Phone number of the sms notifications receiver               |
| status              | string | status of sms notifications                                  |
| email               | string | email of the sms notifications receiver                      |

###### shipment_tracking_email

| Returned Parameters | Type   | Description                                                    |
| ------------------- | ------ | -------------------------------------------------------------- |
| message             | string | Notifications message sent to email                            |
| total_amount        | double | Total amount of the shipment                                   |
| credit_applied      | double | Credit applied on the shipment                                 |
| free_credit_applied | double | Free credit applied on the shipment                            |
| price               | double | Price of the shipment                                          |
| tax_amount          | double | tax amount on the shipment                                     |
| currency_code       | string | currency used for the shipment                                 |
| phone_country_code  | string | country code for the phone of the email notifications receiver |
| phone_number        | string | Phone number of the email notifications receiver               |
| status              | string | status of email notifications                                  |
| email               | string | email of the email notifications receiver                      |


L3
###### shipment items
| Requested Parameters | Type       | Description                            |
| -------------------- | ---------- | -------------------------------------- |
| content              | string(25) | Uuid of the shipment                   |
| weight               | double     | Weight of the item                     |
| height               | double     | Height of the item                     |
| length               | double     | Length of the item                     |
| width                | double     | Width of the item                      |
| currency_code        | string     | Currency use for the value of the item |
| value                | double     | Value of the item                      |
| quantity             | int        | Quantity of the item                   |

Respond Sample:
```
{
    "status_code": 200,
    "message": "Order Successfully Placed",
    "data": [
        {
            "app_uuid": "45689cd5-1da0-47e1-b5ff-81b15db54bd2",
            "order_number": "EI-2410-4Z26C",
            "currency_code": "MYR",
            "total_amount": "13.50",
            "credit_applied": "10.50",
            "free_credit_applied": "3.00",
            "tax_amount": "0.67",
            "account_id": 438368,
            "shipments": [
                {
                    "uuid": "0226e5e7-19cb-464d-9455-2099dc11b3b1",
                    "courier_service": "DHLeC (Drop-Off)",
                    "courier": "DHL eCommerce",
                    "currency_code": "MYR",
                    "total_amount": "6.32",
                    "credit_applied": "4.91",
                    "free_credit_applied": "1.41",
                    "shipment_price": "6.04",
                    "tax_amount": "0.28",
                    "collection_date": "2024-10-02",
                    "tracking_status": 7,
                    "awb_url": "https://s3-ap-southeast-1.amazonaws.com/easyparcel/Public/courier/consignment_note/9fceafc2-3ef9-4c8a-af99-59f6ed17f08a.pdf",
                    "awb_number": "MYAIAEPYNS",
                    "tracking_url": "https://easyparcel.rocks/tools/easytrack/summary?awb=MYAIAEPYNS",
                    "shipment_number": "ES-2410-UTGQV",
                    "sender_point_code": null,
                    "sender_name": "John Doe",
                    "sender_phone_number_country_code": "+60",
                    "sender_phone_number": "1163642281",
                    "sender_alternate_phone_number": null,
                    "sender_alternate_phone_number_country_code": null,
                    "sender_email": "sample@easyparcel.com",
                    "sender_company_name": "ABC Corp",
                    "sender_address1": "123 Main St",
                    "sender_address2": "Apt 4B",
                    "sender_city": "Lunas",
                    "sender_province_code": "MY-02",
                    "sender_postcode": "09600",
                    "sender_country_code": "MY",
                    "receiver_point_code": null,
                    "receiver_name": "Jane Smith",
                    "receiver_phone_number": "1163642281",
                    "receiver_phone_number_country_code": "+60",
                    "receiver_alternate_phone_number": null,
                    "receiver_alternate_phone_number_country_code": null,
                    "receiver_email": "sample@easyparcel.com",
                    "receiver_company_name": "XYZ Inc",
                    "receiver_address1": "456 High St",
                    "receiver_address2": "Apt 4B",
                    "receiver_city": "Bayan Lepas",
                    "receiver_province_code": "MY-07",
                    "receiver_postcode": "11950",
                    "receiver_country_code": "MY",
                    "cod": null,
                    "weight": 2.5,
                    "height": 30,
                    "length": 40,
                    "width": 20,
                    "shipment_items": [
                        {
                            "content": "Electronics",
                            "weight": 0.5,
                            "height": 30,
                            "length": 40,
                            "width": 20,
                            "currency_code": "MYR",
                            "value": 500,
                            "quantity": 1
                        },
                        {
                            "content": "Electronics 2",
                            "weight": 0.5,
                            "height": 10,
                            "length": 20,
                            "width": 20,
                            "currency_code": "MYR",
                            "value": 50,
                            "quantity": 2
                        }
                    ],
                    "shipment_tracking_whatsapp": null,
                    "shipment_tracking_sms": {
                        "message": "Your order from John Doe is ready & trackable once courier scans in. Track at EasyParcel with MYAIAEPYNS -Powered by EasyParcel",
                        "total_amount": "0.23",
                        "credit_applied": "0.18",
                        "free_credit_applied": "0.05",
                        "price": "0.20",
                        "tax_amount": "0.03",
                        "currency_code": "MYR",
                        "phone_country_code": "+60",
                        "phone_number": "1163642281",
                        "status": "SUCCESS",
                        "email": null
                    },
                    "shipment_tracking_email": {
                        "message": null,
                        "total_amount": "0.06",
                        "credit_applied": "0.05",
                        "free_credit_applied": "0.01",
                        "price": "0.05",
                        "tax_amount": "0.01",
                        "currency_code": "MYR",
                        "phone_country_code": null,
                        "phone_number": null,
                        "status": "SUCCESS",
                        "email": "sample@easyparcel.com"
                    }
                },
                {
                    "uuid": "a9200d3e-c697-4481-a85f-1b6b0d2af077",
                    "courier_service": "DHLeC (Drop-Off)",
                    "courier": "DHL eCommerce",
                    "currency_code": "MYR",
                    "total_amount": "6.32",
                    "credit_applied": "4.91",
                    "free_credit_applied": "1.41",
                    "shipment_price": "6.04",
                    "tax_amount": "0.28",
                    "collection_date": "2024-10-03",
                    "tracking_status": 7,
                    "awb_url": null,
                    "awb_number": null,
                    "tracking_url": null,
                    "shipment_number": "ES-2410-SGU6P",
                    "sender_point_code": null,
                    "sender_name": "JWK 1",
                    "sender_phone_number_country_code": "+60",
                    "sender_phone_number": "1163642281",
                    "sender_alternate_phone_number": null,
                    "sender_alternate_phone_number_country_code": null,
                    "sender_email": "sample@easyparcel.com",
                    "sender_company_name": "ABC Corp",
                    "sender_address1": "123 Main St",
                    "sender_address2": "Apt 4B",
                    "sender_city": "Bayan Baru",
                    "sender_province_code": "MY-07",
                    "sender_postcode": "11950",
                    "sender_country_code": "MY",
                    "receiver_point_code": null,
                    "receiver_name": "WK 2",
                    "receiver_phone_number": "1163642281",
                    "receiver_phone_number_country_code": "+60",
                    "receiver_alternate_phone_number": null,
                    "receiver_alternate_phone_number_country_code": null,
                    "receiver_email": "sample@easyparcel.com",
                    "receiver_company_name": "XYZ Inc",
                    "receiver_address1": "456 High St",
                    "receiver_address2": "Apt 4B",
                    "receiver_city": "Lunas",
                    "receiver_province_code": "MY-02",
                    "receiver_postcode": "09600",
                    "receiver_country_code": "MY",
                    "cod": null,
                    "weight": 0.5,
                    "height": 30,
                    "length": 40,
                    "width": 20,
                    "shipment_items": [
                        {
                            "content": "test",
                            "weight": 0.5,
                            "height": 30,
                            "length": 40,
                            "width": 20,
                            "currency_code": "MYR",
                            "value": 200,
                            "quantity": 1
                        }
                    ],
                    "shipment_tracking_whatsapp": {
                        "message": "Hey there! Your order from JWK 1 is ready to be collected for delivery soon!\n\nTracking no: null",
                        "total_amount": "0.28",
                        "credit_applied": "0.22",
                        "free_credit_applied": "0.06",
                        "price": "0.25",
                        "tax_amount": "0.03",
                        "currency_code": "MYR",
                        "phone_country_code": "+60",
                        "phone_number": "1163642281",
                        "status": "Whatsapp service not available at the moment",
                        "email": null
                    },
                    "shipment_tracking_sms": {
                        "message": "Your order from JWK 1 is ready & trackable once courier scans in. Track at EasyParcel with [Placeholder Trackin..] -Powered by EasyParcel",
                        "total_amount": "0.23",
                        "credit_applied": "0.18",
                        "free_credit_applied": "0.05",
                        "price": "0.20",
                        "tax_amount": "0.03",
                        "currency_code": "MYR",
                        "phone_country_code": "+60",
                        "phone_number": "1163642281",
                        "status": "SUCCESS",
                        "email": null
                    },
                    "shipment_tracking_email": {
                        "message": null,
                        "total_amount": "0.06",
                        "credit_applied": "0.05",
                        "free_credit_applied": "0.01",
                        "price": "0.05",
                        "tax_amount": "0.01",
                        "currency_code": "MYR",
                        "phone_country_code": null,
                        "phone_number": null,
                        "status": "SUCCESS",
                        "email": "sample@easyparcel.com"
                    }
                }
            ]
        }
    ],
    "rejected": null,
    "last_key": ""
}
```
</details>

---
<br>

### Get OnDemand Quotation
Get OnDemand Quotation: This feature enables users to obtain OnDemand Shipment quotations from all courier companies available on the EasyParcel platform. Users need to provide sender and receiver addresses to check the shipment quotation.

<details id="Request"> 
  <summary><h5>Request:</h5></summary> 


##### Request 
Parameter used:
L1

| Requested Parameters | Type   | Required | Description                            |
| -------------------- | ------ | -------- | -------------------------------------- |
| schedule_pickup_date | date   | Yes      | Date to pickup the parcel              |
| schedule_pickup_time | time   | Yes      | Time to pickup the parcel              |
| timezone             | string | Yes      | TimeZone of the location of the parcel |
L2
###### waypoint_list

| Requested Parameters | Type   | Required | Description                                                      |
| -------------------- | ------ | -------- | ---------------------------------------------------------------- |
| coordinates          | array  | yes      | coordinates of the parcel (refer to [coordinates](#coordinates)) |
| address              | string | yes      | Address of the parcel                                            |
| type                 | string | yes      | pickup type                                                      |

L3
###### coordinates

| Requested Parameters | Type   | Required | Description             |
| -------------------- | ------ | -------- | ----------------------- |
| latitude             | double | Yes      | latitude of the parcel  |
| longitude            | double | Yes      | longitude of the parcel |


Sample Code:
```
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => 'http://localhost:8023/open_api/ondemand/quotation',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS =>'{
    "schedule_pickup_date": "2024-11-30",
    "schedule_pickup_time": "11:48:35",
    "timezone": "Asia/Kuala_Lumpur",
    "waypoint_list": [
        {
            "coordinates": {
                "latitude": 5.342720241204454,
                "longitude": 100.28204988381822
            },
            "address": "Kawasan Mendaki Bukit Jambul, Lintang Bukit Jambul 1, Bukit Jambul Indah, Bayan Lepas, Mukim 13 Paya Terubong, 11900, Timur Laut, Pulau Pinang, Malaysia",
            "type": "pickup"
        },
        {
            "coordinates": {
                "latitude": 5.325513957,
                "longitude": 100.2862732
            },
            "address": "Suntech @ Penang Cybercity, 1, Lintang Mayang Pasir 3, Bandar Bayan Baru, Bayan Lepas, Mukim 12 Bayan Lepas, 11950, Barat Daya, Pulau Pinang, Malaysia",
            "type": "dropoff"
        }
    ]
}',
  CURLOPT_HTTPHEADER => array(
    'Content-Type: application/json'
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;

```
</details>

<details id="Respond"> 
  <summary><h5>Respond:</h5></summary> 
 
##### Respond

Returned parameters

L1

| Returned Parameters  | Type       | Description                      |
| -------------------- | ---------- | -------------------------------- |
| req_id               | string(25) | Courier identification number    |
| sid                  | string(25) | Shipment id                      |
| short_name           | string(25) | Short name of the courier        |
| courier              | string(25) | Courier name                     |
| img_courier          | string(25) | image path of the courier        |
| transportation_type  | string(25) | type of transportation           |
| transportation       | string(25) | transporation                    |
| durations            | string(25) | duration of the delivery         |
| parcel_type_support: | string     | type of parcel                   |
| payload              | string     | weight of the parcel             |
| dimension            | string     | dimension / size of the parcel   |
| estimate_total       | double     | price of the delivery            |
| currency             | string     | currency used for the price      |
| metadata             | array      | (refer to [metadata](#metadata)) |
L2
###### metadata

| Returned Parameters | Type       | Required | Description                          |
| ------------------- | ---------- | -------- | ------------------------------------ |
| quotationId         | string(25) | Yes      | Unique ID of the Quotation displayed |

Respond Sample:
```
{
    "status_code": 200,
    "message": "",
    "data": [
        {
            "req_id": "19f4161e-f4d7-469a-8b95-a6ba5ca138f4",
            "sid": 3,
            "short_name": "Lalamove",
            "courier": "Lalamove",
            "img_courier": "https://s3-ap-southeast-1.amazonaws.com/easyparcel/Public/source/general/img/couriers/lalamove.svg",
            "transportation_type": "Car",
            "transportation": "-",
            "durations": "7mins",
            "parcel_type_support": "Parcel",
            "payload": "40kg",
            "dimension": "50cmx50cmx50cm",
            "estimate_total": "5.65",
            "currency": "MYR",
            "metadata": {
                "quotationId": "3114850556997669456"
            }
        },
        {
            "req_id": "7729a7b6-2e68-4d9c-9351-249ce3495030",
            "sid": 4,
            "short_name": "Lalamove",
            "courier": "Lalamove",
            "img_courier": "https://s3-ap-southeast-1.amazonaws.com/easyparcel/Public/source/general/img/couriers/lalamove.svg",
            "transportation_type": "Bike",
            "transportation": "-",
            "durations": "7mins",
            "parcel_type_support": "Parcel",
            "payload": "10kg",
            "dimension": "30cmx30cmx30cm",
            "estimate_total": "4.71",
            "currency": "MYR",
            "metadata": {
                "quotationId": "3114850556997669457"
            }
        },
        {
            "req_id": "9effff62-2de3-4bd0-9863-4ee9fa19a7e5",
            "sid": 5,
            "short_name": "Lalamove",
            "courier": "Lalamove",
            "img_courier": "https://s3-ap-southeast-1.amazonaws.com/easyparcel/Public/source/general/img/couriers/lalamove.svg",
            "transportation_type": "4X4",
            "transportation": "-",
            "durations": "7mins",
            "parcel_type_support": "Ideal for small fridge, washing machine, bike, 1-seater sofa",
            "payload": "250kg",
            "dimension": "120cmx90cmx90cm",
            "estimate_total": "9.41",
            "currency": "MYR",
            "metadata": {
                "quotationId": "3114855291217646120"
            }
        },
        {
            "req_id": "85ce9abb-ff6d-4733-b03e-a6936f80de84",
            "sid": 6,
            "short_name": "Lalamove",
            "courier": "Lalamove",
            "img_courier": "https://s3-ap-southeast-1.amazonaws.com/easyparcel/Public/source/general/img/couriers/lalamove.svg",
            "transportation_type": "Large Van",
            "transportation": "-",
            "durations": "7mins",
            "parcel_type_support": "Ideal for washing machine, sofa, treadmill , large parcels",
            "payload": "800kg",
            "dimension": "270cmx130cmx120cm",
            "estimate_total": "22.59",
            "currency": "MYR",
            "metadata": {
                "quotationId": "3114855291217646121"
            }
        },
        {
            "req_id": "e086a156-afe9-4a94-9fa4-3e31c53ab094",
            "sid": 7,
            "short_name": "Lalamove",
            "courier": "Lalamove",
            "img_courier": "https://s3-ap-southeast-1.amazonaws.com/easyparcel/Public/source/general/img/couriers/lalamove.svg",
            "transportation_type": "Lorry 10-ft",
            "transportation": "-",
            "durations": "7mins",
            "parcel_type_support": "Ideal for queen size bed, fridge, 3-seater sofa, wardrobe",
            "payload": "1000kg",
            "dimension": "290cmx150cmx150cm",
            "estimate_total": "32.00",
            "currency": "MYR",
            "metadata": {
                "quotationId": "3114855291217646122"
            }
        },
        {
            "req_id": "6c551ffb-9ea8-49c4-a32b-5ff60e5f1e2f",
            "sid": 8,
            "short_name": "Lalamove",
            "courier": "Lalamove",
            "img_courier": "https://s3-ap-southeast-1.amazonaws.com/easyparcel/Public/source/general/img/couriers/lalamove.svg",
            "transportation_type": "Lorry 14-ft",
            "transportation": "-",
            "durations": "7mins",
            "parcel_type_support": "Ideal for king size bed, large fridge, 3-seater sofa, wardro",
            "payload": "2500kg",
            "dimension": "420cmx200cmx200cm",
            "estimate_total": "64.00",
            "currency": "MYR",
            "metadata": {
                "quotationId": "3114850556997669458"
            }
        },
        {
            "req_id": "9625a425-692f-48e2-9d52-aa520ad43d04",
            "sid": 9,
            "short_name": "Lalamove",
            "courier": "Lalamove",
            "img_courier": "https://s3-ap-southeast-1.amazonaws.com/easyparcel/Public/source/general/img/couriers/lalamove.svg",
            "transportation_type": "Van",
            "transportation": "-",
            "durations": "7mins",
            "parcel_type_support": "Ideal for small fridge, washing machine, bike, 1-seater sofa",
            "payload": "500kg",
            "dimension": "170cmx100cmx120cm",
            "estimate_total": "16.00",
            "currency": "MYR",
            "metadata": {
                "quotationId": "3114850556997669459"
            }
        },
        {
            "sid": 10,
            "short_name": "PandaGo",
            "courier": "PandaGo",
            "img_courier": "https://s3-ap-southeast-1.amazonaws.com/easyparcel/Public/source/general/img/couriers/pandaGo_pink.png",
            "transportation_type": "Bike",
            "transportation": "-",
            "durations": "6mins",
            "parcel_type_support": "Parcel",
            "payload": "15kg",
            "dimension": "43cmx39cmx42cm",
            "estimate_total": "7.06",
            "currency": "MYR",
            "metadata": []
        },
        {
            "sid": 17,
            "short_name": "PandaGoSG",
            "courier": "PandaGo",
            "img_courier": "https://s3-ap-southeast-1.amazonaws.com/easyparcel/Public/source/general/img/couriers/pandaGo_pink.png",
            "transportation_type": "Bike",
            "transportation": "-",
            "durations": "-",
            "parcel_type_support": "Parcel",
            "payload": "15kg",
            "dimension": "43cmx39cmx42cm",
            "estimate_total": "50.28",
            "currency": "MYR",
            "metadata": []
        }
    ],
    "rejected": null,
    "last_key": ""
}
```
</details>

---
<br>

### Submit OnDemand Order
Submit OnDemand Orders: This features enables users to submit the OnDemand shipment orders. Users are required to fill in the necessary fields to access the insurance rate information.

<details id="Request"> 
  <summary><h5>Request:</h5></summary> 
 
##### Request
Parameter used:
L1

| Requested Parameters | Type      | Required | Description                                                                                                                                         |
| -------------------- | --------- | -------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| from_country         | string(2) | Yes      | Sender's country (refer to [country code](#country-code))                                                                                           |
| ondemand_service_id  | string    | Yes      | ondemand service id                                                                                                                                 |
| waypoint_list        | array     | Yes      | An array of waypoints, detailing each stop in the delivery route, including pickup and dropoff locations (refer to [waypoint-list](#Waypoint-list)) |
| schedule_pickup_date | date      | Yes      | Preferred parcel pickup date                                                                                                                        |
| schedule_pickup_time | time      | Yes      | Preferred parcel pickup time                                                                                                                        |
| timezone             | string    | Yes      | Timezone of the parcel located at                                                                                                                   |
| metadata             | array     | Yes      | refer to [metadata](#metadata)                                                                                                                      |

L2 
###### Waypoint list

| Requested Parameters      | Type       | Required | Description                                                                |
| ------------------------- | ---------- | -------- | -------------------------------------------------------------------------- |
| order                     | int        | Yes      | Order sequence                                                             |
| coordinates               | array      | Yes      | Coordinates of the parcel refer to [Coordinates](#Coordinates)             |
| type                      | string     | Yes      | Type/ Categories of the parcel                                             |
| firstName                 | string     | Yes      | Sender's first name                                                        |
| email                     | string     | Yes      | Sender's email name                                                        |
| package                   | array      | Yes      | Package descriptions and quantity (refer to [Package](#Package))           |
| phone_number_country_code | string (2) | Yes      | Sender's phone number country code(refer to [country code](#country-code)) |
| phone_number              | string     | Yes      | Sender's phone number                                                      |
| address                   | string     | Yes      | Address of the parcel                                                      |
| remark                    | string     | Yes      | Remarks for the parcel and shipping                                        |

###### Metadata

| Requested Parameters | Type       | Required | Description                        |
| -------------------- | ---------- | -------- | ---------------------------------- |
| quotationId          | string(35) | Yes      | Unique Id of the request quotation |

L3
###### Coordinates

| Requested Parameters | Type   | Required | Description                      |
| -------------------- | ------ | -------- | -------------------------------- |
| latitude             | double | Yes      | latitude of the parcel location  |
| longitude            | double | Yes      | longitude of the parcel location |

###### Package

| Requested Parameters | Type   | Required | Description                                                |
| -------------------- | ------ | -------- | ---------------------------------------------------------- |
| quantity             | int    | Yes      | Quantity of the parcel                                     |
| description          | string | Yes      | Parcel / content description                               |
| Dimension            | array  | Yes      | Dimension of the parcel (refer to [Dimension](#Dimension)) |

L4 
###### Dimension

| Requested Parameters | Type         | Required | Description          |
| -------------------- | ------------ | -------- | -------------------- |
| height               | double (8,2) | Yes      | Height of the parcel |
| width                | double (8,2) | Yes      | Width of the parcel  |
| length               | double (8,2) | Yes      | Length of the parcel |
| weight               | double (8,2) | Yes      | Weight of the parcel |



Sample code:
```
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => 'http://localhost:8023/open_api/ondemand/order',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS =>'
{
    "from_country": "MY",
    "ondemand_service_id": 3,
    "waypoint_list": [
        {
            "order": 0,
            "coordinates": {
                "latitude": 5.342720241204454,
                "longitude": 100.28204988381822
            },
            "type": "pickup",
            "firstName": "111",
            "email": "as@as.as",
            "package": [
                {
                    "quantity": "1",
                    "description": "1",
                    "dimensions": {
                        "height": "1",
                        "width": "1",
                        "length": "1",
                        "weight": "1"
                    }
                }
            ],
            "phone_number_country_code": "MY",
            "phone_number": "1278491622",
            "address": "L1 Lobby, Suntec City Tower 1 & 2, 7 Temasek Boulevard, Singapore, 038987",
            "remark": "1"
        },
        {
            "order": 1,
            "coordinates": {
                "latitude": 5.325513957,
                "longitude": 100.2862732
            },
            "type": "dropoff",
            "firstName": "222",
            "email": "as@as.as",
            "package": [
                {
                    "quantity": "2",
                    "description": "2",
                    "dimensions": {
                        "height": "2",
                        "width": "2",
                        "length": "2",
                        "weight": "2"
                    }
                }
            ],
            "phone_number_country_code": "MY",
            "phone_number": "127491622",
            "address": "Terminal 1 Departure - Changi Airport, 80 Airport Boulevard, Singapore, 819642",
            "remark": "222"
        }
    ],

    "schedule_pickup_date": "2024-12-10",
    "schedule_pickup_time": "17:35:15",
    "timezone": "Asia/Kuala_Lumpur",
    "metadata": {
        "quotationId": "3114850556997669249"
    }
}',
  CURLOPT_HTTPHEADER => array(
    'Content-Type: application/json'
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;


```
</details>

<details id="Respond"> 
  <summary><h5>Respond:</h5></summary> 
 
##### Respond

Returned parameters

L1

| Returned Parameters | Type   | Description                                                              |
| ------------------- | ------ | ------------------------------------------------------------------------ |
| app_uuid            | string |                                                                          |
| ondemand_service_id | string | ID for on-demand delivery service.                                       |
| order_number        | string | unique number assigned to the order                                      |
| tracking_url        | string | url that link customer to the tracking page to check the delivery status |
| ondemand_payment    | array  | (refer to [ondemand_payment](#ondemand_payment))                         |

L2
###### ondemand_payment
| Requested Parameters | Type   | Description                                 |
| -------------------- | ------ | ------------------------------------------- |
| selling_amount       | double | price of the delivery                       |
| selling_currency     | string | currency used for the price of the currency |

Respond Sample:
```
{
    "status_code": 200,
    "message": "Success",
    "data": {
        "app_uuid": "738e6358-9692-46fa-902f-4edc5463d00c",
        "ondemand_service_id": 3,
        "order_number": "177382847011",
        "tracking_url": "https://share.sandbox.lalamove.com?MY100241206113420384420020079033972&lang=en_MY&sign=50399fb8912d67c5d49d4678b941d614&source=api_wrapper",
        "ondemand_payment": {
            "selling_amount": "5.65",
            "selling_currency": "MYR"
        }
    }
}
```
</details>

---
<br>

### References

<details id="api-status"> 
  <summary><h4>API Return Status</h4></summary> 
  
API Return Status

| Status Code | Description           | Meaning                                                                                                     |
| ----------- | --------------------- | ----------------------------------------------------------------------------------------------------------- |
| 200         | OK                    | The request was successful.                                                                                 |
| 201         | Created               | The request was successful, and a resource was created.                                                     |
| 204         | No Content            | The request was successful, but there is no content to send in the response.                                |
| 400         | Bad Request           | The request could not be understood or was missing required parameters.                                     |
| 401         | Unauthorized          | Authentication failed or user does not have permissions for the requested operation.                        |
| 403         | Forbidden             | Authentication succeeded, but the authenticated user does not have access to the requested resource.        |
| 404         | Not Found             | The requested resource could not be found.                                                                  |
| 500         | Internal Server Error | An error occurred on the server.                                                                            |
| 502         | Bad Gateway           | The server was acting as a gateway or proxy and received an invalid response from the upstream server.      |
| 503         | Service Unavailable   | The server is currently unavailable (because it is overloaded or down for maintenance).                     |
| 504         | Gateway Timeout       | The server was acting as a gateway or proxy and did not receive a timely response from the upstream server. |
</details> 
<details id="country-code"> 
  <summary><h4>Country Code</h4></summary> 

| Short Country Name | Full Country Name                     |
|--------------------|----------------------------------------|
| SR                 | SURINAME                               |
| SD                 | SUDAN                                  |
| VC                 | ST. VINCENT                            |
| XM                 | ST. MAARTEN                            |
| LC                 | ST. LUCIA                              |
| KN                 | ST. KITTS                              |
| XE                 | ST. EUSTATIUS                          |
| BL                 | ST. BARTHELEMY                         |
| LK                 | SRI LANKA                              |
| ES                 | SPAIN                                  |
| ZA                 | SOUTH AFRICA                           |
| XS                 | SOMALILAND (NORTH SOMALIA)             |
| SO                 | SOMALIA                                |
| SB                 | SOLOMON ISLANDS                        |
| SI                 | SLOVENIA                               |
| SK                 | SLOVAKIA                               |
| SG                 | SINGAPORE                              |
| SL                 | SIERRA LEONE                           |
| SC                 | SEYCHELLES                             |
| RS                 | SERBIA                                 |
| SN                 | SENEGAL                                |
| SA                 | SAUDI ARABIA                           |
| ST                 | SAO TOME AND PRINCIPE                  |
| SM                 | SAN MARINO                             |
| WS                 | SAMOA                                  |
| MP                 | SAIPAN                                 |
| RW                 | RWANDA                                 |
| RU                 | RUSSIAN FEDERATION                     |
| RO                 | ROMANIA                                |
| RE                 | REUNION                                |
| QA                 | QATAR                                  |
| PR                 | PUERTO RICO                            |
| PT                 | PORTUGAL                               |
| PL                 | POLAND                                 |
| PH                 | PHILIPPINES                            |
| PE                 | PERU                                   |
| PY                 | PARAGUAY                               |
| PG                 | PAPUA NEW GUINEA                       |
| PA                 | PANAMA                                 |
| PW                 | PALAU                                  |
| PK                 | PAKISTAN                               |
| OM                 | OMAN                                   |
| NO                 | NORWAY                                 |
| NU                 | NIUE                                   |
| NG                 | NIGERIA                                |
| NE                 | NIGER                                  |
| NI                 | NICARAGUA                              |
| NZ                 | NEW ZEALAND                            |
| NC                 | NEW CALEDONIA                          |
| XN                 | NEVIS                                  |
| NL                 | NETHERLANDS                            |
| NP                 | NEPAL                                  |
| NR                 | NAURU                                  |
| NA                 | NAMIBIA                                |
| MM                 | MYANMAR                                |
| MA                 | MOROCCO                                |
| MS                 | MONTSERRAT                             |
| ME                 | MONTENEGRO                             |
| MN                 | MONGOLIA                               |
| MC                 | MONACO                                 |
| MD                 | MOLDOVA, REPUBLIC OF                   |
| FM                 | MICRONESIA, FEDERATED STATES OF        |
| MX                 | MEXICO                                 |
| YT                 | MAYOTTE                                |
| MU                 | MAURITIUS                              |
| MR                 | MAURITANIA                             |
| MQ                 | MARTINIQUE                             |
| MH                 | MARSHALL ISLANDS                       |
| MT                 | MALTA                                  |
| ML                 | MALI                                   |
| MV                 | MALDIVES                               |
| MW                 | MALAWI                                 |
| MY                 | MALAYSIA                               |
| MG                 | MADAGASCAR                             |
| MK                 | MACEDONIA, THE FORMER YUGOSLAV REPUBLIC OF |
| MO                 | MACAU                                  |
| LU                 | LUXEMBOURG                             |
| LT                 | LITHUANIA                              |
| LI                 | LIECHTENSTEIN                          |
| LY                 | LIBYA                                  |
| LR                 | LIBERIA                                |
| LS                 | LESOTHO                                |
| LB                 | LEBANON                                |
| LV                 | LATVIA                                 |
| LA                 | LAO PEOPLE'S DEMOCRATIC REPUBLIC       |
| KG                 | KYRGYZSTAN                             |
| KW                 | KUWAIT                                 |
| XK                 | KOSOVO                                 |
| KR                 | KOREA, REPUBLIC OF                     |
| KP                 | KOREA, DEMOCRATIC PEOPLE'S REPUBLIC OF |
| KI                 | KIRIBATI                               |
| KE                 | KENYA                                  |
| KZ                 | KAZAKHSTAN                             |
| JO                 | JORDAN                                 |
| JE                 | JERSEY                                 |
| JP                 | JAPAN                                  |
| JM                 | JAMAICA                                |
| IT                 | ITALY                                  |
| IL                 | ISRAEL                                 |
| IE                 | IRELAND                                |
| IQ                 | IRAQ                                   |
| IR                 | IRAN, ISLAMIC REPUBLIC OF              |
| ID                 | INDONESIA                              |
| IN                 | INDIA                                  |
| IS                 | ICELAND                                |
| HU                 | HUNGARY                                |
| HK                 | HONG KONG                              |
| HN                 | HONDURAS                               |
| HT                 | HAITI                                  |
| GY                 | GUYANA                                 |
| GW                 | GUINEA BISSAU                          |
| GN                 | GUINEA REPUBLIC                        |
| GG                 | GUERNSEY                               |
| GT                 | GUATEMALA                              |
| GU                 | GUAM                                   |
| GP                 | GUADELOUPE                             |
| GD                 | GRENADA                                |
| GL                 | GREENLAND                              |
| GR                 | GREECE                                 |
| GI                 | GIBRALTAR                              |
| GH                 | GHANA                                  |
| DE                 | GERMANY                                |
| GE                 | GEORGIA                                |
| GM                 | GAMBIA                                 |
| GA                 | GABON                                  |
| ZW                 | ZIMBABWE                               |
| FR                 | FRANCE                                 |
| FI                 | FINLAND                                |
| ZM                 | ZAMBIA                                 |
| FJ                 | FIJI                                   |
| YE                 | YEMEN                                  |
| FO                 | FAROE ISLANDS                          |
| FK                 | FALKLAND ISLANDS (MALVINAS)            |
| ET                 | ETHIOPIA                               |
| VI                 | VIRGIN ISLANDS, U.S.                   |
| EE                 | ESTONIA                                |
| VG                 | VIRGIN ISLANDS, BRITISH                |
| ER                 | ERITREA                                |
| GQ                 | EQUATORIAL GUINEA                      |
| SV                 | EL SALVADOR                            |
| EG                 | EGYPT                                  |
| VN                 | VIETNAM                                |
| EC                 | ECUADOR                                |
| TP                 | EAST TIMOR                             |
| VE                 | VENEZUELA                              |
| DO                 | DOMINICAN REPUBLIC                     |
| DM                 | DOMINICA                               |
| DJ                 | DJIBOUTI                               |
| VU                 | VANUATU                                |
| DK                 | DENMARK                                |
| CZ                 | CZECH REPUBLIC                         |
| CY                 | CYPRUS                                 |
| CU                 | CUBA                                   |
| UZ                 | UZBEKISTAN                             |
| UY                 | URUGUAY                                |
| HR                 | CROATIA                                |
| CI                 | COTE D'IVOIRE                          |
| CR                 | COSTA RICA                             |
| CK                 | COOK ISLANDS                           |
| CD                 | CONGO, THE DEMOCRATIC REPUBLIC OF THE  |
| UM                 | UNITED STATES MINOR OUTLYING ISLANDS   |
| CG                 | CONGO                                  |
| KM                 | COMOROS                                |
| CN                 | CHINA                                  |
| US                 | UNITED STATES                          |
| GF                 | FRENCH GUIANA                          |
| AN                 | NETHERLANDS ANTILLES                   |
| MZ                 | MOZAMBIQUE                             |
| CW                 | CURACAO                                |
| CO                 | COLOMBIA                               |
| CL                 | CHILE                                  |
| TD                 | CHAD                                   |
| CF                 | CENTRAL AFRICAN REPUBLIC               |
| KY                 | CAYMAN ISLANDS                         |
| GB                 | UNITED KINGDOM                         |
| CV                 | CAPE VERDE                             |
| AE                 | UNITED ARAB EMIRATES                   |
| IC                 | CANARY ISLANDS, THE                    |
| CA                 | CANADA                                 |
| UA                 | UKRAINE                                |
| CM                 | CAMEROON                               |
| KH                 | CAMBODIA                               |
| UG                 | UGANDA                                 |
| BI                 | BURUNDI                                |
| BF                 | BURKINA FASO                           |
| BG                 | BULGARIA                               |
| BN                 | BRUNEI DARUSSALAM                      |
| TV                 | TUVALU                                 |
| BR                 | BRAZIL                                 |
| TC                 | TURKS AND CAICOS ISLANDS               |
</details>
<details id="iso3166"> 
  <summary><h4>ISO_3166</h4></summary> 

At EasyParcel, we adhere to the ISO 3166 standard for the identification of states, provinces, and zones. For example, the code "MY-07" corresponds to the state of Penang in Malaysia.

ISO 3166 is a standard published by the International Organization for Standardization (ISO) that defines codes for the names of countries, dependent territories, special areas of geographical interest, and their principal subdivisions (e.g., provinces or states). The official name of the standard is Codes for the representation of names of countries and their subdivisions.
</details>
<details id="malaysia-state-code" >
  <summary><h4>Malaysia State Code</h4></summary>
  
  | Short State Name | Full State Name    |
  |------------------|--------------------|
  | jhr              | Johor              |
  | kdh              | Kedah              |
  | ktn              | Kelantan           |
  | mlk              | Melaka             |
  | nsn              | Negeri Sembilan    |
  | phg              | Pahang             |
  | prk              | Perak              |
  | pls              | Perlis             |
  | png              | Pulau Pinang       |
  | sgr              | Selangor           |
  | trg              | Terengganu         |
  | kul              | Kuala Lumpur       |
  | pjy              | Putra Jaya         |
  | srw              | Sarawak            |
  | sbh              | Sabah              |
  | lbn              | Labuan             |
</details>
<details id="Insurance-Courier-List">
  <summary><h4>Insurance Courier List</h4></summary>
 
| Courier | Courier Name       |
|---------|--------------------|
| EP-CR0DP| J&T Express        |
| EP-CR0DK| Pickupp            |
| EP-CR0DU| Ninjavan           |
| EP-CR0D3| J&T Cargo          |
| EP-CR0U | TNT                |
| EP-CR0DH| Best Express       |
| EP-CR0D1| City-Link Express  |
| EP-CR0T | FedEx              |
| EP-CR06 | Aramex International|
</details>







