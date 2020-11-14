# cdiAppMainRepo

## Structure

This repo is just a centralization of the front a back repos
- CdiAppBackend submodule for the backend, implemented with node.js
- simpleCDIapp submodule for the frontend, implemented with angular

## How to run 

- Just Access https://cdi-app-front.herokuapp.com/ to run the front application
- If you want to check the backend responses, you can test sending a POST request using Postman or any tool like that to https://cdi-app-backend.herokuapp.com/unc following the format:
```
{
    "investmentDate":"2016-11-14",
    "cdbRate": 103.5,
    "currentDate":"2016-12-26"
}
```
- You can also clone the front-end repo and folow the build instructions on its README.md to run the frontend locally.

## How it works

### The backend
All CDI rates are stored in a cluster on cloud.mongodb.com. The mongodb database also stores the TCDI data to avoid calculating it every time the API is called. The data is stored in the format bellow:

```
{
  "_id": "5fab538326e8599025c46515",
  "date": "2019-12-03T00:00:00.000Z",
  "rate": 4.9,
  "tcdi": 0.00018985
}
``` 

When backend service receives a POST request, it calculates the accumulated TCDI while calculating the CDB price to return on the json response performing it with O(n) complexity. The response follows the following format:

```
[
    {
        "date": "2016-11-14",
        "unitPrice": NN.NN
    },
    {
        "date": "2016-11-16",
        "unitPrice": NN.NN
    },
    {
        "date": "2016-11-17",
        "unitPrice": NN.NN
    },
    ...
]
```


### The frontend

- When opened it just plots some hardcoded values
- The user can set the initial date, final date and also the CDB percentage.
- When "calcular" button is pushed, it sends the POST request to the backend service and waits for its response.
- If the answer by the server is not empty, the chart will be ploted with the received data. Also the "valor" label will be set with the value calculated for the final date set by the user.


## Considerations

Since my lack of experience with web development the project was made in a "learn while go" maner, a lot of the implementation is very naive. I think the hardest part was to implement that weird looking front. Well, in some way learning all the tecnologies involved on this test was really challenging too, the easiest part was deploying it to heroku lol.


### Things to Fix

- Create unit tests for the backend and e2e for the front.
- Input fields validation on frontend, right now the application have some bugs related to it.(For example, there is no validation of initial and final date)
- Project architecture lacks of modularization and design, front and backend. No design or architectural patterns were applied, so the design could be improved A LOT.
- The backend does not handle wrong requests, unknown json format and do not send error responses, there are some bugs related to it.
- No comments on the code.
- There is some random garbage through the code.
- the communication between front and back may take a while, so it would be nice to have a loading animation.

### Cool TO-DOs
- Improve frontend app UI.
- Both repos with github actions for automatic deploy to heroku.
- Architectural documentation.




