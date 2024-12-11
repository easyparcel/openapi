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

Parameters used:

| Requested Parameters | Type | Required | Description |
| -------------------- | ---- | -------- | ----------- |
| courier_id           |      |          |             |
| country_code         |      |          |             |
| postcode             |      |          |             |
| city                 |      |          |             |
| state_code           |      |          |             |

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




#### Country Code List

|Short Country Name|Full Country Name|
|:----|:----|
|SR|SURINAME|
|SD|SUDAN|
|VC|ST. VINCENT|
|XM|ST. MAARTEN|
|LC|ST. LUCIA|
|KN|ST. KITTS|
|XE|ST. EUSTATIUS|
|BL|ST. BARTHELEMY|
|LK|SRI LANKA|
|ES|SPAIN|
|ZA|SOUTH AFRICA|
|XS|SOMALILAND (NORTH SOMALIA)|
|SO|SOMALIA|
|SB|SOLOMON ISLANDS|
|SI|SLOVENIA|
|SK|SLOVAKIA|
|SG|SINGAPORE|
|SL|SIERRA LEONE|
|SC|SEYCHELLES|
|RS|SERBIA|
|SN|SENEGAL|
|SA|SAUDI ARABIA|
|ST|SAO TOME AND PRINCIPE|
|SM|SAN MARINO|
|WS|SAMOA|
|MP|SAIPAN|
|RW|RWANDA|
|RU|RUSSIAN FEDERATION|
|RO|ROMANIA|
|RE|REUNION|
|QA|QATAR|
|PR|PUERTO RICO|
|PT|PORTUGAL|
|PL|POLAND|
|PH|PHILIPPINES|
|PE|PERU|
|PY|PARAGUAY|
|PG|PAPUA NEW GUINEA|
|PA|PANAMA|
|PW|PALAU|
|PK|PAKISTAN|
|OM|OMAN|
|NO|NORWAY|
|NU|NIUE|
|NG|NIGERIA|
|NE|NIGER|
|NI|NICARAGUA|
|NZ|NEW ZEALAND|
|NC|NEW CALEDONIA|
|XN|NEVIS|
|NL|NETHERLANDS|
|NP|NEPAL|
|NR|NAURU|
|NA|NAMIBIA|
|MM|MYANMAR|
|MA|MOROCCO|
|MS|MONTSERRAT|
|ME|MONTENEGRO|
|MN|MONGOLIA|
|MC|MONACO|
|MD|MOLDOVA, REPUBLIC OF|
|FM|MICRONESIA, FEDERATED STATES OF|
|MX|MEXICO|
|YT|MAYOTTE|
|MU|MAURITIUS|
|MR|MAURITANIA|
|MQ|MARTINIQUE|
|MH|MARSHALL ISLANDS|
|MT|MALTA|
|ML|MALI|
|MV|MALDIVES|
|MW|MALAWI|
|MY|MALAYSIA|
|MG|MADAGASCAR|
|MK|MACEDONIA, THE FORMER YUGOSLAV REPUBLIC OF|
|MO|MACAU|
|LU|LUXEMBOURG|
|LT|LITHUANIA|
|LI|LIECHTENSTEIN|
|LY|LIBYA|
|LR|LIBERIA|
|LS|LESOTHO|
|LB|LEBANON|
|LV|LATVIA|
|LA|LAO PEOPLE'S DEMOCRATIC REPUBLIC|
|KG|KYRGYZSTAN|
|KW|KUWAIT|
|XK|KOSOVO|
|KR|KOREA, REPUBLIC OF|
|KP|KOREA, DEMOCRATIC PEOPLE'S REPUBLIC OF|
|KI|KIRIBATI|
|KE|KENYA|
|KZ|KAZAKHSTAN|
|JO|JORDAN|
|JE|JERSEY|
|JP|JAPAN|
|JM|JAMAICA|
|IT|ITALY|
|IL|ISRAEL|
|IE|IRELAND|
|IQ|IRAQ|
|IR|IRAN, ISLAMIC REPUBLIC OF|
|ID|INDONESIA|
|IN|INDIA|
|IS|ICELAND|
|HU|HUNGARY|
|HK|HONG KONG|
|HN|HONDURAS|
|HT|HAITI|
|GY|GUYANA|
|GW|GUINEA BISSAU|
|GN|GUINEA REPUBLIC|
|GG|GUERNSEY|
|GT|GUATEMALA|
|GU|GUAM|
|GP|GUADELOUPE|
|GD|GRENADA|
|GL|GREENLAND|
|GR|GREECE|
|GI|GIBRALTAR|
|GH|GHANA|
|DE|GERMANY|
|GE|GEORGIA|
|GM|GAMBIA|
|GA|GABON|
|ZW|ZIMBABWE|
|FR|FRANCE|
|FI|FINLAND|
|ZM|ZAMBIA|
|FJ|FIJI|
|YE|YEMEN|
|FO|FAROE ISLANDS|
|FK|FALKLAND ISLANDS (MALVINAS)|
|ET|ETHIOPIA|
|VI|VIRGIN ISLANDS, U.S.|
|EE|ESTONIA|
|VG|VIRGIN ISLANDS, BRITISH|
|ER|ERITREA|
|GQ|EQUATORIAL GUINEA|
|SV|EL SALVADOR|
|EG|EGYPT|
|VN|VIETNAM|
|EC|ECUADOR|
|TP|EAST TIMOR|
|VE|VENEZUELA|
|DO|DOMINICAN REPUBLIC|
|DM|DOMINICA|
|DJ|DJIBOUTI|
|VU|VANUATU|
|DK|DENMARK|
|CZ|CZECH REPUBLIC|
|CY|CYPRUS|
|CU|CUBA|
|UZ|UZBEKISTAN|
|UY|URUGUAY|
|HR|CROATIA|
|CI|COTE D'IVOIRE|
|CR|COSTA RICA|
|CK|COOK ISLANDS|
|CD|CONGO, THE DEMOCRATIC REPUBLIC OF THE|
|UM|UNITED STATES MINOR OUTLYING ISLANDS|
|CG|CONGO|
|KM|COMOROS|
|CN|CHINA|
|US|UNITED STATES|
|GF|FRENCH GUIANA|
|AN|NETHERLANDS ANTILLES|
|MZ|MOZAMBIQUE|
|CW|CURACAO|
|CO|COLOMBIA|
|CL|CHILE|
|TD|CHAD|
|CF|CENTRAL AFRICAN REPUBLIC|
|KY|CAYMAN ISLANDS|
|GB|UNITED KINGDOM|
|CV|CAPE VERDE|
|AE|UNITED ARAB EMIRATES|
|IC|CANARY ISLANDS, THE|
|CA|CANADA|
|UA|UKRAINE|
|CM|CAMEROON|
|KH|CAMBODIA|
|UG|UGANDA|
|BI|BURUNDI|
|BF|BURKINA FASO|
|BG|BULGARIA|
|BN|BRUNEI DARUSSALAM|
|TV|TUVALU|
|BR|BRAZIL|
|TC|TURKS AND CAICOS ISLANDS|
|TM|TURKMENISTAN|
|BW|BOTSWANA|
|BA|BOSNIA AND HERZEGOVINA|
|BQ|BONAIRE|
|BO|BOLIVIA|
|BT|BHUTAN|
|TR|TURKEY|
|BM|BERMUDA|
|TN|TUNISIA|
|BJ|BENIN|
|TT|TRINIDAD AND TOBAGO|
|BZ|BELIZE|
|TO|TONGA|
|BE|BELGIUM|
|TG|TOGO|
|BY|BELARUS|
|BB|BARBADOS|
|BD|BANGLADESH|
|BH|BAHRAIN|
|TH|THAILAND|
|BS|BAHAMAS|
|TZ|TANZANIA|
|AZ|AZERBAIJAN|
|TJ|TAJIKISTAN|
|AT|AUSTRIA|
|AU|AUSTRALIA|
|TW|TAIWAN|
|PF|TAHITI|
|AW|ARUBA|
|AM|ARMENIA|
|SY|SYRIA|
|AR|ARGENTINA|
|AG|ANTIGUA|
|AI|ANGUILLA|
|CH|SWITZERLAND|
|AO|ANGOLA|
|AD|ANDORRA|
|SE|SWEDEN|
|AS|AMERICAN SAMOA|
|SZ|SWAZILAND|
|DZ|ALGERIA|
|AL|ALBANIA|
|AF|AFGHANISTAN|

