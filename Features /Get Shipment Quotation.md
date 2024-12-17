### Get Shipment Quotation:
Get Shipment Quotation: This feature enables users to obtain shipment quotations from all courier companies available on the EasyParcel platform. Users need to provide sender and receiver addresses to check the shipment quotation.

### [Request](#Requested-Parameters)  |  [Return](#Returned-Parameters) 

#### Requested Parameters:

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

#### Returned Parameters:

Return L1

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

Return L2
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

Return Sample:
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

            ]
        }
    ]
}
```
</details>
