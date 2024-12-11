# Overview

### Easy Parcel API

The EasyParcel API allows your application to access current data within EasyParcel. However, EasyParcel API is using RESTful with PHP concept to develop API for web based applications. Through the API, several common operations can be performed on EasyParcel objects.


| API         | Link                               |
| ----------- | ---------------------------------- |
| Development | http://demo.connect.easyparcel.my/ |
| Production  | https://connect.easyparcel.my/     |

API Functions/Features:
#### Get Shipment Quotation:
Get Shipment Quotation: This feature enables users to obtain shipment quotations from all courier companies available on the EasyParcel platform. Users need to provide sender and receiver addresses to check the shipment quotation.

Parameters used:

| Requested Parameters | Type        | Required | Description                            |
| -------------------- | ----------- | -------- | -------------------------------------- |
| from_postcode        | string(10)  | Yes      | Sender's postcode                      |
| from_state           | string(35)  | Yes      | Sender's state                         |
| from_country         | string(2)   | Yes      | Sender's country [[Country Code List]] |
| to_postcode          | string(10)  | Yes      | Receiver's postcode                    |
| to_state             | string(35)  | Yes      | Receiver's state                       |
| to_country           | string(2)   | Yes      | Receiver's country                     |
| weight               | double(8,2) | Yes      | The weight of the parcel.              |

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


| Requested Parameters | Type        | Required | Description                   |
| -------------------- | ----------- | -------- | ----------------------------- |
| courier_id           | string(25)  | Yes      | Courier Identification number |
| items                | string      | Yes      | Item Name                     |
| quantity             | int (10)    | Yes      | Quantity of the item          |
| value                | double(8,2) | Yes      | Value of the item             |
| currency_code        | string (3)  | Yes      | Country's currency            |
| shipment_weight      | double(8,2) | Yes      | Weight of item                |
| shipment_width       | double(8,2) | Optional | Width of item                 |
| shipment_length      | double(8,2) | Optional | Length of item                |
| shipment_height      | double(8,2) | Optional | Height of item                |
| coll_postcode        | string(10)  | Yes      | Sender's post code            |
| coll_province_code   | string(35)  | Yes      | Sender's province code        |
| coll_country_code    | string(2)   | Yes      | Sender's country code         |
| deli_postcode        | string(10)  | Yes      | Receiver's post code          |
| deli_province_code   | string(35)  | Yes      | Receiver's province code      |
| deli_country_code    | string(2)   | Yes      | Receiver's country code       |
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

Parameters used:

| Requested Parameters | Type       | Required | Description                   |
| -------------------- | ---------- | -------- | ----------------------------- |
| courier_id           | string(25) | Yes      | Courier identification number |
| country_code         | string(2)  | Yes      | Dropoff point's country code  |
| postcode             | string(10) | Yes      | Dropoff point's postcode      |
| city                 | string(35) | Yes      | Dropoff point's city          |
| state_code           | string(35) | Yes      | Dropoff point's state_code    |

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




#### Submit Shipment Orders
Submit Shipment Orders: This features enables users to submit the shipment orders. Users are required to fill in the necessary fields to access the insurance rate information.

Parameters used:

| Requested Parameters | Type        | Required | Description |
| -------------------- | ----------- | -------- | ----------- |
| service_id           | string(10)  | Yes      |             |
| collection_date      | date        | Yes      |             |
| weight               | double(8,2) | Yes      |             |
| height               | double(8,2) | Yes      |             |
| length               | double(8,2) | Yes      |             |
| width                | double(8,2) | Yes      |             |


**Items**

| Requested Parameters | Type        | Required | Description |
| -------------------- | ----------- | -------- | ----------- |
| content              | string      | Yes      |             |
| currency_code        | string (3)  | Yes      |             |
| value                | double(8,2) | Yes      |             |
| quantity             | int         | Yes      |             |
| insurance_service_id | string      | Yes      |             |
| invoices             | string      | Yes      |             |
| photos               | string      | Yes      |             |


**Origin**

| Requested Parameters      | Type      | Required | Description |
| ------------------------- | --------- | -------- | ----------- |
| name                      | string    | Yes      |             |
| company                   | string    | Yes      |             |
| phone_number_country_code | string    | Yes      |             |
| phone_number              | string    | Yes      |             |
| email                     | string    | Yes      |             |
| address_1                 | string    | Yes      |             |
| address_2                 | string    | Yes      |             |
| postcode                  | string    | Yes      |             |
| town                      | string    | Yes      |             |
| province_code             | string    | Yes      |             |
| country_code              | string(2) | Yes      |             |

