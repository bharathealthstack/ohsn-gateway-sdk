To get started, the following flows have to be implemented and tested.

### [API Docs for OHSN Gateway](https://documenter.getpostman.com/view/1963101/Szmh3chd?version=latest)

### 1. Register

Endpoint: `POST /register/app`
```javascript
{
    "name": "New HSP", //Required
    "type": "HSP", //Required: Accepted values - HSP, EUA
    "email": "<Email ID for the HSP>",
    "username": "new_hsp", //Required
    "password": "newhsp@123", //Required
    "phone": "<Phone Number>",
    "supported_channels": [{"name": "<channel>"}], //Required: Accepted values for channel - phone, video, chat
    "endpoints": [
        {
            "type": "base",
            "url": "<base URL>" //Required: The base URL of the endpoints that can be used to reach the app
        }
    ]
}
```

### 2. Login

Once registered, the app has to use the `username` and `password` and implement login on its end to interact with the gateway.

Endpoint: `POST /login/app`
```javascript
{
    "username": "new_hsp", //Required
    "password": "newhsp@123", //Required
}
```

### 3. Refresh Access Token

The app have to use the `refreshtoken` to refresh the token.

Endpoint: `POST /refresh-accesstoken/app`
```javascript
{
    "refreshtoken": "<JWT>" //Required
}
```

### 4. Refresh API Token

The app have to pass a valid `accesstoken` to refresh the API token.

Endpoint: `POST /refresh-apitoken/app`
```curl
--header 'accesstoken: <JWT>'
```

### 5. Get Public Key

The public key of the gateway is exposed via an API so that the apps can use it to validate tokens sent while interacting with other apps.

Endpoint: `POST /refresh-apitoken/app`

### 6. Update App

The app have to pass a valid `accesstoken` to refresh the API token.

Endpoint: `POST /update/app`
```javascript
// Parameters of the app that needs to be updated.
{
    "serviceable": true,
    "id": 1
}
```

### 6. Search API

If you are an EUA, this API is what you would use to get available service providers for a service.
If you are a HSP, you would have already built a `search` API and once you are registered and `serviceable`, 
this endpoint hits the search API using the base endpoint given while registering the app.

Endpoint: `POST /search/app`
Please refer to the [architecture document](https://docs.google.com/document/d/1ljqmCiel8UCdPXC2OZNabhW-7WLJMh6hFsVTDRVGRDQ/edit?usp=sharing) for contract


### 6. Dry Run API

If you are an EUA, please stay tuned for updates on support for this endpoint.
If you are a HSP, you can use this endpoint to validate your search response and Token management/

Endpoint: `POST /onboard/dryrun`
Payload will be same as the expected payload on the search API.
