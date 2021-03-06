# Local Lambda development and testing

## Running the server locally

To run the server locally, start it by running:

```bash
python3 app.py
```

Then in another terminal run the following cURL command:

```bash
curl -X POST http://localhost:5050/greet -H "Content-type: application/json" -d "{\"name\":\"Jon\"}"
```

This should return a JSON response like the following:

```text
{"message": "Hello Jon!"}
```

If no `name` is provided in the data JSON, it uses the name `anon` as a default.

## Simulating AWS Lambda locally with Docker

Tu run the previous server as it was in AWS Lambda, first build the docker image:

```bash
make build
```

This will build a docker image that includes everything to run lambda locally.

Then run the container with:

```bash
make run
```

This will shows logs when receiving a trigger and everything that you can see in AWS with AWS Cloudwatch.

To query the Lambda, open a new terminal, and run the following cURL command:

```bash
curl -XPOST "http://localhost:5050/2015-03-31/functions/function/invocations" -d '{}'
```

Which will return the following JSON response:

```text
{"statusCode": 200, "headers": {"Content-Type": "application/json"}, "body": "{\"message\": \"Hello World!\"}"}
```