**Destination**

| Requested Parameters      | Type      | Required | Description |
| ------------------------- | --------- | -------- | ----------- |
| name                      | string    | Yes      |             |
| company                   | string    | Yes      |             |
| phone_number_country_code | string    | Yes      |             |
| phone_number              | string    | Yes      |             |
| email                     | string    | Yes      |             |
| address_1                 | string    | Yes      |             |
| address_2                 | string    | Yes      |             |
| postcode                  | string    | Yes      |             |
| town                      | string    | Yes      |             |
| province_code             | string    | Yes      |             |
| country_code              | string(2) | Yes      |             |

**Notification**

| Requested Parameters | Type    | Required | Description |
| -------------------- | ------- | -------- | ----------- |
| sms                  | boolean | Yes      |             |
| email                | boolean | Yes      |             |
| whatsapp             | boolean | Yes      |             |


**Airways Bills Branding**

| Requested Parameters | Type    | Required | Description |
| -------------------- | ------- | -------- | ----------- |
| enable               | boolean | Yes      |             |


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
        "email": "weikeong.liew@easyparcel.com",
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
        "email": "weikeong.liew@easyparcel.com",
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
#### Get OnDemand Quotation
Get OnDemand Quotation: This feature enables users to obtain OnDemand Shipment quotations from all courier companies available on the EasyParcel platform. Users need to provide sender and receiver addresses to check the shipment quotation.

Parameter used:

| Requested Parameters | Type   | Required | Description |
| -------------------- | ------ | -------- | ----------- |
| schedule_pickup_date | date   | Yes      |             |
| schedule_pickup_time | time   | Yes      |             |
| timezone             | string | Yes      |             |
| address              | string | Yes      |             |
| type                 | string | Yes      |             |

**coordinates**

| Requested Parameters | Type   | Required | Description |
| -------------------- | ------ | -------- | ----------- |
| latitude             | double | Yes      |             |
| longitude            | double | Yes      |             |


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


#### Submit OnDemand Order
Submit OnDemand Orders: This features enables users to submit the OnDemand shipment orders. Users are required to fill in the necessary fields to access the insurance rate information.

Parameter used:

| Requested Parameters      | Type       | Required | Description |
| ------------------------- | ---------- | -------- | ----------- |
| from_country              | string(2)  | Yes      |             |
| ondemand_service_id       | string     | Yes      |             |
| order                     | int        | Yes      |             |
| type                      | string     | Yes      |             |
| firstName                 | string     | Yes      |             |
| email                     | string     | Yes      |             |
| phone_number_country_code | string (2) | Yes      |             |
| phone_number              | string     | Yes      |             |
| address                   | string     | Yes      |             |
| remark                    | string     | Yes      |             |
| schedule_pickup_date      | date       | Yes      |             |
| schedule_pickup_time      | time       | Yes      |             |
| timezone                  | string     | Yes      |             |
**Coordinates**

| Requested Parameters | Type   | Required | Description |
| -------------------- | ------ | -------- | ----------- |
| latitude             | double | Yes      |             |
| longitude            | double | Yes      |             |

**Package**

| Requested Parameters | Type   | Required | Description |
| -------------------- | ------ | -------- | ----------- |
| quantity             | int    | Yes      |             |
| description          | string | Yes      |             |
**Dimension**

| Requested Parameters | Type         | Required | Description |
| -------------------- | ------------ | -------- | ----------- |
| height               | int          | Yes      |             |
| width                | double (8,2) | Yes      |             |
| length               | double (8,2) | Yes      |             |
| weight               | double (8,2) | Yes      |             |
**metadata**

| Requested Parameters | Type       | Required | Description |
| -------------------- | ---------- | -------- | ----------- |
| quotationId          | string(35) | Yes      |             |
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




#### References 

<details> 
  <summary><h4>Country Code List</h4></summary> 
  <div>
    
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
  </div>
</details>

<details>
  <summary><h4>Malaysia State Code</h4></summary>
  <div>

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

  </div>
</details>

<details>
  <summary><h4>Insurance Courier List</h4></summary>
  <div>

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

  </div>
</details>

