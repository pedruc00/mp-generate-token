### mp-generate-token

This guide walks you through setting up and running the mp-generate-token application. 
With this app, you can generate and retrieve access tokens for API integration. 
Let’s get started!

#### Setup Steps

##### Generate a Private Key
Navigate to the ./certs directory and create a private key named private.pem. Use one of the following commands, 
depending on your operating system:

###### Mac/Linux: (Ensure the key is at least 2048 bits for security.)
```
openssl genrsa -out private.pem 3072
```

###### Windows: (Save the key as private.pem.)
```
ssh-keygen -t rsa -b 3072
```

#### Install and Run the Application
Move into the app directory and install dependencies:
```shell
cd app
npm install
```

#### Start the development server:
```shell
npm run dev
```
By default, the application will run at http://localhost:4000.

#### How to Use

##### Step 1: Retrieve the JWKS
Visit http://localhost:4000/jwks to fetch the public JWKS. This is required for configuration in the selvbetjeningsportalen.


##### Step 2: Generate a JWT Token
Navigate to http://localhost:4000/jwt_token to generate the JWT token you’ll use to request an access token.

##### Step 3: Exchange JWT for Access Token
Use the JWT token from the previous step to request an access token. Here’s an example using curl:
```shell
curl -d "grant_type=urn:ietf:params:oauth:grant-type:jwt-bearer&assertion={jwt-token-from-step-2}" \
     -H "Content-Type: application/x-www-form-urlencoded" \
     -X POST https://ver2.maskinporten.no/token
```

##### Step 4: Access the API
With the access token in hand, connect to the API. Here’s an example request:
```shell
curl -X GET https://<API-ENDPOINT>/tildelinger/v1 \
     -H "Authorization: Bearer {accessToken}"
```

If everything is set up correctly, you’ll get a warm welcome from the API. 😊

###### Notes
* API Endpoint: Replace <API-ENDPOINT> with the actual API URL you’re integrating with.
* Postman Option: If you prefer GUI tools, you can use Postman to send the same requests.


