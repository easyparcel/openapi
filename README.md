# Overview

### Easy Parcel API

The EasyParcel API allows your application to access current data within EasyParcel. However, EasyParcel API is using RESTful with PHP concept to develop API for web based applications. Through the API, several common operations can be performed on EasyParcel objects.


| API         | Link                               |
| ----------- | ---------------------------------- |
| Development | http://demo.connect.easyparcel.my/ |
| Production  | https://connect.easyparcel.my/     |

API Functions/Features:

#### Get Shipment Quotation:
Get Shipment Quotation: This feature enables users to obtain shipment quotations from all courier companies on the EasyParcel platform. Users need to provide sender and receiver addresses to check the shipment quotation.

Parameters used:

| Requested Parameters | Type | Required | Description |
| -------------------- | ---- | -------- | ----------- |
| from_postcode        |      |          |             |
| from_state           |      |          |             |
| from_country         |      |          |             |
| to_postcode          |      |          |             |
| to_state             |      |          |             |
| to_country           |      |          |             |
| weight               |      |          |             |

Sample Code:
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


#### Get Insurance Quotation:
Get Insurance Quotation: This features enables users to check the insurance quotations from specific courier companies on the EasyParcel platform. Users are required to fill in the necessary fields to access the insurance rate information.


| Requested Parameters | Type | Required | Description |
| -------------------- | ---- | -------- | ----------- |
| courier_id           |      |          |             |
| items                |      |          |             |
| quantity             |      |          |             |
| value                |      |          |             |
| currency_code        |      |          |             |
| shipment_weight      |      |          |             |
| shipment_width       |      |          |             |
| shipment_height      |      |          |             |
| coll_postcode        |      |          |             |
| coll_province_code   |      |          |             |
| coll_country_code    |      |          |             |
| deli_postcode        |      |          |             |
| deli_province_code   |      |          |             |
| deli_country_code    |      |          |             |
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


#### Get Courier Dropoff point
Get Courier Drop off point: This features enables users to check the available Drop off point for selected courier and zones. Users are required to fill in the necessary fields to access the insurance rate information.
