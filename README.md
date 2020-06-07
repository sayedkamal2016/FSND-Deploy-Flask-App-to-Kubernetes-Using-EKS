# Deploying a Flask API

This is the project repo for the Fullstack Developer Nanodegree Project 4: Server Deployment, Containerization, and Testing.

API endpoint: [http://a4d5c5647129311ea8d420a22cf9d500-2039112863.eu-west-1.elb.amazonaws.com/](http://a4d5c5647129311ea8d420a22cf9d500-2039112863.eu-west-1.elb.amazonaws.com/)

The Flask app that will be used for this project consists of a simple API with three endpoints:

- `GET '/'`: This is a simple health check, which returns the response 'Healthy'. 
- `POST '/auth'`: This takes a email and password as json arguments and returns a JWT based on a custom secret.
- `GET '/contents'`: This requires a valid JWT, and returns the un-encrpyted contents of that token. 

There is a Postman Collection in the file: udacity-eks.postman_collection.json 


To run the three end point: 


1- GET '/': This is a simple health check, which returns the response 'Healthy'.



2- To try the /auth endpoint, use the following command:
    export TOKEN=`curl -d '{"email":"<EMAIL>","password":"<PASSWORD>"}' -H "Content-Type: application/json" -X POST localhost:8080/auth  | jq -r '.token'`

This calls the endpoint 'localhost:8080/auth' with the {"email":"<EMAIL>","password":"<PASSWORD>"} as the message body. The return value is a JWT token based on the secret you supplied. We are assigning that secret to the environment variable 'TOKEN'. To see the JWT token, run:

echo $TOKEN


3- To try the /contents endpoint which decrypts the token and returns its content, run:

curl --request GET 'http://127.0.0.1:8080/contents' -H "Authorization: Bearer ${TOKEN}" | jq .


