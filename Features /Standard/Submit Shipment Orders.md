### Submit Shipment Orders
Submit Shipment Orders: This features enables users to submit the shipment orders. Users are required to fill in the necessary fields to access the insurance rate information.

#### [Feature/Endpoints](../README.md)  |  [Back to official documentation](../../README.md) 

#### Endpoint URL: 
`https://api.easyparcel.com/shipment/submit_orders`

### [Request](#Requested-Parameters)  |  [Return](#Returned-Parameters) 

#### Requested Parameters

| Requested Parameters | Type        | Required | Description                                                                 |
| -------------------- | ----------- | -------- | --------------------------------------------------------------------------- |
| service_id           | string(10)  | Yes      | Service Identification number                                               |
| collection_date      | date        | Yes      | Date to collect the parcel                                                  |
| weight               | double(8,2) | Yes      | Weight of the parcel                                                        |
| height               | double(8,2) | Yes      | Height of the parcel                                                        |
| length               | double(8,2) | Yes      | Length of the parcel                                                        |
| width                | double(8,2) | Yes      | Width of the parcel                                                         |
| item                 | array       | Yes      | Item of the parcel (refer to [item](#items))                                |
| Origin               | array       | Yes      | Origin of the parcel (refer to [origin](#Origin))                           |
| Destination          | array       | Yes      | Destination of the parcel to sent to (refer to [destination](#destination)) |
| awb_branding         | array       | Yes      | Airway bill branding(refer to [awb_branding](#awb_branding))                |

###### Origin

| Requested Parameters      | Type      | Required | Description                                        |
| ------------------------- | --------- | -------- | -------------------------------------------------- |
| name                      | string    | Yes      | Sender's Name                                      |
| company                   | string    | Yes      | Sender's Company                                   |
| phone_number_country_code | string    | Yes      | (refer to [Country Code](../../References/Country%20Code.md))           |
| phone_number              | string    | Yes      | Sender's phone number                              |
| email                     | string    | Yes      | Sender's email                                     |
| address_1                 | string    | Yes      | Sender's address                                   |
| address_2                 | string    | Yes      | Sender's address                                   |
| postcode                  | string    | Yes      | Sender's postcode                                  |
| town                      | string    | Yes      | Sender's town area                                 |
| province_code             | string    | Yes      | Sender's province (refer to [ISO 3166](../References/ISO%203166.md)) |
| country_code              | string(2) | Yes      | (refer to [Country Code](../../References/Country%20Code.md))           |

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
| province_code             | string    | Yes      | Receiver's province (refer to (refer to [ISO 3166](../../References/ISO%203166.md))                        |
| country_code              | string(2) | Yes      | Receiver's country code(refer to [Country Code](../../References/Country%20Code.md))             |
| Notification              | array     | Yes      | Notifications of the parcel status (refer to [Notification](#Notification)) |

###### awb_branding

| Requested Parameters | Type    | Required | Description                                 |
| -------------------- | ------- | -------- | ------------------------------------------- |
| enable               | boolean | Yes      | To enable or disable Airways Bills Branding |


###### Items

| Requested Parameters | Type        | Required | Description                                                                      |
| -------------------- | ----------- | -------- | -------------------------------------------------------------------------------- |
| content              | string      | Yes      | Description of the content                                                       |
| currency_code        | string (3)  | Yes      | The currency code of the parcel content.                                         |
| value                | double(8,2) | Yes      | Value of the parcel                                                              |
| quantity             | int         | Yes      | The parcel quantity                                                              |
| Insurance_purchase   | array       | Yes      | Purchased Insurance details (refer to [insurance purchase](#Insurance-purchase)) |


###### Notification

| Requested Parameters | Type  | Required | Description                                                                             |
| -------------------- | ----- | -------- | --------------------------------------------------------------------------------------- |
| sms                  | array | Yes      | status of enabling sms notification of the parcel (refer to [sms](#sms))                |
| email                | array | Yes      | status of enabling email notification of the parcel (refer to [email](#email))          |
| whatsapp             | array | Yes      | status of enabling whatsapp notification of the parcel (refer to [whatsapp](#whatsapp)) |



###### Insurance purchase
| Requested Parameters | Type   | Required | Description              |
| -------------------- | ------ | -------- | ------------------------ |
| insurance_service_id | string | Yes      | insurance service number |
| invoices             | string | Yes      | links to the invoices    |
| photos               | string | Yes      | Image location           |


##### sms
| Requested Parameters | Type    | Required | Description                                         |
| -------------------- | ------- | -------- | --------------------------------------------------- |
| enable               | boolean | Yes      | To enable or disable sms notification of the parcel |

##### email

| Requested Parameters | Type    | Required | Description                                           |
| -------------------- | ------- | -------- | ----------------------------------------------------- |
| enable               | boolean | Yes      | To enable or disable email notification of the parcel |

##### whatsapp

| Requested Parameters | Type    | Required | Description                                              |
| -------------------- | ------- | -------- | -------------------------------------------------------- |
| enable               | boolean | Yes      | To enable or disable whatsapp notification of the parcel |


Request Sample Code:
```
{
  "list": [
    {
      "service_id": "EP-CS0R",
      "collection_date": "2024-10-02",
       "weight": 2.5,
        "height": 30,
        "length": 40,
        "width": 20,
      "item": [
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
      "origin": {
        "name": "John Doe",
        "company": "ABC Corp",
        "phone_number_country_code": "+60",
        "phone_number": "1163642281",
        "email": "weikeong.liew@easyparcel.com",
        "address_1": "123 Main St",
        "address_2": "Apt 4B",
        "postcode": "09600",
        "town": "Lunas",
        "province_code": "MY-02",
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
        "postcode": "11950",
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
            "enable": false
          }
        }
      },
      "awb_branding": {
        "enable": true
      }
   
    },

    {
      "service_id": "EP-CS0R",
      "collection_date": "2024-10-03",
       "weight": 0.5,
        "height": 30,
        "length": 40,
        "width": 20,
      "item": [
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
      "origin": {
        "name": "JWK 1",
        "company": "ABC Corp",
        "phone_number_country_code": "+60",
        "phone_number": "1163642281",
        "email": "weikeong.liew@easyparcel.com",
        "address_1": "123 Main St",
        "address_2": "Apt 4B",
        "postcode": "11950",
        "town": "Bayan Baru",
        "province_code": "MY-07",
        "country_code": "MY"
      },
      "destination": {
        "name": "WK 2",
        "company": "XYZ Inc",
        "phone_number_country_code": "+60",
        "phone_number": "1163642281",
        "email": "weikeong.liew@easyparcel.com",
        "address_1": "456 High St",
        "address_2": "Floor 2",
        "postcode": "09600",
        "town": "Lunas",
        "province_code": "MY-02",
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
}
```

---


#### Returned parameters

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

| Returned Parameters                          | Type       | Description                                                                       |
| -------------------------------------------- | ---------- | --------------------------------------------------------------------------------- |
| uuid                                         | string(25) | Uuid of the shipment                                                              |
| courier_service                              | string     | The courier service and type selected for the shipment                            |
| courier                                      | string     | Name of the courier service                                                       |
| currency_code                                | string     | Currency use for the shipment                                                     |
| total_amount                                 | double     | The shipment amount / price of this particular shipments                          |
| credit_applied                               | double     | Credit applied for this particular shipment                                       |
| free_credit_applied                          | double     | Free credit applied for this particular shipment                                  |
| shipment_price                               | double     | Price of this particular shipment                                                 |
| tax_amount                                   | double     | Tax amount of this particular shipment                                            |
| collection_date                              | date       | Collection date of the parcel                                                     |
| tracking_status                              | int        | The tracking status of the parcel                                               |
| awb_url                                      | string     | The url to access the airway bill                                                 |
| awb_number                                   | string     | The airway bill number                                                            |
| tracking_url                                 | string     | The url to tracking the parcel                                                    |
| shipment_number                              | string     | The unique number of the shipment                                                 |
| sender_point_code                            | string     | A unique identifier for the sender's location                                     |
| sender_name                                  | string     | Name of the sender                                                                |
| sender_phone_number_country_code             | string     | The country code of the phone of the sender                                       |
| sender_phone_number                          | string     | Phone number of the sender                                                        |
| sender_alternate_phone_number                | string     | Alternate phone number of the sender                                              |
| sender_alternate_phone_number_country_code   | string     | Alternate the country code of the phone of the sender                             |
| sender_email                                 | string     | Sender's Email                                                                    |
| sender_company_name                          | string     | Sender's Company Name                                                             |
| sender_address1                              | string     | Sender's Address 1                                                                |
| sender_address2                              | string     | Sender's Address 2                                                                |
| sender_city                                  | string     | Sender's city                                                                     |
| sender_province_code                         | string     | Sender's province (refer to [ISO 3166](../../References/ISO%203166.md))             |
| sender_postcode                              | string     | Sender's post code                                                                |
| sender_country_code                          | string     | Sender's country code (refer to [Country Code](../../References/Country%20Code.md)) |
| receiver_point_code                          | string     | A unique identifier for the sender's location                                     |
| receiver_name                                | string     | Name of the receiver                                                              |
| receiver_phone_number_country_code           | string     | The country code of the phone of the receiver                                     |
| receiver_phone_number                        | string     | Phone number of the receiver                                                      |
| receiver_alternate_phone_number              | string     | Alternate phone number of the receiver                                            |
| receiver_alternate_phone_number_country_code | string     | Alternate the country code of the phone of the receiver                           |
| receiver_email                               | string     | Receiver's Email                                                                  |
| receiver_company_name                        | string     | Receiver's Company Name                                                           |
| receiver_address1                            | string     | Receiver's Address 1                                                              |
| receiver_address2                            | string     | Receiver's Address 2                                                              |
| receiver_city                                | string     | Receiver's city                                                                   |
| receiver_province_code                       | string     | Sender's province (refer to [ISO 3166](../../References/ISO%203166.md))                                 |
| receiver_postcode                            | string     | Sender's post code                                                                |
| receiver_country_code                        | string     | Sender's country code (refer to [Country Code](../../References/Country%20Code.md))                  |
| cod                                          | string     | Cash on delivery status                                                           |
| weight                                       | double     | Weight of the  shipment                                                           |
| height                                       | double     | Height of the shipment parcels                                                    |
| lenght                                       | double     | Lenght of the particular shipment                                                 |
| width                                        | double     | Width of the particular shipment                                                  |
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

Return Sample:
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
