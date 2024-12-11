Overview

Easy Parcel API

The EasyParcel API allows your application to access current data within EasyParcel. However, EasyParcel API is using RESTful with PHP concept to develop API for web based applications. Through the API, several common operations can be performed on EasyParcel objects.


Flow chart




|Development|http://demo.connect.easyparcel.my/|
| :- | :- |
|Production|https://connect.easyparcel.my/|

API Functions

**Get Shipment Quotation:**

Get Shipment Quotation: This feature enables users to obtain shipment quotations from all courier companies on the EasyParcel platform. Users need to provide sender and receiver addresses to check the shipment quotation.

Parameters used:

|Requested Parameters|Type|Required|Description|
| :- | :- | :- | :- |
|from\_postcode||||
|from\_state||||
|from\_country||||
|to\_postcode||||
|to\_state||||
|to\_country||||
|weight||||


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

**Get Insurance Quotation**

Get Insurance Quotation: This features enables users to check the insurance quotations from specific courier companies on the EasyParcel platform. Users are required to fill in the necessary fields to access the insurance rate information.

|Requested Parameters|Type|Required|Description|
| :- | :- | :- | :- |
|courier\_id||||
|items||||
|quantity||||
|value||||
|currency\_code||||
|shipment\_weight||||
|shipment\_length||||
|shipment\_width||||
|shipment\_height||||
|coll_postcode||||
|||||
|||||
|||||


Parameters used:

"list": [

{

"courier\_id": "EP-CR05",

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

"currency\_code": "MYR",

"shipment\_weight": 1.5,

"shipment\_length": 100,

"shipment\_width": 100,

"shipment\_height": 100,

"coll\_postcode": "11900",

"coll\_province\_code": "MY-07",

"coll\_country\_code": "MY",

"deli\_postcode": "11900",

"deli\_province\_code": "MY-07",

"deli\_country\_code": "MY"

},

{

"courier\_id": "EP-CR0A",

"items": [

{

"quantity": 5,

"value": 75.00

}

],

"currency\_code": "MYR",

"shipment\_weight": 0.8,

"shipment\_length": 100,

"shipment\_width": 100,

"shipment\_height": 100,

"coll\_postcode": "11900",

"coll\_province\_code": "MY-07",

"coll\_country\_code": "MY",

"deli\_postcode": "11900",

"deli\_province\_code": "MY-07",

"deli\_country\_code": "MY"

}

]

Sample Code:

<?php

$curl = curl\_init();

curl\_setopt\_array($curl, array(

`  `CURLOPT\_URL => 'http://localhost:8023/open\_api/shipment/insurance\_quotations',

`  `CURLOPT\_RETURNTRANSFER => true,

`  `CURLOPT\_ENCODING => '',

`  `CURLOPT\_MAXREDIRS => 10,

`  `CURLOPT\_TIMEOUT => 0,

`  `CURLOPT\_FOLLOWLOCATION => true,

`  `CURLOPT\_HTTP\_VERSION => CURL\_HTTP\_VERSION\_1\_1,

`  `CURLOPT\_CUSTOMREQUEST => 'POST',

`  `CURLOPT\_POSTFIELDS =>'{

`  `"list": [

`    `{

`      `"courier\_id": "EP-CR05",

`      `"items": [

`        `{

`          `"quantity": 2,

`          `"value": 100.50

`        `},

`        `{

`          `"quantity": 1,

`          `"value": 50.25

`        `}

`      `],

`      `"currency\_code": "MYR",

`      `"shipment\_weight": 1.5,

`      `"shipment\_length": 100,

`      `"shipment\_width": 100,

`      `"shipment\_height": 100,

`      `"coll\_postcode": "11900",

`      `"coll\_province\_code": "MY-07",

`      `"coll\_country\_code": "MY",

`      `"deli\_postcode": "11900",

`      `"deli\_province\_code": "MY-07",

`      `"deli\_country\_code": "MY"

`    `},

`    `{

`      `"courier\_id": "EP-CR0A",

`      `"items": [

`        `{

`          `"quantity": 5,

`          `"value": 75.00

`        `}

`      `],

`      `"currency\_code": "MYR",

`      `"shipment\_weight": 0.8,

`      `"shipment\_length": 100,

`      `"shipment\_width": 100,

`      `"shipment\_height": 100,

`      `"coll\_postcode": "11900",

`      `"coll\_province\_code": "MY-07",

`      `"coll\_country\_code": "MY",

`      `"deli\_postcode": "11900",

`      `"deli\_province\_code": "MY-07",

`      `"deli\_country\_code": "MY"

`    `}

`  `]

}',

`  `CURLOPT\_HTTPHEADER => array(

`    `'Content-Type: application/json'

`  `),

));

