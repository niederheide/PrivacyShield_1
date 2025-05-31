PrivGuard - Privacy Compliance Management Platform
A sophisticated privacy compliance management platform that leverages advanced multi-AI technologies to transform complex data protection workflows into intuitive, actionable insights.

Architecture Overview
PrivGuard is a full-stack TypeScript application with:

Frontend: React SPA with Vite build system
Backend: Express.js REST API
Database: PostgreSQL with Drizzle ORM
AI Integration: Multi-provider AI analysis (OpenAI, Anthropic, ContextGem)
File Processing: Server-side PDF parsing and document analysis
Core Features
Privacy Compliance Modules
DPIA Assistant: Wizard-based Data Protection Impact Assessment with step-by-step guidance
Gap Detection: Triple-AI compliance analysis comparing internal policies against regulatory requirements
Vendor Assessment: Contract analysis with Quick Assessment Tools for data sharing agreements
Breach Orchestrator: Incident management with regulatory notification workflows
DPO Assistant: AI-powered chatbot providing privacy guidance with regulatory citations
Statutory Rules Engine: Pre-configured compliance rules mapped to jurisdictions (GDPR, CCPA, etc.)
Audit & Training: Staff training logs with evidence management and audit trails
Document Processing
Legal Document Corpus: Persistent storage of regulatory texts and legal documents
Client Policy Management: Session-based policy uploads with real-time analysis
AI Document Analysis: Structured field extraction from privacy policies and contracts
Multi-format Support: PDF, DOCX, and text document processing
AI Analysis Pipeline
ContextGem: Document intelligence and structured field extraction
OpenAI GPT-4o: Compliance gap analysis and risk assessment
Anthropic Claude: Secondary analysis for validation and alternative perspectives
Dual LLM Consensus: Cross-validation of AI analysis results
Technology Stack
Frontend Dependencies
{
  "react": "^18.3.1",
  "react-dom": "^18.3.1",
  "typescript": "5.6.3",
  "vite": "^5.4.14",
  "tailwindcss": "^3.4.17",
  "wouter": "^3.3.5",
  "@tanstack/react-query": "^5.60.5",
  "@radix-ui/react-*": "Various UI components",
  "react-hook-form": "^7.55.0",
  "lucide-react": "^0.453.0",
  "recharts": "^2.15.2"
}
Backend Dependencies
{
  "express": "^4.21.2",
  "drizzle-orm": "^0.39.1",
  "@neondatabase/serverless": "^0.10.4",
  "multer": "^2.0.0",
  "pdf-parse": "^1.1.1",
  "openai": "^4.103.0",
  "@anthropic-ai/sdk": "^0.37.0",
  "passport": "^0.7.0",
  "express-session": "^1.18.1",
  "zod": "^3.24.2"
}
Complete Environment Configuration
Required Environment Variables
Create a .env file with ALL of the following variables:

# Database Configuration (REQUIRED)
DATABASE_URL=postgresql://username:password@host:port/database
PGHOST=your_database_host
PGPORT=5432
PGDATABASE=privguard
PGUSER=your_database_user
PGPASSWORD=your_database_password
# AI Service API Keys (At least OPENAI_API_KEY required)
OPENAI_API_KEY=sk-your_openai_api_key_here
ANTHROPIC_API_KEY=sk-ant-your_anthropic_key_here
CONTEXTGEM_API_KEY=your_contextgem_key_here
GEMINI_API_KEY=your_gemini_key_here
GOOGLE_API_KEY=your_google_api_key_here
# Server Configuration
PORT=5000
NODE_ENV=production
# Session Security (REQUIRED)
SESSION_SECRET=your_secure_random_session_secret_minimum_32_characters
# File Upload Configuration
MAX_FILE_SIZE=50mb
UPLOAD_PATH=./uploads
Database Schema
The application uses Drizzle ORM with the following core tables:

