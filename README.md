# Text-to-Speech Application

A serverless text-to-speech application built with AWS services that converts text into natural-sounding audio using Amazon Polly.

## Features

- Convert text to speech with multiple voice options
- Support for MP3, OGG, and PCM audio formats
- Adjustable speech speed (extra slow to extra fast)
- Real-time character counter (3000 character limit)
- Audio playback and download functionality
- Responsive web interface

## Architecture

- **Frontend**: Static HTML/CSS/JavaScript hosted on S3
- **Backend**: AWS Lambda function with Python
- **API**: Amazon API Gateway REST API
- **Text-to-Speech**: Amazon Polly
- **Storage**: S3 bucket for audio files
- **Infrastructure**: Terraform for deployment

## Prerequisites

- AWS CLI configured with appropriate credentials
- Terraform installed
- PowerShell (for Windows deployment)

## Deployment

1. **Clone and navigate to backend directory**:
   ```bash
   cd text-to-speech/backend
   ```

2. **Initialize and deploy infrastructure**:
   ```bash
   terraform init
   terraform plan
   terraform apply
   ```

3. **Create Lambda deployment package**:
   ```powershell
   Compress-Archive -Path lambda.py -DestinationPath lambda.zip -Force
   ```

4. **Update frontend with API endpoint**:
   - Copy the `rest_api_endpoint` output from Terraform
   - Update `API_BASE_URL` in `frontend/index.html`

5. **Upload frontend to S3**:
   - Upload `frontend/index.html` to the created S3 bucket
   - Access via the `website_endpoint` output

## Usage

1. Enter text (up to 3000 characters)
2. Select voice, format, and speed
3. Click "Generate Speech"
4. Play or download the generated audio

## Voice Options

- **Joanna** (US, Female)
- **Matthew** (US, Male)
- **Amy** (UK, Female)
- **Brian** (UK, Male)

## Audio Formats

- **MP3**: Standard compressed audio
- **OGG**: Open-source compressed audio
- **PCM**: Uncompressed audio

## Cleanup

To remove all resources:
```bash
terraform destroy
```

## Cost Considerations

- Amazon Polly: Pay per character processed
- Lambda: Pay per request and execution time
- S3: Pay for storage and requests
- API Gateway: Pay per API call

Audio files expire after 1 hour to minimize storage costs.