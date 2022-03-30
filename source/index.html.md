---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - javascript
  - python

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  # - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the Cari API
---

# Introduction

Welcome to the Cari API! You can use our API to access Cari API endpoints, which can get information on identity, finance, and data.

We have language bindings in Shell, JavaScript, and Python! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

<!-- This example API documentation page was created with [Slate](https://github.com/slatedocs/slate). Feel free to edit it and use it as a base for your own API's documentation. -->

<!-- # Authentication

> To authorize, use this code:

```python
import Cari
api = Cari.authorize('dev_2dad33a9-03ea-43ee-aac9-ee182fd4ec23')
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here" \
  -H "Authorization: dev_2dad33a9-03ea-43ee-aac9-ee182fd4ec23"
```

```javascript
const Cari = require("Cari");
let api = Cari.authorize("dev_2dad33a9-03ea-43ee-aac9-ee182fd4ec23");
``` -->

> Make sure to replace `dev_2dad33a9-03ea-43ee-aac9-ee182fd4ec23` with your API key.

Cari uses API keys to allow access to the API. You can register a new Cari API key at our [developer portal](http://example.com/developers).

Cari expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: dev_2dad33a9-03ea-43ee-aac9-ee182fd4ec23`

<aside class="notice">
You must replace <code>dev_2dad33a9-03ea-43ee-aac9-ee182fd4ec23</code> with your personal API key.
</aside>

# Identity

## Create new KYC verification

```python
import requests

url = "https://dev.cari.finance/identity/verify/"

payload={'type': 'passport'}
files=[
  ('selfie',('selfie.jpeg',open('/path/to/selfie/selfie.jpeg','rb'),'image/jpeg')),
  ('front',('passport-2.jpeg',open('/path/to/passport/passport.jpeg','rb'),'image/jpeg')),
  ('back',('file',open('/path/to/passport/passport.jpeg','rb'),'image/jpeg'))
]
headers = {
  'Authorization': 'dev_2dad33a9-03ea-43ee-aac9-ee182fd4ec23'
}

response = requests.request("POST", url, headers=headers, data=payload, files=files)

print(response.text)
```

```shell
curl  --location --request POST "https://dev.cari.finance/identity/verify/" \
--header "Authorization: dev_2dad33a9-03ea-43ee-aac9-ee182fd4ec23" \
--form "type=\"passport\"" \
--form "selfie=@\"/path/to/selfie/selfie.jpeg\"" \
--form "front=@\"/path/to/passport/passport.jpeg\""
```

```javascript
const headers = new Headers();
headers.append("Authorization", "dev_2dad33a9-03ea-43ee-aac9-ee182fd4ec23");

const formdata = new FormData();
formdata.append("type", "passport");
formdata.append("selfie", fileInput.files[0], "/path/to/selfie/selfie.jpeg");
formdata.append("front", fileInput.files[0], "/path/to/passport/passport.jpeg");
formdata.append("back", fileInput.files[0], "/path/to/passport/passport.jpeg");

const requestOptions = {
  method: "POST",
  headers: headers,
  body: formdata,
  redirect: "follow",
};

fetch("https://dev.cari.finance/identity/verify/", requestOptions)
  .then((response) => response.text())
  .then((result) => console.log(result))
  .catch((error) => console.log("error", error));
```

> The above command returns JSON structured like this:

```json
{
  "type": "passport",
  "user": "62052d9572ad48000c1f1f4f",
  "selfie": {
    "SourceImageFace": {
      "topLeftX": 196,
      "topLeftY": 344,
      "width": 174,
      "height": 224,
      "confidence": 0.99933
    },
    "MatchedFaces": [
      {
        "chinTipX": 485,
        "rightEyeCenterX": 590,
        "yaw": 5,
        "chinTipY": 1006,
        "rightEyeCenterY": 595,
        "leftEyeCenterY": 610,
        "leftEyeCenterX": 365,
        "pitch": 2,
        "quality": 1.08989,
        "roll": -3,
        "eyeDistance": 225,
        "topLeftX": 244,
        "topLeftY": 381,
        "width": 489,
        "height": 616,
        "confidence": 1,
        "similarity": 0.748,
        "attributes": {
          "lips": "Together",
          "glasses": "Eye"
        },
        "face_id": 1
      }
    ],
    "UnmatchedFaces": []
  },
  "front": {
    "mrz_type": "TD3",
    "valid_score": 98,
    "raw_text": "P<U5AGEORGE<<KENVRQEQELEENED3 CT<<<<<<A<<<<<<<<<<\n5007686871USA88031 6 OM2 301 1 36254056095<082372",
    "type": "P<",
    "country": "USA",
    "number": "500768687",
    "date_of_birth": "840516",
    "expiration_date": "260115",
    "nationality": "USA",
    "sex": "M",
    "names": "KENROY BENEDICT",
    "surname": "GEORGE",
    "personal_number": "254056095<0823",
    "check_number": "1",
    "check_date_of_birth": "0",
    "check_expiration_date": "6",
    "check_composite": "2",
    "check_personal_number": "7",
    "valid_number": true,
    "valid_date_of_birth": true,
    "valid_expiration_date": true,
    "valid_composite": true,
    "valid_personal_number": true,
    "method": "black_tophat",
    "walltime": 3.776029348373413,
    "filename": "/app/photos/1646741109987-passport.jpeg"
  }
}
```

This endpoint retrieves all kittens.

### HTTP Request

`POST https://dev.cari.finance/identity/verify/`

### Query Parameters

| Parameter | Default | Description                                                 |
| --------- | ------- | ----------------------------------------------------------- |
| type      | card    | The type of identity document used for verification.        |
| selfie    | empty   | The destination of identity document used for verification. |
| front     | empty   | The destination of identity document used for verification. |
| back      | empty   | The destination of identity document used for verification. |

<!-- <aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside> -->

## Get a Specific Verification

```python
import requests

url = "https://dev.cari.finance/identity/verify/62052d9572ad48000c1f1f4d"

headers = {
  'Authorization': 'dev_2dad33a9-03ea-43ee-aac9-ee182fd4ec23'
}

response = requests.request("GET", url, headers=headers, data=payload, files=files)

print(response.text)
```

```shell
curl "https://dev.cari.finance/identity/verify/62052d9572ad48000c1f1f4d" \
  -H "Authorization: dev_2dad33a9-03ea-43ee-aac9-ee182fd4ec23"
```

```javascript
const headers = new Headers();
headers.append("Authorization", "dev_2dad33a9-03ea-43ee-aac9-ee182fd4ec23");

const requestOptions = {
  method: "GET",
  headers: headers,
  redirect: "follow",
};

fetch(
  "https://dev.cari.finance/identity/verify/62052d9572ad48000c1f1f4d",
  requestOptions
)
  .then((response) => response.text())
  .then((result) => console.log(result))
  .catch((error) => console.log("error", error));
```

> The above command returns JSON structured like this:

```json
{
  "type": "passport",
  "user": "62052d9572ad48000c1f1f4f",
  "selfie": {
    "SourceImageFace": {
      "topLeftX": 196,
      "topLeftY": 344,
      "width": 174,
      "height": 224,
      "confidence": 0.99933
    },
    "MatchedFaces": [
      {
        "chinTipX": 485,
        "rightEyeCenterX": 590,
        "yaw": 5,
        "chinTipY": 1006,
        "rightEyeCenterY": 595,
        "leftEyeCenterY": 610,
        "leftEyeCenterX": 365,
        "pitch": 2,
        "quality": 1.08989,
        "roll": -3,
        "eyeDistance": 225,
        "topLeftX": 244,
        "topLeftY": 381,
        "width": 489,
        "height": 616,
        "confidence": 1,
        "similarity": 0.748,
        "attributes": {
          "lips": "Together",
          "glasses": "Eye"
        },
        "face_id": 1
      }
    ],
    "UnmatchedFaces": []
  },
  "front": {
    "mrz_type": "TD3",
    "valid_score": 98,
    "raw_text": "P<U5AGEORGE<<KENVRQEQELEENED3 CT<<<<<<A<<<<<<<<<<\n5007686871USA88031 6 OM2 301 1 36254056095<082372",
    "type": "P<",
    "country": "USA",
    "number": "500768687",
    "date_of_birth": "840516",
    "expiration_date": "260115",
    "nationality": "USA",
    "sex": "M",
    "names": "KENROY BENEDICT",
    "surname": "GEORGE",
    "personal_number": "254056095<0823",
    "check_number": "1",
    "check_date_of_birth": "0",
    "check_expiration_date": "6",
    "check_composite": "2",
    "check_personal_number": "7",
    "valid_number": true,
    "valid_date_of_birth": true,
    "valid_expiration_date": true,
    "valid_composite": true,
    "valid_personal_number": true,
    "method": "black_tophat",
    "walltime": 3.776029348373413,
    "filename": "/app/photos/1646741109987-passport.jpeg"
  }
}
```

This endpoint retrieves a specific verification.

<!-- <aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside> -->

### HTTP Request

`GET https://dev.cari.finance/identity/verify/:verification_id`

### URL Parameters

| Parameter | Description                            |
| --------- | -------------------------------------- |
| ID        | The ID of the verification to retrieve |

<!-- ## Delete a Specific Verification

```python
import Cari

api = Cari.authorize('dev_2dad33a9-03ea-43ee-aac9-ee182fd4ec23')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2" \
  -X DELETE \
  -H "Authorization: dev_2dad33a9-03ea-43ee-aac9-ee182fd4ec23"
```

```javascript
const Cari = require("Cari");

let api = Cari.authorize("dev_2dad33a9-03ea-43ee-aac9-ee182fd4ec23");
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted": ":("
}
```

This endpoint deletes a specific verification.

### HTTP Request

`DELETE https://dev.cari.finance/identity/verify/:verification_id`

### URL Parameters

| Parameter | Description                    |
| --------- | ------------------------------ |
| ID        | The ID of the kitten to delete | -->