-- Core tables automatically created by Drizzle migrations
legal_documents         -- Persistent legal/regulatory document corpus
client_policies         -- User-uploaded internal policies  
statutory_rules         -- Pre-configured compliance rules by jurisdiction
dpia_assessments        -- Data Protection Impact Assessments
dpia_workflow_steps     -- DPIA wizard step data
dpia_risks             -- Risk assessments from DPIA analysis
vendor_assessments     -- Contract review and vendor risk analysis
breach_incidents       -- Data breach incident management
audit_evidence         -- Training and audit documentation
document_analysis      -- AI analysis results storage
gap_analysis_results   -- Compliance gap analysis outcomes
Installation & Setup
Prerequisites
Node.js 18+ (tested with 18.19.0)
PostgreSQL 13+ database
Git
OpenAI API account (minimum requirement)
Anthropic API account (optional but recommended)
Step 1: Clone and Install
git clone https://github.com/your-org/privguard.git
cd privguard
npm install
Step 2: Database Setup
# Create PostgreSQL database
createdb privguard
# Set database URL in .env file
echo "DATABASE_URL=postgresql://username:password@localhost:5432/privguard" >> .env
# Initialize database schema
npm run db:push
Step 3: Environment Configuration
# Copy template and configure
cp .env.example .env
# Edit .env with your actual values
# CRITICAL: Set at least DATABASE_URL, OPENAI_API_KEY, and SESSION_SECRET
Step 4: Build and Start
# Development mode
npm run dev
# Production build
npm run build
npm start
API Endpoints Reference
Authentication & Session Management
POST /api/auth/login - User authentication
POST /api/auth/logout - Session termination
GET /api/auth/user - Current user info
Dashboard & Statistics
GET /api/dashboard - Dashboard overview with compliance metrics
GET /api/dashboard/recent-activity - Recent system activity
Document Management
POST /api/legal-documents - Upload legal/regulatory documents
GET /api/legal-documents - List all legal documents
PUT /api/legal-documents/:id - Update document metadata
DELETE /api/legal-documents/:id - Remove document
POST /api/client-policies - Upload internal policies
GET /api/client-policies - List uploaded policies
DELETE /api/client-policies/:id - Remove policy
Compliance Analysis
POST /api/gap-analysis/run - Execute compliance gap analysis
GET /api/gap-analysis/:id - Retrieve analysis results
POST /api/document-analysis - AI-powered document field extraction
GET /api/statutory-rules - Get compliance rules by jurisdiction
DPIA (Data Protection Impact Assessment)
POST /api/dpia - Create new DPIA assessment
GET /api/dpia - List all DPIAs
GET /api/dpia/:id - Get specific DPIA
PUT /api/dpia/:id/step/:stepNumber - Update DPIA workflow step
POST /api/dpia/:id/document-analysis - Analyze documents for DPIA
POST /api/dpia/:id/risk-assessment - Generate AI risk assessment
Vendor Assessment
POST /api/vendor-assessments - Create vendor assessment
GET /api/vendor-assessments - List assessments
POST /api/contract-analysis - Analyze vendor contracts
GET /api/vendor-assessments/:id/export - Export assessment report
Breach Management
POST /api/breach-incidents - Report data breach
GET /api/breach-incidents - List all incidents
PUT /api/breach-incidents/:id - Update incident status
POST /api/breach-incidents/:id/notify - Send regulatory notifications
Audit & Training
POST /api/audit-evidence - Upload audit evidence
GET /api/audit-evidence - List audit records
GET /api/training-records - Staff training logs
GET /api/audit-evidence/export - Export audit trail
DPO Assistant (Chatbot)
POST /api/dpo-chat - Chat with DPO assistant
GET /api/dpo-chat/history - Chat history
POST /api/dpo-chat/search - Search legal documents
AWS Deployment Guide
Pre-Deployment Checklist
PostgreSQL RDS instance created
All environment variables configured in AWS
File storage strategy decided (local vs S3)
SSL certificate ready for production
Domain name configured (optional)
Deployment Option 1: AWS Elastic Beanstalk
# Install EB CLI
pip install awsebcli
# Initialize Elastic Beanstalk
eb init privguard --platform node.js
# Create production environment
eb create privguard-prod
# Set all environment variables
eb setenv DATABASE_URL=your_rds_url \
         OPENAI_API_KEY=your_openai_key \
         ANTHROPIC_API_KEY=your_anthropic_key \
         SESSION_SECRET=your_session_secret \
         NODE_ENV=production
