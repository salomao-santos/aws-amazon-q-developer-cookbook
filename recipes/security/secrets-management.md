# Secrets Management Recipe

## Description
Implement secure handling of sensitive data like API keys, passwords, and tokens to prevent exposure in code.

## Prompt Template

```
Refactor the following [LANGUAGE] code to securely manage secrets:

[PASTE_CODE]

Security requirements:
- Remove hardcoded credentials/API keys
- Use environment variables for secrets
- Implement secrets rotation (if applicable)
- Add validation for required secrets
- Use secure secret storage ([AWS Secrets Manager/HashiCorp Vault/etc.])
- Never log sensitive data
- Add .env to .gitignore
- Follow [FRAMEWORK] security best practices
- Include setup instructions
```

## Example Usage

### Example 1: Remove Hardcoded Credentials

**Prompt:**
```
Refactor the following Node.js code to securely manage secrets:

const mysql = require('mysql2');
const stripe = require('stripe')('sk_live_abc123xyz789');

const connection = mysql.createConnection({
  host: 'db.example.com',
  user: 'admin',
  password: 'SuperSecret123!',
  database: 'production'
});

const sendEmail = async (to, subject, body) => {
  const nodemailer = require('nodemailer');
  const transporter = nodemailer.createTransport({
    service: 'gmail',
    auth: {
      user: 'app@company.com',
      pass: 'myEmailPassword123'
    }
  });
  
  await transporter.sendMail({ from: 'app@company.com', to, subject, html: body });
};

Security requirements:
- Remove all hardcoded credentials
- Use environment variables for all secrets
- Use dotenv package for local development
- Add validation for required environment variables
- Never log sensitive data
- Add .env to .gitignore
- Follow Node.js security best practices
- Include setup instructions in comments
```

**Expected Output:**
```javascript
/**
 * Database and API Configuration
 * 
 * Required environment variables:
 * - DB_HOST: Database hostname
 * - DB_USER: Database username
 * - DB_PASSWORD: Database password
 * - DB_NAME: Database name
 * - STRIPE_SECRET_KEY: Stripe API secret key
 * - EMAIL_USER: Email service username
 * - EMAIL_PASSWORD: Email service password
 * 
 * Setup:
 * 1. Copy .env.example to .env
 * 2. Fill in all required values
 * 3. Ensure .env is in .gitignore
 */

require('dotenv').config();
const mysql = require('mysql2');
const stripe = require('stripe');

// Validate required environment variables
const requiredEnvVars = [
  'DB_HOST',
  'DB_USER',
  'DB_PASSWORD',
  'DB_NAME',
  'STRIPE_SECRET_KEY',
  'EMAIL_USER',
  'EMAIL_PASSWORD'
];

for (const envVar of requiredEnvVars) {
  if (!process.env[envVar]) {
    throw new Error(`Missing required environment variable: ${envVar}`);
  }
}

// Initialize Stripe with secret from environment
const stripeClient = stripe(process.env.STRIPE_SECRET_KEY);

// Create database connection with credentials from environment
const connection = mysql.createConnection({
  host: process.env.DB_HOST,
  user: process.env.DB_USER,
  password: process.env.DB_PASSWORD,
  database: process.env.DB_NAME,
  // Additional security: enable SSL
  ssl: {
    rejectUnauthorized: true
  }
});

// Error handling without exposing credentials
connection.connect((err) => {
  if (err) {
    // Log error without sensitive details
    console.error('Database connection failed:', err.code);
    process.exit(1);
  }
  console.log('Database connected successfully');
});

const sendEmail = async (to, subject, body) => {
  const nodemailer = require('nodemailer');
  
  // Use environment variables for email credentials
  const transporter = nodemailer.createTransport({
    service: 'gmail',
    auth: {
      user: process.env.EMAIL_USER,
      pass: process.env.EMAIL_PASSWORD
    }
  });
  
  try {
    await transporter.sendMail({
      from: process.env.EMAIL_USER,
      to,
      subject,
      html: body
    });
    console.log(`Email sent to ${to}`);
  } catch (error) {
    // Log error without exposing credentials
    console.error('Email send failed:', error.message);
    throw error;
  }
};

module.exports = {
  stripeClient,
  connection,
  sendEmail
};
```