$response = curl\_exec($curl);

curl\_close($curl);

echo $response;


**Get Courier Dropoff point**

Get Courier Drop off point: This features enables users to check the available Drop off point for selected courier and zones. Users are required to fill in the necessary fields to access the insurance rate information.

Parameters used:

"courier\_id": "EP-CR0A",

"country\_code": "MY",

"postcode":"09600",

"city":"Lunas",

"state\_code": "MY-02"


Sample code:

<?php

$curl = curl\_init();

curl\_setopt\_array($curl, array(

`  `CURLOPT\_URL => 'http://localhost:8023/open\_api/shipment/get\_courier\_dropoff\_points',

`  `CURLOPT\_RETURNTRANSFER => true,

`  `CURLOPT\_ENCODING => '',

`  `CURLOPT\_MAXREDIRS => 10,

`  `CURLOPT\_TIMEOUT => 0,

`  `CURLOPT\_FOLLOWLOCATION => true,

`  `CURLOPT\_HTTP\_VERSION => CURL\_HTTP\_VERSION\_1\_1,

`  `CURLOPT\_CUSTOMREQUEST => 'POST',

`  `CURLOPT\_POSTFIELDS =>'{

`    `"courier\_id": "EP-CR0A",

`    `"country\_code": "MY",

`    `"postcode":"09600",

`    `"city":"Lunas",

`    `"state\_code": "MY-02"

}',

`  `CURLOPT\_HTTPHEADER => array(

`    `'Content-Type: application/json'

`  `),

));

$response = curl\_exec($curl);

curl\_close($curl);

echo $response;


**Submit Shipment Orders**

Parameters used:

"list": [

{

"service\_id": "EP-CS0IW",

"collection\_date": "2024-10-22",

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

"currency\_code": "MYR",

"value": 200,

"quantity": 1,

"insurance\_purchase":{

"insurance\_service\_id":23,

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

"currency\_code": "MYR",

"value": 500,

"quantity": 1,

"insurance\_purchase":{

"insurance\_service\_id":23,

"invoices": "https://ep-website-media.s3.ap-southeast-1.amazonaws.com/my/wp-content/uploads/2024/02/sf-express-exd.webp"

}

}

],

"origin": {

"name": "John Doe",

"company": "ABC Corp",

"phone\_number\_country\_code": "+60",

"phone\_number": "1163642281",

"email": "weikeong.liew@easyparcel.com",

"address\_1": "123 Main St",

"address\_2": "Apt 4B",

"postcode": "11900",

"town": "Lunas",

"province\_code": "MY-07",

"country\_code": "MY"

},

"destination": {

"name": "Jane Smith",

"company": "XYZ Inc",

"phone\_number\_country\_code": "+60",

"phone\_number": "1163642281",

"email": "weikeong.liew@easyparcel.com",

"address\_1": "456 High St",

"address\_2": "Floor 2",

"postcode": "11900",

"town": "Bayan Lepas",

"province\_code": "MY-07",

"country\_code": "MY",

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

"awb\_branding": {

"enable": true

}

}

]

Sample code:

<?php

