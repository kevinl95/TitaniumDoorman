# TitaniumDoorman

[![Lint CloudFormation Template](https://github.com/kevinl95/TitaniumDoorman/actions/workflows/main.yml/badge.svg)](https://github.com/kevinl95/TitaniumDoorman/actions/workflows/main.yml)

Hardware-less doorbell for TiDB hackathon. Visitors scan QR code → interact with AI agent → resident gets notified.

## Quick Deploy

[![Deploy to AWS](https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/new?stackName=titanium-doorman&templateURL=https://raw.githubusercontent.com/YOUR_USERNAME/TitaniumDoorman/main/cloudformation.yml)

**Prerequisites:**
- AWS Account with permissions for Lambda, API Gateway, SNS, S3, Secrets Manager
- TiDB Serverless cluster (get free at [tidbcloud.com](https://tidbcloud.com))

**Setup Steps:**
1. Click "Deploy to AWS" button above
2. Enter your TiDB endpoint, username, password, and notification email  
3. Deploy the stack (takes ~3 minutes)
4. Open the "QRCodeUrl" from stack outputs
5. Print the QR code page and post by your door!
6. Done! Visitors can now scan and interact with your virtual doorman



## Demo Flow

1. **Visitor scans QR code** → Opens visitor.html
2. **Visitor types message** → "Hi, I have a package delivery"
3. **AI classifies intent** → "delivery" 
4. **Resident gets email** → "🚪 Doorbell Visit - Delivery"
5. **Agent responds** → "I'll let the resident know about your delivery"

## Architecture

- **API Gateway** - Public endpoints for visitor interactions
- **Lambda Functions** - Session management and AI agent orchestration  
- **TiDB Serverless** - Stores visits, transcripts with vector search
- **AWS Bedrock** - LLM for visitor intent classification
- **SNS** - Resident notifications