### Submit OnDemand Order
Submit OnDemand Orders: This features enables users to submit the OnDemand shipment orders. Users are required to fill in the necessary fields to access the insurance rate information.

### [Request](#Requested-Parameters)  |  [Return](#Returned-Parameters) 

#### Requested Parameters:

| Requested Parameters | Type      | Required | Description                                                                                                                                         |
| -------------------- | --------- | -------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| from_country         | string(2) | Yes      | Sender's country (refer to [Country Code](../References/Country%20Code.md))                                                                                           |
| ondemand_service_id  | string    | Yes      | ondemand service id                                                                                                                                 |
| waypoint_list        | array     | Yes      | An array of waypoints, detailing each stop in the delivery route, including pickup and dropoff locations (refer to [waypoint-list](#Waypoint-list)) |
| schedule_pickup_date | date      | Yes      | Preferred parcel pickup date                                                                                                                        |
| schedule_pickup_time | time      | Yes      | Preferred parcel pickup time                                                                                                                        |
| timezone             | string    | Yes      | Timezone of the parcel located at                                                                                                                   |
| metadata             | array     | Yes      | refer to [metadata](#metadata)                                                                                                                      |

###### Waypoint list

| Requested Parameters      | Type       | Required | Description                                                                |
| ------------------------- | ---------- | -------- | -------------------------------------------------------------------------- |
| order                     | int        | Yes      | Order sequence                                                             |
| coordinates               | array      | Yes      | Coordinates of the parcel refer to [Coordinates](#Coordinates)             |
| type                      | string     | Yes      | Type/ Categories of the parcel                                             |
| firstName                 | string     | Yes      | Sender's first name                                                        |
| email                     | string     | Yes      | Sender's email name                                                        |
| package                   | array      | Yes      | Package descriptions and quantity (refer to [Package](#Package))           |
| phone_number_country_code | string (2) | Yes      | Sender's phone number country code(refer to [Country Code](../References/Country%20Code.md)) |
| phone_number              | string     | Yes      | Sender's phone number                                                      |
| address                   | string     | Yes      | Address of the parcel                                                      |
| remark                    | string     | Yes      | Remarks for the parcel and shipping                                        |

###### Metadata

| Requested Parameters | Type       | Required | Description                        |
| -------------------- | ---------- | -------- | ---------------------------------- |
| quotationId          | string(35) | Yes      | Unique Id of the request quotation |


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


###### Dimension

| Requested Parameters | Type         | Required | Description          |
| -------------------- | ------------ | -------- | -------------------- |
| height               | double (8,2) | Yes      | Height of the parcel |
| width                | double (8,2) | Yes      | Width of the parcel  |
| length               | double (8,2) | Yes      | Length of the parcel |
| weight               | double (8,2) | Yes      | Weight of the parcel |



Request Sample code:
```
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
}
```

---

#### Returned parameters


| Returned Parameters | Type   | Description                                                              |
| ------------------- | ------ | ------------------------------------------------------------------------ |
| app_uuid            | string | A unique ID for your app, created to make sure each app has a distinct identifier. |
| ondemand_service_id | string | ID for on-demand delivery service.                                       |
| order_number        | string | unique number assigned to the order                                      |
| tracking_url        | string | url that link customer to the tracking page to check the delivery status |
| ondemand_payment    | array  | (refer to [ondemand_payment](#ondemand_payment))                         |


###### ondemand_payment
| Requested Parameters | Type   | Description                                 |
| -------------------- | ------ | ------------------------------------------- |
| selling_amount       | double | price of the delivery                       |
| selling_currency     | string | currency used for the price of the currency |

Return Sample:
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

