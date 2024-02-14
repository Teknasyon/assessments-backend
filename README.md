# Backend Assessment

This repository contains an assessment task which is designed to evaluate
candidates in the job application process and to help us assess the approaches
and abilities of participants.

In the task, you are expected to complete the project described below. While
completing the task, please make sure that you are delivering the best work you
can to assist us in an accurate evaluation.

## Requirements

### Technologies to be used:

- Golang, Node.js or PHP
- Kafka or Redpanda
- Docker
- Git

### Constraints and Conventions:

- Use of testable, predictable code routines as soon as possible
- Developing the project with frequent commits on version control system
- Use of "conventional commits" convention for commit messages
- Minimum 60% unit testing code coverage
- Writing a markdown documentation to describe how to run it
- If your language choice is Golang, following the conventions of
  [Standard Go Project Layout](https://github.com/golang-standards/project-layout)
- The whole system should be containerized and ready to run in any environment.

## How to Get Started?

Begin by creating the project codebase.

Next, transfer the codebase to a git repository and share the repository address
upon completion.

## Scenerio

In a system that receives high traffic, we will have two services.

The first service will handle incoming traffic concurrently through an HTTP
protocol and:

- place the messages into a queue structure set up with either Kafka or
  Redpanda.
- show us the final state of the records.

The second service will process queued messages and will modify the records
accordingly. The final records will be kept in a persistent storage.

## Events

- BALANCE_INCREASE: Increases the balance of the respective currency in a
  wallet.
- BALANCE_DECREASE: Decreases the balance of the respective currency in a
  wallet.

### API

#### POST / - Dispatching Events

Request:

```http
POST /
Content-Type: application/json

{
    "events": [
        {
            "app": "01HPMTX8916FF4ABFBDESX1AGH",
            "type": "BALANCE_INCREASE",
            "time": "2024-02-12T11:50:40.280Z",
            "meta": {
              "user": "01HPMV114ZE7Z54M6XV8H4EEMB"
            },
            "wallet": "01HPMV01XPAXCG242W7SZWD0S5",
            "attributes": {
                "amount": "33.20",
                "currency": "TRY"
            }
        },
        {
            "app": "01HPMTX8916FF4ABFBDESX1AGH",
            "type": "BALANCE_DECREASE",
            "time": "2024-02-12T11:50:40.281Z",
            "meta": {
              "user": "01HPMV114ZE7Z54M6XV8H4EEMB"
            },
            "wallet": "01HPMV01XPAXCG242W7SZWD0S5",
            "attributes": {
                "amount": "3.10",
                "currency": "TRY"
            }
        }
    ]
}
```

Response:

```
HTTP 200 OK
```

#### GET / - Displaying Latest State

Request:

```http
GET /
```

Response:

```
HTTP 200 OK
Content-Type: application/json; charset=utf-8

{
    "wallets": [
        {
            "id": "01HPMV01XPAXCG242W7SZWD0S5",
            "balances": [
                {
                    "currency": "TRY",
                    "amount": "30.10"
                }
            ]
        }
    ]
}
```

## Engineering Expectations

- Including behavior and/or E2E tests are a huge plus.
- It's not mandatory but using a API spec and/or collection of http requests
  would be nice.
- Technical design documentation, providing runtime metrics, monitoring
  dashboards and keeping records of architectural decisions are also
  appreciated.

## Your Questions

You can send your questions regarding the assessment to
[eser@teknasyon.com](mailto:eser@teknasyon.com).

## License

Licensed under [Apache 2.0](LICENSE).
