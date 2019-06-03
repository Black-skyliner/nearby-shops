# Shopping

## Requirements

- PHP 7 or later
- Mysql 

## Getting Started
Clone this project using the following commands:

```
$ git clone https://github.com/Black-skyliner/nearby-shops.git

$ cd nearby-shops
```

### Set up the Backend
Use the package manager [composer](https://getcomposer.org/) to install the project dependencies.

```
$ cd symfony4

$ composer install
```

#### Configure .env file
Copy and edit the .env file and enter the credentials (Mysql User and password) there:

```
$ cp .env.dist .env
```

> DATABASE_URL=mysql://your_user:your_password@127.0.0.1:3306/nearby-shops

#### Create database
Create the database and tables.

```
$ php bin/console doctrine:database:create

$ php bin/console doctrine:schema:update --force
```
#### Generate fake data

```
$ php bin/console doctrine:fixtures:load --append
```

#### Run server
Start the internal server of PHP.

```
$ php -S 127.0.0.1:8000 -t public/
```

## Usage
To get the token use the following request.

```
CURL --header "Content-Type: application/json" --request POST --data {\"security\":{\"credentials\":{\"email\":\"demo@test.com\",\"password\":\"demo\"}},\"location\":{\"latitude\":\"-71.918303\",\"longitude\":\"30.897918\"}} http://127.0.0.1:8000/auth/login
```

Format of data sent to the API:

```json
{
    "security": {
        "credentials": {
            "email": "demo@test.com",
            "password": "demo"
        }
    },
    "location": {
        "latitude": "-71.918303",
        "longitude": "30.897918"
    }
}
```

Then use the token value in the following requests to get:
The list of nearby shops.

```
CURL --header "X-AUTH-TOKEN: Your_token" --request GET 127.0.0.1:8000/api/shop/list
```

The list of preferred shops.

```
CURL --header "X-AUTH-TOKEN: Your_token" --request GET 127.0.0.1:8000/api/shop/preferredList
```

Add a shop to the preferred list (ex. id = 1).

```
CURL --header "X-AUTH-TOKEN: Your_token" --request GET 127.0.0.1:8000/api/shop/1/like/
```

Remove a shop from the preferred list (ex. id = 1).

```
CURL --header "X-AUTH-TOKEN: Your_token" --request DELETE 127.0.0.1:8000/api/shop/1/remove
```

Dislike a shop (ex. id = 2).

```
CURL --header "X-AUTH-TOKEN: Your_token" --request GET 127.0.0.1:8000/api/shop/2/dislike
```

Register user

```
CURL --header "Content-Type: application/json" --request PUT --data {\"email\":\"demo1@test.com\",\"password\":\"demo\"} http://127.0.0.1:8000/auth/register
```

Format of data sent to the API:
```json
{
    "email": "demo1@test.com",
    "password": "demo"
}
```



