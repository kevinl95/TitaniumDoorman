# TitaniumDoorman

<p align="center">
  <img src="assets/titaniumdoormanlogo.png" alt="TitaniumDoorman Logo" width="200">
</p>

[![Lint CloudFormation Template](https://github.com/kevinl95/TitaniumDoorman/actions/workflows/main.yml/badge.svg)](https://github.com/kevinl95/TitaniumDoorman/actions/workflows/main.yml)

Hardware-less doorbell for the [TiDB AgentX Hackathon](https://tidb-2025-hackathon.devpost.com). Visitors can scan a QR code → interact with an AI agent → resident gets notified via a text on their phone! No transformer, batteries, wires, or chime required. This makes it perfect for apartments, condos, or older homes. Best of all, it deploys with a single click with no coding or cloud experience required!

## Quick Deploy

[![Deploy to AWS](https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/new?stackName=titanium-doorman&templateURL=https://raw.githubusercontent.com/YOUR_USERNAME/TitaniumDoorman/main/cloudformation.yml)

**Prerequisites:**
- AWS Account with permissions for Lambda, API Gateway, SNS, S3, Secrets Manager, Bedrock
- TiDB Serverless cluster (get free at [tidbcloud.com](https://tidbcloud.com))

**Setup Steps:**
1. Click "Deploy to AWS" button above
2. Enter your TiDB endpoint, username, password, and notification phone number (+1234567890)
3. Deploy the stack (takes ~3 minutes)
4. Open the "QRCodeUrl" from stack outputs
5. Print the QR code page and post by your door!
6. Done! Visitors can now scan and interact with your virtual doorman

## How It Works

**Multi-Step Agentic AI Workflow:**

1. **Data Ingestion** → Visitor messages stored in TiDB with session tracking
2. **Historical Search** → Agent searches previous visits by name and intent patterns
3. **AI Classification** → Amazon Bedrock (Titan Text Express) analyzes message context
4. **AI Response Generation** → Personalized responses based on visitor history
5. **External Actions** → SMS notifications sent to resident with visit context

**Intelligence Features:**
- Recognizes returning visitors and personalizes responses
- Learns from historical visit patterns stored in TiDB
- Uses vector and full-text search for contextual awareness
- Fallback classification ensures reliability

## Architecture

- **API Gateway** - Public endpoints for visitor interactions
- **Lambda Functions** - Session management and AI agent orchestration  
- **TiDB Serverless** - Stores visits, transcripts with vector search
- **AWS Bedrock** - LLM for visitor intent classification
- **SNS** - Resident notifications