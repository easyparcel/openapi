### Get OnDemand Quotation
Get OnDemand Quotation: This feature enables users to obtain OnDemand Shipment quotations from all courier companies available on the EasyParcel platform. Users need to provide sender and receiver addresses to check the shipment quotation.

### [Request](#Requested-Parameters)  |  [Return](#Returned-Parameters) 

#### Requested Parameters:

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

---

#### Returned Parameters:

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

Return Sample:
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