**Example .env file:**
```bash
# Database Configuration
DB_HOST=db.example.com
DB_USER=admin
DB_PASSWORD=SuperSecret123!
DB_NAME=production

# API Keys
STRIPE_SECRET_KEY=sk_live_abc123xyz789

# Email Configuration
EMAIL_USER=app@company.com
EMAIL_PASSWORD=myEmailPassword123
```

**Example .env.example file:**
```bash
# Database Configuration
DB_HOST=localhost
DB_USER=your_db_user
DB_PASSWORD=your_db_password
DB_NAME=your_db_name

# API Keys
STRIPE_SECRET_KEY=your_stripe_secret_key

# Email Configuration
EMAIL_USER=your_email@example.com
EMAIL_PASSWORD=your_email_password
```

**Example .gitignore addition:**
```
# Environment variables
.env
.env.local
.env.*.local
```

### Example 2: AWS Secrets Manager Integration

**Prompt:**
```
Refactor the following Python code to use AWS Secrets Manager:

import psycopg2
import boto3

def get_db_connection():
    return psycopg2.connect(
        host="prod-db.abc123.us-east-1.rds.amazonaws.com",
        database="myapp",
        user="admin",
        password="MyDatabasePassword123!"
    )

def send_sms(phone, message):
    sns = boto3.client('sns',
        aws_access_key_id='AKIAIOSFODNN7EXAMPLE',
        aws_secret_access_key='wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY',
        region_name='us-east-1'
    )
    sns.publish(PhoneNumber=phone, Message=message)

Security requirements:
- Remove all hardcoded credentials
- Use AWS Secrets Manager for database credentials
- Use IAM roles instead of access keys
- Add error handling for secret retrieval
- Cache secrets appropriately
- Never log sensitive data
- Follow AWS security best practices
- Include boto3 secrets manager setup
```

