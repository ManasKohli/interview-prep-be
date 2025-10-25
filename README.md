# Interview Prep Backend

## Purpose

Automated interview detection and preparation service. Monitors Gmail for interview invites, extracts structured data, generates AI-powered study materials, and manages calendar integrations.

## System Design

**Tech Stack**: Python 3.11+, FastAPI, PostgreSQL, SQLAlchemy (async)

**Core Services**:
- Email monitoring and parsing via Gmail API
- Calendar scheduling via Google Calendar API  
- AI prep generation via OpenAI API
- Data persistence in PostgreSQL

**Architecture Pattern**: RESTful API with background workers for async processing

**Key Endpoints**:
- `POST /api/v1/interviews/detect` - Trigger email scan
- `GET /api/v1/interviews/{id}` - Retrieve interview details
- `POST /api/v1/interviews/{id}/generate-prep` - Generate study materials
- `POST /api/v1/interviews/{id}/schedule` - Add prep blocks to calendar

## Data Flow

1. **Email Detection**: Background worker polls Gmail API using IMAP push notifications
2. **Parsing**: NLP extracts company, role, interview type, date from email body
3. **Storage**: Structured data persisted to PostgreSQL with deduplication logic
4. **AI Generation**: OpenAI API generates role-specific prep questions based on job description
5. **Calendar Integration**: Google Calendar API creates prep event suggestions
6. **API Response**: REST endpoints serve processed data to frontend

## Security & Auth

- OAuth 2.0 for Google service authentication
- Credential encryption at rest using AWS KMS
- API authentication via JWT tokens
- Rate limiting on external API calls (OpenAI, Gmail)