# Deploy application
eb deploy
Deployment Option 2: Docker on AWS ECS
# Use provided Dockerfile
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production
COPY . .
RUN npm run build
EXPOSE 5000
CMD ["npm", "start"]
# Build and push to ECR
aws ecr create-repository --repository-name privguard
docker build -t privguard .
docker tag privguard:latest 123456789.dkr.ecr.us-east-1.amazonaws.com/privguard:latest
docker push 123456789.dkr.ecr.us-east-1.amazonaws.com/privguard:latest
# Create ECS cluster and service with environment variables
Deployment Option 3: AWS EC2 with PM2
# On EC2 instance
git clone https://github.com/your-org/privguard.git
cd privguard
npm install
npm run build
# Install PM2
npm install -g pm2
# Create ecosystem file
cat > ecosystem.config.js << EOF
module.exports = {
  apps: [{
    name: 'privguard',
    script: 'dist/index.js',
    env: {
      NODE_ENV: 'production',
      PORT: 5000,
      DATABASE_URL: 'your_database_url',
      OPENAI_API_KEY: 'your_openai_key',
      ANTHROPIC_API_KEY: 'your_anthropic_key',
      SESSION_SECRET: 'your_session_secret'
    }
  }]
}
EOF
# Start with PM2
pm2 start ecosystem.config.js
pm2 save
pm2 startup
Database Migration & Data Management
Initial Setup
# Push schema to database
npm run db:push
# Verify tables created
psql $DATABASE_URL -c "\dt"
Data Seeding (Legal Documents)
The application includes pre-configured statutory rules for major jurisdictions:

GDPR (European Union)
CCPA (California)
PIPEDA (Canada)
LGPD (Brazil)
Backup Strategy
# Regular database backup
pg_dump $DATABASE_URL > backup_$(date +%Y%m%d).sql
# Restore from backup
psql $DATABASE_URL < backup_20240101.sql
File Storage Configuration
Local Storage (Default)
Files uploaded to ./uploads directory. Ensure proper permissions and backup strategy.

AWS S3 Integration (Recommended for Production)
Update server/routes.ts multer configuration:

// Replace local storage with S3
const s3Storage = multerS3({
  s3: new AWS.S3(),
  bucket: 'your-bucket-name',
  key: function (req, file, cb) {
    cb(null, Date.now().toString() + '-' + file.originalname)
  }
})
Monitoring & Logging
Application Logs
Express.js request logging enabled
Database query logging via Drizzle
AI API call logging with response tracking
Error handling with stack traces
AWS CloudWatch Integration
// Add to server/index.ts
const winston = require('winston');
const CloudWatchLogs = require('winston-cloudwatch');
winston.add(new CloudWatchLogs({
  logGroupName: 'privguard-logs',
  logStreamName: 'application-logs'
}));
Health Checks
GET /api/health - Application health status
Database connectivity check
AI service availability check
Security Considerations
Environment Security
All API keys in environment variables
Session secrets properly configured
Database credentials secured
CORS policies configured
Rate limiting implemented
File Upload Security
File type validation
Size limits enforced
Virus scanning recommended
Secure file storage paths
Data Privacy
No sensitive data in logs
Encrypted database connections
Session data secured
GDPR compliance built-in
Troubleshooting
Common Issues
Database Connection Failed

