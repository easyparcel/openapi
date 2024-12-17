### Get Courier Dropoff point
Get Courier Drop off point: This features enables users to check the available Drop off point for selected courier and zones. Users are required to fill in the necessary fields to access the insurance rate information.

### [Request](#Requested-Parameters)  |  [Return](#Returned-Parameters) 

#### Requested Parameters

L1

| Requested Parameters | Type       | Required | Description                                                           |
| -------------------- | ---------- | -------- | --------------------------------------------------------------------- |
| courier_id           | string(25) | Yes      | Courier identification number                                         |
| country_code         | string(2)  | Yes      | Dropoff point's country code (refer to [country code](References/country%20code)) |
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

 --- 

#### Returned parameters

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

Return Sample:
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
