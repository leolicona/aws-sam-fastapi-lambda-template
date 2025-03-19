# FastAPI on AWS Lambda with SAM

This project contains source code and supporting files for a serverless FastAPI application that you can deploy with the AWS SAM CLI. It includes the following files and folders:

- `hello_world/` - Code for the application's Lambda function. A FastAPI app with a Mangum wrapper.
- `template.yaml` - A template that defines the application's AWS resources.

## API Gateway Lambda Proxy Integration

This project utilizes API Gateway's proxy integration to route requests to the Lambda function running FastAPI. The SAM template includes two key route configurations:

```yaml
Events:
  ProxyRoute:
    Type: Api
    Properties:
      Path: /{proxy+}
      Method: ANY
  RootRoute:
    Type: Api
    Properties:
      Path: /
      Method: ANY
```

The `/{proxy+}` route handles all paths except the root path, while the `/` route specifically handles the root path. This dual configuration ensures that all routes work correctly, including the root endpoint.

## Prerequisites

- [AWS CLI](https://aws.amazon.com/cli/)
- [AWS SAM CLI](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-cli-install.html)
- Python 3.9 or higher

## Deploying

1. Build the application:
   ```bash
   sam build
   ```

2. Deploy the application:
   ```bash
   sam deploy --guided
   ```

   During the guided deployment, you'll be prompted to set various parameters. For most, the defaults are fine.

3. After deployment, you'll receive an API Gateway endpoint URL. You can access your API at this URL.

## API Endpoints

The application includes these endpoints:

- `GET /` - Returns `{"Hello": "World"}`
- `GET /test` - Returns `{"hell": "yeah"}`

## Local Development

For local development:

1. Install the requirements:
   ```bash
   pip install -r requirements.txt
   ```

2. Run the application locally:
   ```bash
   cd hello_world
   python app.py
   ```

   The application will be available at http://localhost:5000.

## Cleaning Up

To remove the deployed application and all its resources:

```bash
sam delete
```