# Check environment variables
echo $DATABASE_URL
# Test connection
psql $DATABASE_URL -c "SELECT 1;"
AI API Errors

# Verify API keys
curl -H "Authorization: Bearer $OPENAI_API_KEY" https://api.openai.com/v1/models
Build Failures

# Clear node modules and reinstall
rm -rf node_modules package-lock.json
npm install
File Upload Issues

# Check upload directory permissions
mkdir -p uploads
chmod 755 uploads
Debug Mode
# Enable debug logging
DEBUG=* npm run dev
Performance Optimization
Database Indexing
Key indexes automatically created by Drizzle schema:

legal_documents.jurisdiction_codes
dpia_assessments.created_by
client_policies.uploaded_by
Caching Strategy
React Query for frontend caching
Express session store for user data
Consider Redis for production scaling
AI API Optimization
Request batching where possible
Response caching for repeated queries
Fallback strategies for API failures
Support & Maintenance
Regular Maintenance Tasks
Database backup verification
Log rotation and cleanup
Dependency updates
Security patch deployment
Performance monitoring review
Scaling Considerations
Horizontal scaling via load balancer
Database read replicas for reporting
CDN for static assets
Container orchestration with Kubernetes
This README provides complete instructions to recreate the PrivGuard platform in any AWS environment. All dependencies, configurations, and deployment options are thoroughly documented.

# PrivGuard - Privacy Compliance Management Platform

A sophisticated privacy compliance management platform that leverages advanced multi-AI technologies to transform complex data protection workflows into intuitive, actionable insights.

## Architecture Overview

PrivGuard is a full-stack TypeScript application with:
- **Frontend**: React SPA with Vite build system
- **Backend**: Express.js REST API
- **Database**: PostgreSQL with Drizzle ORM
- **AI Integration**: Multi-provider AI analysis (OpenAI, Anthropic, ContextGem)
- **File Processing**: Server-side PDF parsing and document analysis

## Core Features

### Privacy Compliance Modules
- **DPIA Assistant**: Wizard-based Data Protection Impact Assessment with step-by-step guidance
- **Gap Detection**: Triple-AI compliance analysis comparing internal policies against regulatory requirements
- **Vendor Assessment**: Contract analysis with Quick Assessment Tools for data sharing agreements
- **Breach Orchestrator**: Incident management with regulatory notification workflows
- **DPO Assistant**: AI-powered chatbot providing privacy guidance with regulatory citations
- **Statutory Rules Engine**: Pre-configured compliance rules mapped to jurisdictions (GDPR, CCPA, etc.)
- **Audit & Training**: Staff training logs with evidence management and audit trails