**Expected Output:**
```python
"""
Database and AWS Configuration using AWS Secrets Manager

Required setup:
1. Create secret in AWS Secrets Manager with database credentials
2. Attach IAM policy to Lambda/EC2 role to read secrets
3. Set environment variable: DB_SECRET_NAME

IAM Policy needed:
{
  "Version": "2012-10-17",
  "Statement": [{
    "Effect": "Allow",
    "Action": ["secretsmanager:GetSecretValue"],
    "Resource": "arn:aws:secretsmanager:region:account-id:secret:secret-name"
  }]
}
"""

import json
import os
import psycopg2
import boto3
from botocore.exceptions import ClientError
from functools import lru_cache

# Initialize AWS clients using IAM role (no hardcoded credentials)
secretsmanager = boto3.client('secretsmanager')
sns = boto3.client('sns')  # Uses IAM role automatically

@lru_cache(maxsize=1)
def get_database_credentials():
    """
    Retrieve database credentials from AWS Secrets Manager.
    Cached to avoid repeated API calls.
    
    Returns:
        dict: Database credentials
        
    Raises:
        Exception: If secret retrieval fails
    """
    secret_name = os.environ.get('DB_SECRET_NAME')
    
    if not secret_name:
        raise ValueError('DB_SECRET_NAME environment variable not set')
    
    try:
        response = secretsmanager.get_secret_value(SecretId=secret_name)
        
        # Parse the secret string
        if 'SecretString' in response:
            secret = json.loads(response['SecretString'])
            return secret
        else:
            raise ValueError('Secret not found in expected format')
            
    except ClientError as e:
        error_code = e.response['Error']['Code']
        
        # Log error without exposing sensitive details
        if error_code == 'ResourceNotFoundException':
            print(f'Secret {secret_name} not found')
        elif error_code == 'InvalidRequestException':
            print('Invalid request to Secrets Manager')
        elif error_code == 'InvalidParameterException':
            print('Invalid parameter in request')
        elif error_code == 'DecryptionFailure':
            print('Failed to decrypt secret')
        elif error_code == 'InternalServiceError':
            print('Secrets Manager service error')
        else:
            print(f'Error retrieving secret: {error_code}')
            
        raise Exception('Failed to retrieve database credentials') from e

def get_db_connection():
    """
    Create a database connection using credentials from Secrets Manager.
    
    Returns:
        psycopg2.connection: Database connection
    """
    try:
        credentials = get_database_credentials()
        
        # Validate required fields
        required_fields = ['host', 'database', 'username', 'password']
        for field in required_fields:
            if field not in credentials:
                raise ValueError(f'Missing required field in secret: {field}')
        
        connection = psycopg2.connect(
            host=credentials['host'],
            database=credentials['database'],
            user=credentials['username'],
            password=credentials['password'],
            port=credentials.get('port', 5432),
            sslmode='require'  # Enforce SSL
        )
        
        print('Database connected successfully')
        return connection
        
    except Exception as e:
        # Log error without credentials
        print(f'Database connection failed: {type(e).__name__}')
        raise

def send_sms(phone: str, message: str):
    """
    Send SMS using AWS SNS with IAM role authentication.
    
    Args:
        phone: Phone number in E.164 format
        message: SMS message text
        
    Raises:
        Exception: If SMS sending fails
    """
    try:
        # Validate inputs (don't log phone or message)
        if not phone or not message:
            raise ValueError('Phone and message are required')
        
        # SNS client uses IAM role automatically, no credentials needed
        response = sns.publish(
            PhoneNumber=phone,
            Message=message
        )
        
        # Log success without sensitive data
        print(f'SMS sent successfully, MessageId: {response["MessageId"]}')
        
    except ClientError as e:
        error_code = e.response['Error']['Code']
        print(f'SNS publish failed: {error_code}')
        raise Exception('Failed to send SMS') from e
    except Exception as e:
        print(f'Unexpected error sending SMS: {type(e).__name__}')
        raise

# Example usage
if __name__ == '__main__':
    # Ensure environment variable is set
    if not os.environ.get('DB_SECRET_NAME'):
        print('Error: DB_SECRET_NAME environment variable required')
        exit(1)
    
    # Test database connection
    try:
        conn = get_db_connection()
        conn.close()
        print('Database test successful')
    except Exception as e:
        print(f'Database test failed: {e}')
```

**Example secret structure in AWS Secrets Manager:**
```json
{
  "host": "prod-db.abc123.us-east-1.rds.amazonaws.com",
  "port": 5432,
  "database": "myapp",
  "username": "admin",
  "password": "MyDatabasePassword123!"
}
```

## Best Practices

1. **Never Hardcode**: Never commit secrets to version control
2. **Environment Variables**: Use for local development
3. **Secret Stores**: Use dedicated services for production (AWS Secrets Manager, HashiCorp Vault)
4. **IAM Roles**: Prefer IAM roles over access keys in AWS
5. **Rotation**: Implement automatic secret rotation
6. **Least Privilege**: Grant minimal permissions needed
7. **Audit Logging**: Log secret access (not the secrets themselves)
8. **Encryption**: Encrypt secrets at rest and in transit

## Secret Storage Options

### Local Development
- **dotenv**: Environment variables from .env file
- **.gitignore**: Exclude .env files from version control

### Production
- **AWS Secrets Manager**: Managed secret storage with rotation
- **HashiCorp Vault**: Enterprise secret management
- **Azure Key Vault**: Azure secret storage
- **Google Secret Manager**: GCP secret storage
- **Docker Secrets**: For container orchestration

## Checklist

- [ ] No hardcoded credentials in code
- [ ] Secrets stored in environment variables or secret manager
- [ ] .env files excluded from version control
- [ ] .env.example provided with dummy values
- [ ] Required environment variables validated at startup
- [ ] Secrets never logged or exposed in error messages
- [ ] IAM roles used instead of access keys (AWS)
- [ ] Secret rotation implemented (if applicable)
- [ ] Documentation includes setup instructions

## Related Recipes

- [API Security](./api-security.md)
- [AWS Security](./aws-security.md)
- [Authentication](./auth.md)