$curl = curl\_init();

curl\_setopt\_array($curl, array(

`  `CURLOPT\_URL => 'https://developer.easyparcel.com/open\_api/shipment/submit\_orders',

`  `CURLOPT\_RETURNTRANSFER => true,

`  `CURLOPT\_ENCODING => '',

`  `CURLOPT\_MAXREDIRS => 10,

`  `CURLOPT\_TIMEOUT => 0,

`  `CURLOPT\_FOLLOWLOCATION => true,

`  `CURLOPT\_HTTP\_VERSION => CURL\_HTTP\_VERSION\_1\_1,

`  `CURLOPT\_CUSTOMREQUEST => 'POST',

`  `CURLOPT\_POSTFIELDS =>'{

`  `"list": [

`    `{

`      `"service\_id": "EP-CS0IW",

`      `"collection\_date": "2024-10-22",

`       `"weight": 0.5,

`        `"height": 10,

`        `"length": 10,

`        `"width": 10,

`      `"item": [

`        `{

`          `"content": "Electronics",

`          `"weight": 0.5,

`          `"height": 100,

`          `"length": 100,

`          `"width": 100,

`          `"currency\_code": "MYR",

`          `"value": 200,

`          `"quantity": 1,

`          `"insurance\_purchase":{

`                `"insurance\_service\_id":23,

`                `"invoices": "https://ep-website-media.s3.ap-southeast-1.amazonaws.com/my/wp-content/uploads/2024/02/sf-express-exd.webp",

`                `"photos": "https://s3-ap-southeast-1.amazonaws.com/easyparcel/Public/source/general/img/couriers/DHLeC.jpg"

`            `}

`        `},

`        `{

`          `"content": "Electronics 2",

`          `"weight": 0.7,

`          `"height": 120,

`          `"length": 100,

`          `"width": 100,

`          `"currency\_code": "MYR",

`          `"value": 500,

`          `"quantity": 1,

`          `"insurance\_purchase":{

`                `"insurance\_service\_id":23,

`                `"invoices": "https://ep-website-media.s3.ap-southeast-1.amazonaws.com/my/wp-content/uploads/2024/02/sf-express-exd.webp"

`            `}

`        `}

`      `],

`      `"origin": {

`        `"name": "John Doe",

`        `"company": "ABC Corp",

`        `"phone\_number\_country\_code": "+60",

`        `"phone\_number": "1163642281",

`        `"email": "weikeong.liew@easyparcel.com",

`        `"address\_1": "123 Main St",

`        `"address\_2": "Apt 4B",

`        `"postcode": "11900",

`        `"town": "Lunas",

`        `"province\_code": "MY-07",

`        `"country\_code": "MY"

`      `},

`      `"destination": {

`        `"name": "Jane Smith",

`        `"company": "XYZ Inc",

`        `"phone\_number\_country\_code": "+60",

`        `"phone\_number": "1163642281",

`        `"email": "weikeong.liew@easyparcel.com",

`        `"address\_1": "456 High St",

`        `"address\_2": "Floor 2",

`        `"postcode": "11900",

`        `"town": "Bayan Lepas",

`        `"province\_code": "MY-07",

`        `"country\_code": "MY",

`        `"notification": {

`          `"sms": {

`            `"enable": true

`          `},

`          `"email": {

`            `"enable": true

`          `},

`          `"whatsapp": {

`            `"enable": true

`          `}

`        `}

`      `},

`      `"awb\_branding": {

`        `"enable": true

`      `}



`    `}

`  `]

}',

`  `CURLOPT\_HTTPHEADER => array(

`    `'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJhcHAiOnsiY2xpZW50X2lkIjoiNjU3MzEyOTYtMzkzZi00MmJjLTllNTktY2E5NjcyYmViNmY2In0sInVzZXIiOnsiaWQiOiI0ZTAyMTA1YzQ2NmNmYzg4Y2U4MmQ2NTEwMGI0YzBhZEptbnJDT1hSNmV6UHRtSFUyWkNyYmc9PSIsImVhc3lfYWNjb3VudF9pZCI6IjA5ZjcxMjc5LTBjMGItNDcxOS05OTM5LWMwMzVjYWVlYzYxOSIsImFjY291bnRfaWQiOiI4NzIwNjYwIn0sImlhdCI6MTczMTg5OTM0MCwiaXNzIjoiZWFzeXBhcmNlbCIsImF1ZCI6ImVhc3lwYXJjZWwiLCJleHAiOjE3MzE5MzUzNDB9.S2yUdWfzIPZETtQhvc9dRmtVq8Wz\_HBNDU5N-VJFblU',

`    `'Content-Type: application/json',

`    `'Cookie: XSRF-TOKEN=eyJpdiI6InhzeWxGNlVETzhsZVhaZy9PRDFOZWc9PSIsInZhbHVlIjoicmY1eWd2YVh4bWxjVjNiNGNJSzcvU3hCckd5SlNIQ0JuQW1WdmVpM090dmE2ckdQdEJEN1JvU3Z3eTNXdWpzL1RMNzhzK2E3QWFmc3JIM3RaWnQ0dDA4N2k2TFg0NEcrZ0hwRlBLVWtFODlJdVl0dm04TmR6Z2h2YUpTdkQ2MCsiLCJtYWMiOiJhZTBkYjU0OGE2NWI4NmRkNzFiYzZhYmYyZjIzNmJkMjc1OWMzM2Q3MGYwZTgzNzY0MTM4ZjMwZGY5MDE4ODQwIiwidGFnIjoiIn0%3D; easyparcel\_delivery\_developer\_session=bMPA9PgT6xH8Fk1hYFxoIKPuoFvKqU1WSUNV0Epe'

`  `),

));

