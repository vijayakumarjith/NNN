# Instamojo NodeJS Wrapper

Official Node.JS wrapper for [Instamojo APIs](https://docs.instamojo.com/v2/docs/overview-and-setup-1).

## Installation
If you are using NPM as your package manager, run

> npm i @instamojo/retail

If you are using YARN as your package manager, run

> yarn i @instamojo/retail

## Initialisation
You need to load the default Instamojo class from "@instamojo/retail" package
    
    const  Instamojo = require('@instamojo/retail')
    
    const mojo = new Instamojo({
	    sandbox :  true,
		client_id :  'XXXX',
		client_secret : 'XXXX'
	})
  
  ### Options
  
| Key | Type | Description | Default |
|--|--|--|--|
|**sandbox**|Boolean|Pass "**true**" if you want to test the integration, "**false**" for production| false |
| **client_id**  | String | Alphanumeric value, unique for every client and environment | undefined |
| **client_secret** | String | Alphanumeric value, unique for every client and environment	| undefined |


## APIs Available
We currently provide for the support of the following modules:
 - Authenticate
 - Payments
 - Refunds
 - Orders

### Authentication V2
To use any of the modules, you need to make sure that you have the authentication token

    // intialization code here...
    mojo.authenticate()
	    .then(mojo => {
		    // do your task here
	    })
	    .catch(mojo => {
		    // handle exception here
	    })

#### Options
*No arguments*

--- 
### Payments
#### Create Payment Request
This will create a payment request on Instamojo.

    mojo.payments.createRequest({
	    // params here
    }, (err, res) => {
	    if (err) {
		    console.log(err)
		    return
		}
		// do your task here
    })

#### Get Payment Request Detail
This will fetch the details of a payment request.

    mojo.payments.getRequest({
	    request_id: 'xxxx-xxxx',
    }, (err, res) => {
    	if (err) {
		    console.log(err)
		    return
		}
		// do your task here
	})

##### Options

| Key  | Type | Description | Default |
|--|--|--|--|
| **request_id** | String | Unique Identifier for the payment request | undefined |


#### Get Payment Detail
This will fetch the details of a payment.

    mojo.payments.getDetails({
	    payment_id: 'xxxx-xxxx'
	}, (err, res) => {
		if (err) { 
			console.log(err)
			return
		}
		// do your task here
	})
	
##### Options

| Key  | Type | Description | Default |
|--|--|--|--|
| **payment_id** | String | Unique Identifier for the payment | undefined |

#### Get Payments List
This will fetch the list of payments.

    mojo.payments.list({
		limit: 10,
		page: 1
	}, (err, res) => {
		if (err) { 
			console.log(err)
			return
		}
		// do your task here
	})

##### Options
| Key  | Type | Description | Default |
|--|--|--|--|
| **limit** | Integer | Number of records to fetch at a time | undefined |
| **page** | Integer | Page Number to get nth records | undefined |

--- 
### Refunds
#### Create Refund for a Payment
Use this to create refund for a payment

    mojo.refunds.create({
	    payment_id :  'xxxx-xxxx',
	    type :  'TNR',
	    refund_amount :  '1',
	    transaction_id:  'aaaa-bbbb',
	    body :  'Some refund cause'
    }, (err, res) => {
		if (err) { 
			console.log(err)
			return
		}
		// do your task here
    })

##### Options
| Key  | Type | Description | Default |
|--|--|--|--|
| **payment_id** | String | Unique Identifier for the payment | undefined |
| **type** | String | A three letter short-code identifying the reason for this case [See Codes Here](https://docs.instamojo.com/v2/docs/create-a-refund-1) | undefined |
| **body** | String | Short description for refund cause | undefined |
| **refund_amount** | String (in Rupees) | This field can be used to specify the refund amount. Can be less than the payment amount | undefined |
| **transaction_id** | String | Unique id generated by you for future references | undefined |

#### Get Refund Detail
Use this to fetch details of a refund

    mojo.refunds.getDetail({
		id: 'xxx-xxx',
	}, (err, res) => {
		if (err) { 
			console.log(err)
			return
		}
		// do your task here
	})

##### Options
| Key  | Type | Description | Default |
|--|--|--|--|
| **id** | String | Unique Instamojo Identifier (not transaction_id) for the refund | undefined |

#### Get Refunds List
Use this fetch list of refunds

    mojo.refunds.list({
	    limit: 10,
	    page: 1
    }, (err, res) => {
		if (err) { 
			console.log(err)
			return
		}
		// do your task here	    
    })

##### Options
| Key  | Type | Description | Default |
|--|--|--|--|
| **limit** | Integer | Number of records to fetch at a time | undefined |
| **page** | Integer | Page Number to get nth number of records | undefined |

--- 
### Orders
#### Create a new Order
Use this to create a new order

    mojo.orders.create({
	    name : 'Name here',
	    email : 'Email id here',
	    phone : '9999999999',
	    currency: 'INR',
	    amount: 100,
	    transaction_id: 'aaaa-bbbb',
	    redirect_url: 'https://instamojo.com'
    }, (err, res) => {
		if (err) { 
			console.log(err)
			return
		}
		// do your task here
	})

##### Options
| Key  | Type | Description | Default | Limit |
|--|--|--|--|--|
| **name** | String | Name of the payee | undefined | 100 chars |
| **email** | String | Email of the payee | undefined | 75 chars |
| **phone** | String | Phone Number of the payee | undefined | N/A |
| **currency** | String | String identifier for the currency. Currently, only  `INR`  (for Indian Rupee) is supported. | undefined | N/A |
| **amount** | Number | Amount the payee has to pay. Numbers upto 2 decimal places are supported. | undefined | N/A |
| **transaction_id** | String | Unique identifier for the order. Identifier can contain alphanumeric characters, hyphens and underscores only. This is generally the unique order id (or primary key) in your system. | undefined | 64 chars | 
| **redirect_url** | String | Full URL to which the customer is redirected after payment. Redirection happens even if payment wasn't successful. This URL shouldn't contain any query parameters. | undefined | N/A

#### Create an Order using Payment Request ID
Use this to create a new order using a payment request id

    mojo.orders.create({
		id: 'xxxx-xxxx'
	}, (err, res) => {
		if (err) { 
			console.log(err)
			return
		}
		// do your task here
	})
##### Options
| Key  | Type | Description | Default |
|--|--|--|--|
| **id** | String | Unique Identifier for Payment Request | undefined |

#### Get Order Detail
Use this to fetch details of a order

    mojo.orders.getDetail({
	    order_id: 'xxxx-xxxx'
    }, (err, res) => {
	    if (err) { 
			console.log(err)
			return
		}
		// do your task here
    })

##### Options
| Key  | Type | Description | Default |
|--|--|--|--|
| **order_id** | String | Unique Identifier for the Order | undefined |

#### Get Orders List
Use this to fetch list of orders

    mojo.orders.list({
	    limit: 10,
	    page: 1,
    }, (err, res) => {
	  	if (err) { 
			console.log(err)
			return
		}
		// do your task here  
    })
    
##### Options
| Key  | Type | Description | Default |
|--|--|--|--|
| **limit** | Integer | Number of records to fetch at a time | undefined |
| **page** | Integer | Page Number to get nth records | undefined |

#### Get Transaction Detail
Use this to fetch detail of any order's transaction

    mojo.orders.getTransactionDetail({
		transaction_id: 'aaaa-bbbb',
	}, (err, res) => {
		if (err) { 
			console.log(err)
			return
		}
		// do your task here  
	})
##### Options
| Key  | Type | Description | Default |
|--|--|--|--|
| **transaction_id** | String | Unique identifier of the transaction | undefined |

## Development & Testing
We support two environments for integration, **Sandbox** and **Production**. 

> For all the testing and development purposes, please use sandbox. 
> You can get testing credentials from sandbox dashboard. Additionally, you need to pass "sandbox: true". See "Initialization" for more information.

If you want to run unit test cases, you can do so by running the command below:

    npm run test

### Security
If you discover any security related issues, please email to [support@instamojo.com](mailto:support@instamojo.com)  instead of using the issue tracker.

## License
The MIT License. Please see  [License File](https://github.com/Instamojo/instamojo-nodejs/blob/master/LICENSE.md)  for more information. Copyright © 2020  [Instamojo](https://www.instamojo.com/)