### Document Processing
- **Legal Document Corpus**: Persistent storage of regulatory texts and legal documents
- **Client Policy Management**: Session-based policy uploads with real-time analysis
README.md
-91
+307
A sophisticated privacy compliance management platform that leverages advanced multi-AI technologies to transform complex data protection workflows into intuitive, actionable insights.
## Features
- **DPIA Assistant**: AI-powered Data Protection Impact Assessment with dual LLM analysis
- **Gap Detection**: Triple-AI analysis (ContextGem, OpenAI, Claude) for compliance gap identification
- **Vendor Assessment**: Contract review and risk assessment with Quick Assessment Tools
- **Breach Orchestrator**: Incident management and regulatory notification workflows
- **DPO Chatbot Assistant**: Privacy guidance with document references
- **Statutory Rules Engine**: Jurisdiction-mapped compliance requirements
- **Audit & Training Logs**: Complete audit trails for all operations
## Architecture Overview
PrivGuard is a full-stack TypeScript application with:
- **Frontend**: React SPA with Vite build system
- **Backend**: Express.js REST API
- **Database**: PostgreSQL with Drizzle ORM
- **AI Integration**: Multi-provider AI analysis (OpenAI, Anthropic, ContextGem)
- **File Processing**: Server-side PDF parsing and document analysis
## Core Features
### Privacy Compliance Modules
- **DPIA Assistant**: Wizard-based Data Protection Impact Assessment with step-by-step guidance
- **Gap Detection**: Triple-AI compliance analysis comparing internal policies against regulatory requirements
- **Vendor Assessment**: Contract analysis with Quick Assessment Tools for data sharing agreements
- **Breach Orchestrator**: Incident management with regulatory notification workflows
- **DPO Assistant**: AI-powered chatbot providing privacy guidance with regulatory citations
- **Statutory Rules Engine**: Pre-configured compliance rules mapped to jurisdictions (GDPR, CCPA, etc.)
- **Audit & Training**: Staff training logs with evidence management and audit trails
### Document Processing
- **Legal Document Corpus**: Persistent storage of regulatory texts and legal documents
- **Client Policy Management**: Session-based policy uploads with real-time analysis
- **AI Document Analysis**: Structured field extraction from privacy policies and contracts
- **Multi-format Support**: PDF, DOCX, and text document processing
### AI Analysis Pipeline
- **ContextGem**: Document intelligence and structured field extraction
- **OpenAI GPT-4o**: Compliance gap analysis and risk assessment
- **Anthropic Claude**: Secondary analysis for validation and alternative perspectives
- **Dual LLM Consensus**: Cross-validation of AI analysis results
## Technology Stack
- **Frontend**: React, TypeScript, Tailwind CSS, shadcn/ui
- **Backend**: Node.js, Express, TypeScript
- **Database**: PostgreSQL with Drizzle ORM
- **AI Integration**: OpenAI GPT-4o, Anthropic Claude, ContextGem
- **File Processing**: PDF parsing, document analysis
## Prerequisites
- Node.js 18+
- PostgreSQL database
- API keys for OpenAI and Anthropic (optional)
## Environment Variables
Create a `.env` file with the following variables:
### Frontend Dependencies
```json
{
  "react": "^18.3.1",
  "react-dom": "^18.3.1",
  "typescript": "5.6.3",
  "vite": "^5.4.14",
  "tailwindcss": "^3.4.17",
  "wouter": "^3.3.5",
  "@tanstack/react-query": "^5.60.5",
  "@radix-ui/react-*": "Various UI components",
  "react-hook-form": "^7.55.0",
  "lucide-react": "^0.453.0",
  "recharts": "^2.15.2"
}
```
### Backend Dependencies
```json
{
  "express": "^4.21.2",
  "drizzle-orm": "^0.39.1",
  "@neondatabase/serverless": "^0.10.4",
  "multer": "^2.0.0",
  "pdf-parse": "^1.1.1",
  "openai": "^4.103.0",
  "@anthropic-ai/sdk": "^0.37.0",
  "passport": "^0.7.0",
  "express-session": "^1.18.1",
  "zod": "^3.24.2"
}
```
## Complete Environment Configuration
### Required Environment Variables
Create a `.env` file with ALL of the following variables:
```env
# Database
# Database Configuration (REQUIRED)
DATABASE_URL=postgresql://username:password@host:port/database
# AI Services (Optional)
OPENAI_API_KEY=your_openai_api_key
ANTHROPIC_API_KEY=your_anthropic_api_key
CONTEXTGEM_API_KEY=your_contextgem_api_key
PGHOST=your_database_host
PGPORT=5432
PGDATABASE=privguard
PGUSER=your_database_user
PGPASSWORD=your_database_password
# AI Service API Keys (At least OPENAI_API_KEY required)
OPENAI_API_KEY=sk-your_openai_api_key_here
ANTHROPIC_API_KEY=sk-ant-your_anthropic_key_here
CONTEXTGEM_API_KEY=your_contextgem_key_here
GEMINI_API_KEY=your_gemini_key_here
GOOGLE_API_KEY=your_google_api_key_here
# Server Configuration
PORT=5000
NODE_ENV=production
```
## Installation
1. Clone the repository:
```bash
git clone <repository-url>
# Session Security (REQUIRED)
SESSION_SECRET=your_secure_random_session_secret_minimum_32_characters
# File Upload Configuration
MAX_FILE_SIZE=50mb
UPLOAD_PATH=./uploads
```
### Database Schema
The application uses Drizzle ORM with the following core tables:
```sql
-- Core tables automatically created by Drizzle migrations
legal_documents         -- Persistent legal/regulatory document corpus
client_policies         -- User-uploaded internal policies  
statutory_rules         -- Pre-configured compliance rules by jurisdiction
dpia_assessments        -- Data Protection Impact Assessments
dpia_workflow_steps     -- DPIA wizard step data
dpia_risks             -- Risk assessments from DPIA analysis
vendor_assessments     -- Contract review and vendor risk analysis
breach_incidents       -- Data breach incident management
audit_evidence         -- Training and audit documentation
document_analysis      -- AI analysis results storage
gap_analysis_results   -- Compliance gap analysis outcomes
```
## Installation & Setup
### Prerequisites
- Node.js 18+ (tested with 18.19.0)
- PostgreSQL 13+ database
- Git
- OpenAI API account (minimum requirement)
- Anthropic API account (optional but recommended)
### Step 1: Clone and Install
```bash
git clone https://github.com/your-org/privguard.git
cd privguard
```
2. Install dependencies:
```bash
npm install
```
3. Set up environment variables:
```bash
### Step 2: Database Setup
```bash
# Create PostgreSQL database
createdb privguard
# Set database URL in .env file
echo "DATABASE_URL=postgresql://username:password@localhost:5432/privguard" >> .env
# Initialize database schema
npm run db:push
```
### Step 3: Environment Configuration
```bash
# Copy template and configure
cp .env.example .env
# Edit .env with your configuration
```
4. Set up the database:
```bash
# Edit .env with your actual values
# CRITICAL: Set at least DATABASE_URL, OPENAI_API_KEY, and SESSION_SECRET
```
### Step 4: Build and Start
```bash
# Development mode
npm run dev
# Production build
npm run build
npm start
```
## API Endpoints Reference
### Authentication & Session Management
- `POST /api/auth/login` - User authentication
- `POST /api/auth/logout` - Session termination
- `GET /api/auth/user` - Current user info
### Dashboard & Statistics
- `GET /api/dashboard` - Dashboard overview with compliance metrics
- `GET /api/dashboard/recent-activity` - Recent system activity
### Document Management
- `POST /api/legal-documents` - Upload legal/regulatory documents
- `GET /api/legal-documents` - List all legal documents
- `PUT /api/legal-documents/:id` - Update document metadata
- `DELETE /api/legal-documents/:id` - Remove document
- `POST /api/client-policies` - Upload internal policies
- `GET /api/client-policies` - List uploaded policies
- `DELETE /api/client-policies/:id` - Remove policy
### Compliance Analysis
- `POST /api/gap-analysis/run` - Execute compliance gap analysis
- `GET /api/gap-analysis/:id` - Retrieve analysis results
- `POST /api/document-analysis` - AI-powered document field extraction
- `GET /api/statutory-rules` - Get compliance rules by jurisdiction
### DPIA (Data Protection Impact Assessment)
- `POST /api/dpia` - Create new DPIA assessment
- `GET /api/dpia` - List all DPIAs
- `GET /api/dpia/:id` - Get specific DPIA
- `PUT /api/dpia/:id/step/:stepNumber` - Update DPIA workflow step
- `POST /api/dpia/:id/document-analysis` - Analyze documents for DPIA
- `POST /api/dpia/:id/risk-assessment` - Generate AI risk assessment
### Vendor Assessment
- `POST /api/vendor-assessments` - Create vendor assessment
- `GET /api/vendor-assessments` - List assessments
- `POST /api/contract-analysis` - Analyze vendor contracts
- `GET /api/vendor-assessments/:id/export` - Export assessment report
### Breach Management
- `POST /api/breach-incidents` - Report data breach
- `GET /api/breach-incidents` - List all incidents
- `PUT /api/breach-incidents/:id` - Update incident status
- `POST /api/breach-incidents/:id/notify` - Send regulatory notifications
### Audit & Training
- `POST /api/audit-evidence` - Upload audit evidence
- `GET /api/audit-evidence` - List audit records
- `GET /api/training-records` - Staff training logs
- `GET /api/audit-evidence/export` - Export audit trail
### DPO Assistant (Chatbot)
- `POST /api/dpo-chat` - Chat with DPO assistant
- `GET /api/dpo-chat/history` - Chat history
- `POST /api/dpo-chat/search` - Search legal documents
## AWS Deployment Guide
### Pre-Deployment Checklist
1. PostgreSQL RDS instance created
2. All environment variables configured in AWS
3. File storage strategy decided (local vs S3)
4. SSL certificate ready for production
5. Domain name configured (optional)
### Deployment Option 1: AWS Elastic Beanstalk
```bash
# Install EB CLI
pip install awsebcli
# Initialize Elastic Beanstalk
eb init privguard --platform node.js
# Create production environment
eb create privguard-prod
# Set all environment variables
eb setenv DATABASE_URL=your_rds_url \
         OPENAI_API_KEY=your_openai_key \
         ANTHROPIC_API_KEY=your_anthropic_key \
         SESSION_SECRET=your_session_secret \
         NODE_ENV=production