$response = curl\_exec($curl);

curl\_close($curl);

echo $response;


**Get OnDemand Quotation**

Parameters used:

"schedule\_pickup\_date": "2024-11-30",

"schedule\_pickup\_time": "11:48:35",

"timezone": "Asia/Kuala\_Lumpur",

"waypoint\_list": [

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

<?php

$curl = curl\_init();

curl\_setopt\_array($curl, array(

`  `CURLOPT\_URL => 'http://localhost:8023/open\_api/ondemand/quotation',

`  `CURLOPT\_RETURNTRANSFER => true,

`  `CURLOPT\_ENCODING => '',

`  `CURLOPT\_MAXREDIRS => 10,

`  `CURLOPT\_TIMEOUT => 0,

`  `CURLOPT\_FOLLOWLOCATION => true,

`  `CURLOPT\_HTTP\_VERSION => CURL\_HTTP\_VERSION\_1\_1,

`  `CURLOPT\_CUSTOMREQUEST => 'POST',

`  `CURLOPT\_POSTFIELDS =>'{

`    `"schedule\_pickup\_date": "2024-11-30",

`    `"schedule\_pickup\_time": "11:48:35",

`    `"timezone": "Asia/Kuala\_Lumpur",

`    `"waypoint\_list": [

`        `{

`            `"coordinates": {

`                `"latitude": 5.342720241204454,

`                `"longitude": 100.28204988381822

`            `},

`            `"address": "Kawasan Mendaki Bukit Jambul, Lintang Bukit Jambul 1, Bukit Jambul Indah, Bayan Lepas, Mukim 13 Paya Terubong, 11900, Timur Laut, Pulau Pinang, Malaysia",

`            `"type": "pickup"

`        `},

`        `{

`            `"coordinates": {

`                `"latitude": 5.325513957,

`                `"longitude": 100.2862732

`            `},

`            `"address": "Suntech @ Penang Cybercity, 1, Lintang Mayang Pasir 3, Bandar Bayan Baru, Bayan Lepas, Mukim 12 Bayan Lepas, 11950, Barat Daya, Pulau Pinang, Malaysia",

`            `"type": "dropoff"

`        `}

`    `]

}',

`  `CURLOPT\_HTTPHEADER => array(

`    `'Content-Type: application/json'

`  `),

));

