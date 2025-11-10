# Lambda Function Creation Recipe

## Description
Create AWS Lambda functions following best practices for performance, security, and maintainability.

## Prompt Template

```
Create an AWS Lambda function for [PURPOSE] with the following requirements:
- Runtime: [Python/Node.js/Java/etc.]
- Trigger: [API Gateway/S3/EventBridge/etc.]
- Input event structure: [SPECIFY_EVENT_SCHEMA]
- Expected output: [SPECIFY_OUTPUT]
- Include error handling and retries
- Include CloudWatch logging
- Follow AWS Lambda best practices (cold start optimization, proper IAM)
- Include environment variable usage
- Add proper timeout and memory configuration comments
```

## Example Usage

### Example 1: S3 Image Processing Lambda

**Prompt:**
```
Create an AWS Lambda function for image processing with the following requirements:
- Runtime: Python 3.11
- Trigger: S3 bucket upload event
- Input event structure: S3 event with bucket name and object key
- Expected output: Processed image saved to different S3 bucket
- Include error handling for missing files, invalid formats
- Include CloudWatch logging
- Follow AWS Lambda best practices (cold start optimization, proper IAM)
- Include environment variable usage for bucket names
- Add proper timeout (300s) and memory (1024MB) configuration comments
- Use Pillow library for image resizing to 800x600
```

**Expected Output:**
- Lambda handler function
- S3 client initialization (outside handler for reuse)
- Error handling and logging
- Environment variable configuration
- Requirements.txt or package.json

### Example 2: API Gateway Integration Lambda

**Prompt:**
```
Create an AWS Lambda function for user authentication with the following requirements:
- Runtime: Node.js 18
- Trigger: API Gateway POST request
- Input event structure: API Gateway proxy event with JSON body containing username and password
- Expected output: API Gateway proxy response with JWT token
- Include error handling for invalid credentials (401), missing parameters (400)
- Include CloudWatch logging
- Follow AWS Lambda best practices
- Include environment variable usage for JWT secret
- Add proper timeout (30s) and memory (512MB) configuration comments
```

## Best Practices

1. **Specify Runtime**: Always mention the runtime version
2. **Event Source**: Clearly define the trigger and event structure
3. **Environment Variables**: Request configuration via environment variables
4. **Error Handling**: Include specific error scenarios
5. **Resource Limits**: Specify appropriate timeout and memory settings
6. **Cold Starts**: Request optimization techniques for frequently-used functions
7. **IAM Permissions**: Ask for minimal required permissions

## Testing

Use [Lambda Testing recipes](../testing/lambda-testing.md) to create unit and integration tests.

## Related Recipes

- [Error Handling](../code-optimization/error-handling.md)
- [Lambda Testing](../testing/lambda-testing.md)
- [Security Best Practices](../security/aws-security.md)