# Deploy application
eb deploy
```
### Deployment Option 2: Docker on AWS ECS
```dockerfile
# Use provided Dockerfile
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production
COPY . .
RUN npm run build
EXPOSE 5000
CMD ["npm", "start"]
```
```bash
# Build and push to ECR
aws ecr create-repository --repository-name privguard
docker build -t privguard .
docker tag privguard:latest 123456789.dkr.ecr.us-east-1.amazonaws.com/privguard:latest
docker push 123456789.dkr.ecr.us-east-1.amazonaws.com/privguard:latest
# Create ECS cluster and service with environment variables
```
### Deployment Option 3: AWS EC2 with PM2
```bash
# On EC2 instance
git clone https://github.com/your-org/privguard.git
cd privguard
npm install
npm run build
# Install PM2
npm install -g pm2
# Create ecosystem file
cat > ecosystem.config.js << EOF
module.exports = {
  apps: [{
    name: 'privguard',
    script: 'dist/index.js',
    env: {
      NODE_ENV: 'production',
      PORT: 5000,
      DATABASE_URL: 'your_database_url',
      OPENAI_API_KEY: 'your_openai_key',
      ANTHROPIC_API_KEY: 'your_anthropic_key',
      SESSION_SECRET: 'your_session_secret'
    }
  }]
}
EOF
# Start with PM2
pm2 start ecosystem.config.js
pm2 save
pm2 startup
```
## Database Migration & Data Management
### Initial Setup
```bash
# Push schema to database
npm run db:push
```
5. Build the application:
```bash
npm run build
```
6. Start the server:
```bash
npm start
```
## Development
To run in development mode:
```bash
npm run dev
```
## API Endpoints
### Core Modules
- `GET /api/dashboard` - Dashboard statistics
- `GET /api/statutory-rules` - Compliance rules
- `POST /api/gap-analysis/run` - Run gap analysis
- `POST /api/dpia` - Create DPIA assessment
- `GET /api/vendor-assessments` - Vendor assessments
### Document Management
- `POST /api/legal-documents` - Upload legal documents
- `GET /api/legal-documents` - List legal documents
- `POST /api/client-policies` - Upload client policies
- `GET /api/client-policies` - List client policies
### AI Analysis
- `POST /api/document-analysis` - Analyze documents with AI
- `POST /api/risk-assessment` - Generate risk assessments
## Deployment
### AWS...
[truncated]
[truncated]