$response = curl\_exec($curl);

curl\_close($curl);

echo $response;


**Submit OnDemand Order**

Parameters used:

"from\_country": "MY",

"ondemand\_service\_id": 3,

"waypoint\_list": [

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

"phone\_number\_country\_code": "MY",

"phone\_number": "1278491622",

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

"phone\_number\_country\_code": "MY",

"phone\_number": "127491622",

"address": "Terminal 1 Departure - Changi Airport, 80 Airport Boulevard, Singapore, 819642",

"remark": "222"

}

],

"schedule\_pickup\_date": "2024-12-10",

"schedule\_pickup\_time": "17:35:15",

"timezone": "Asia/Kuala\_Lumpur",

"metadata": {

"quotationId": "3114850556997669249"

}

<?php

$curl = curl\_init();

curl\_setopt\_array($curl, array(

`  `CURLOPT\_URL => 'http://localhost:8023/open\_api/ondemand/order',

`  `CURLOPT\_RETURNTRANSFER => true,

`  `CURLOPT\_ENCODING => '',

`  `CURLOPT\_MAXREDIRS => 10,

`  `CURLOPT\_TIMEOUT => 0,

`  `CURLOPT\_FOLLOWLOCATION => true,

`  `CURLOPT\_HTTP\_VERSION => CURL\_HTTP\_VERSION\_1\_1,

`  `CURLOPT\_CUSTOMREQUEST => 'POST',

`  `CURLOPT\_POSTFIELDS =>'

{

`    `"from\_country": "MY",

`    `"ondemand\_service\_id": 3,

`    `"waypoint\_list": [

`        `{

`            `"order": 0,

`            `"coordinates": {

`                `"latitude": 5.342720241204454,

`                `"longitude": 100.28204988381822

`            `},

`            `"type": "pickup",

`            `"firstName": "111",

`            `"email": "as@as.as",

`            `"package": [

`                `{

`                    `"quantity": "1",

`                    `"description": "1",

`                    `"dimensions": {

`                        `"height": "1",

`                        `"width": "1",

`                        `"length": "1",

`                        `"weight": "1"

`                    `}

`                `}

`            `],

`            `"phone\_number\_country\_code": "MY",

`            `"phone\_number": "1278491622",

`            `"address": "L1 Lobby, Suntec City Tower 1 & 2, 7 Temasek Boulevard, Singapore, 038987",

`            `"remark": "1"

`        `},

`        `{

`            `"order": 1,

`            `"coordinates": {

`                `"latitude": 5.325513957,

`                `"longitude": 100.2862732

`            `},

`            `"type": "dropoff",

`            `"firstName": "222",

`            `"email": "as@as.as",

`            `"package": [

`                `{

`                    `"quantity": "2",

`                    `"description": "2",

`                    `"dimensions": {

`                        `"height": "2",

`                        `"width": "2",

`                        `"length": "2",

`                        `"weight": "2"

`                    `}

`                `}

`            `],

`            `"phone\_number\_country\_code": "MY",

`            `"phone\_number": "127491622",

`            `"address": "Terminal 1 Departure - Changi Airport, 80 Airport Boulevard, Singapore, 819642",

`            `"remark": "222"

`        `}

`    `],

`    `"schedule\_pickup\_date": "2024-12-10",

`    `"schedule\_pickup\_time": "17:35:15",

`    `"timezone": "Asia/Kuala\_Lumpur",

`    `"metadata": {

`        `"quotationId": "3114850556997669249"

`    `}

}',

`  `CURLOPT\_HTTPHEADER => array(

`    `'Content-Type: application/json'

`  `),

));

$response = curl\_exec($curl);

curl\_close($curl);

echo $response;


