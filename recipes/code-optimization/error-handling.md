# Error Handling Recipe

## Description
Enhance error handling to make code more robust, maintainable, and user-friendly.

## Prompt Template

```
Improve error handling in the following [LANGUAGE] code:

[PASTE_CODE]

Requirements:
- Add try-catch blocks for potential failures
- Include specific error types/classes
- Add proper error messages and logging
- Implement graceful degradation
- Add input validation
- Follow [FRAMEWORK] error handling best practices
- Include error recovery mechanisms where appropriate
```

## Example Usage

### Example 1: API Error Handling

**Prompt:**
```
Improve error handling in the following Node.js Express code:

app.post('/api/users', async (req, res) => {
  const user = await createUser(req.body);
  res.json(user);
});

async function createUser(data) {
  const user = await db.users.create(data);
  await sendWelcomeEmail(user.email);
  return user;
}

Requirements:
- Add try-catch blocks for database and email failures
- Include specific error types (ValidationError, DatabaseError)
- Add proper HTTP status codes and error messages
- Implement graceful degradation (user created even if email fails)
- Add input validation for required fields
- Follow Express.js error handling best practices
- Include error logging with context
```

**Expected Improvements:**
- Comprehensive error handling with specific error types
- Proper HTTP status codes
- Graceful failure handling
- Detailed error logging

### Example 2: Python Function Error Handling

**Prompt:**
```
Improve error handling in the following Python code:

def process_file(filepath):
    file = open(filepath, 'r')
    data = json.loads(file.read())
    result = calculate_statistics(data['values'])
    file.close()
    return result

Requirements:
- Add try-except blocks for file operations and JSON parsing
- Include specific exception types (FileNotFoundError, JSONDecodeError, KeyError)
- Add proper error messages and logging
- Use context managers for file handling
- Add input validation for filepath
- Follow Python error handling best practices
- Include error recovery mechanisms where appropriate
```

**Expected Improvements:**
- Context managers for resource cleanup
- Specific exception handling
- Input validation
- Proper cleanup in error cases

### Example 3: AWS Lambda Error Handling

**Prompt:**
```
Improve error handling in the following AWS Lambda function:

def lambda_handler(event, context):
    bucket = event['Records'][0]['s3']['bucket']['name']
    key = event['Records'][0]['s3']['object']['key']
    
    s3_client = boto3.client('s3')
    obj = s3_client.get_object(Bucket=bucket, Key=key)
    data = obj['Body'].read()
    
    result = process_data(data)
    
    s3_client.put_object(
        Bucket=os.environ['OUTPUT_BUCKET'],
        Key=f'processed/{key}',
        Body=result
    )
    
    return {'statusCode': 200}

Requirements:
- Add try-except blocks for S3 operations and data processing
- Include specific error types (botocore.exceptions)
- Add proper error messages and CloudWatch logging
- Implement retry logic for transient S3 failures
- Add event structure validation
- Follow AWS Lambda error handling best practices
- Return proper error responses for monitoring
```

**Expected Improvements:**
- Robust error handling for AWS services
- CloudWatch logging integration
- Retry mechanisms
- Event validation

## Best Practices

1. **Specific Exceptions**: Catch specific exceptions, not generic ones
2. **Error Context**: Include contextual information in error messages
3. **Logging**: Log errors with appropriate severity levels
4. **User Messages**: Provide helpful error messages to users
5. **Recovery**: Implement recovery mechanisms when possible
6. **Resource Cleanup**: Ensure resources are cleaned up in error cases
7. **Testing**: Test error paths thoroughly

## Related Recipes

- [API Endpoint Creation](../code-creation/api-endpoint.md)
- [Testing Error Paths](../testing/error-testing.md)
- [Logging Best Practices](./logging.md)
