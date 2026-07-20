# HR Module System

A complete Human Resource management system for job applications with BPMN workflow integration.

## Features

- **Job Posting**: Admin can post new job positions
- **Application Submission**: Candidates can apply for positions
- **Workflow Management**: Full BPMN workflow from application to onboarding
- **Admin Dashboard**: Manage applications through the complete hiring process
- **Authentication**: Password-protected admin dashboard
- **Real-time Database**: Powered by Supabase for persistent data storage

## Setup Instructions

### 1. Set Up Supabase

1. Go to [supabase.com](https://supabase.com) and create a free account
2. Click "New Project" and create a new project
3. Wait for the project to be set up (2-3 minutes)
4. Go to Project Settings → API
5. Copy your:
   - **Project URL** (e.g., https://xyzcompany.supabase.co)
   - **anon public key** (under "Project API keys")

### 2. Create Database Tables

1. In your Supabase project, go to the SQL Editor
2. Copy the contents of `supabase-setup.sql`
3. Paste it into the SQL Editor and run it
4. This will create the `jobs` and `applications` tables with proper security policies

### 3. Configure Your Application

1. Open `index.html` in a text editor
2. Find lines 391-392:
   ```javascript
   const SUPABASE_URL = 'YOUR_SUPABASE_URL';
   const SUPABASE_ANON_KEY = 'YOUR_SUPABASE_ANON_KEY';
   ```
3. Replace the placeholder values with your actual Supabase credentials:
   ```javascript
   const SUPABASE_URL = 'https://your-project.supabase.co';
   const SUPABASE_ANON_KEY = 'your-anon-key-here';
   ```

### 4. Change Admin Password

1. In `index.html`, find line 406:
   ```javascript
   const ADMIN_PASSWORD = 'admin123';
   ```
2. Change 'admin123' to your desired password

## Deployment

### Deploy to Vercel

1. Push your code to GitHub
2. Go to [vercel.com](https://vercel.com)
3. Click "Add New Project" → Import your GitHub repository
4. Vercel will automatically detect the configuration
5. Click "Deploy"

**Important**: Make sure to add your Supabase credentials in the deployed version before going live!

## Usage

### For Candidates

1. Open the application
2. Click "Apply for Job"
3. Fill out the application form
4. Submit your application

### For Admin

1. Click "Admin Dashboard"
2. Enter the admin password
3. Use the tabs to:
   - **Applications**: View and manage applications through the hiring workflow
   - **Post Job**: Create new job postings
   - **Manage Jobs**: View and delete existing job postings

## Workflow Stages

The application follows this BPMN workflow:

1. **Received** → Application submitted
2. **Shortlisted** → Candidate selected for review
3. **Interviewed** → Interview completed
4. **Offer Prepared** → Offer details prepared
5. **Offer Issued** → Offer sent to candidate
6. **Onboarded** → Candidate successfully hired

## Database Schema

### Jobs Table
- `id`: Unique identifier
- `title`: Job title
- `department`: Department name
- `description`: Job description
- `requirements`: Required qualifications
- `salary`: Salary range
- `location`: Job location
- `posted_date`: When the job was posted

### Applications Table
- `id`: Unique identifier
- `job_id`: Reference to job (nullable for general applications)
- `job_title`: Title of the position applied for
- `name`: Applicant's full name
- `email`: Applicant's email
- `phone`: Applicant's phone number
- `experience`: Years of experience
- `cover_letter`: Cover letter text
- `status`: Current workflow status
- `workflow`: Array of completed workflow steps
- `submitted_date`: When application was submitted

## Security Notes

- The admin password is stored in the frontend code. For production, consider using Supabase Auth for secure authentication
- Row Level Security (RLS) is enabled on Supabase tables
- Currently, all operations are public. For production, implement proper authentication policies

## Support

For issues or questions, check the Supabase documentation at [supabase.com/docs](https://supabase.com/docs)
