### Get Insurance Quotation:
Get Insurance Quotation: This features enables users to check the insurance quotations from specific courier companies on the EasyParcel platform. Users are required to fill in the necessary fields to access the insurance rate information.

### [Request](#Requested-Parameters)  |  [Return](#Returned-Parameters) 

#### Requested Parameters

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


### Requested Parameters

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

Return Sample:
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

