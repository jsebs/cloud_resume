DynamoDB - table to store and return a 'views' item

API - Lambda Function (Python 3.8) using HTTPS endpoints to communicate with the DB and update the view counter

import json
import boto3 // imports libraries
dynamodb = boto3.resource('dynamodb') // assigns a var with the dynamodb resource to interact with
table = dynamodb.table('cloudresume-test') // calls the table from the db
def lambda_handler(event, context):
    response = table.get_item(Key={ // gets the 'id' item from the table where the key 'id' is '1'
        'id':'1'
    })
    views = response['Item']['views'] // gets the 'views'
    views = views + 1 // adds 1 to the current value in 'views'
    print(views) // prints the 'views' value
    response = table.put_item(Item={ // updates the item in the db table where the 'id' is '1' and 'views' is equal to the new value of 'views' (incremented by 1)
        'id':'1',
        'views':views
    })
    return views


// JavaScript Lambda trigger to display + increase view count
const counter = document.querySelector(".counter-number"); // variable that selects the '.counter-number' class from the index.html page
async function updateCounter() {
    let response = await fetch("https://xf2bddy7jkrbvi6ddks4ypilla0bpmvb.lambda-url.us-west-2.on.aws/"); // function performs a fetch request on the HTTP endpoint of our Lambda func
    let data = await response.json(); // stores the response from the fetch request in a new 'data' var
    counter.innerHTML = ` Views: ${data}`; // updates the number in the 'counter-number' element to display what was returned by the fetch request
}

updateCounter();
