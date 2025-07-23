# Notes App

A personal notes application built with React and AWS Amplify that allows users to create, view, and manage their private notes with optional image attachments.

## 🚀 Features

- **User Authentication**: Secure email-based authentication
- **Personal Notes**: Create and manage your private collection of notes
- **Rich Content**: Add text descriptions and upload images (PNG/JPEG) to your notes
- **Cloud Storage**: All notes and images are securely stored in AWS cloud
- **Responsive Design**: Modern UI using AWS Amplify UI React components
- **Real-time Updates**: Automatic synchronization across devices

## 🏗️ Architecture

This application uses a modern serverless architecture powered by AWS Amplify Gen 2:

### Frontend
- **React 18.3.1** - Modern React with hooks
- **Vite** - Fast build tool and development server
- **AWS Amplify UI React** - Pre-built UI components
- **ES6+ JavaScript** - Modern JavaScript features

### Backend (AWS Amplify)
- **Authentication** - AWS Cognito for user management
- **Database** - AWS AppSync (GraphQL API) with DynamoDB
- **Storage** - AWS S3 for image storage
- **Authorization** - Owner-based access control

### Data Model
```typescript
Note {
  id: string (auto-generated)
  name: string (required)
  description: string (required)
  image: string (optional - filename)
  owner: string (auto-assigned)
}
```

## 📱 How to Use

### Getting Started
1. **Sign Up/Sign In**: Create an account or sign in with your email
2. **Create Notes**: Use the form to add new notes with a name and description
3. **Add Images**: Optionally upload images to make your notes more visual
4. **View Notes**: Browse your notes in the grid layout
5. **Delete Notes**: Remove notes you no longer need
6. **Sign Out**: Securely sign out when done

### Creating a Note
1. Fill in the "Note Name" field (required)
2. Add a "Note Description" (required)
3. Optionally select an image file (PNG or JPEG)
4. Click "Create Note"

### Managing Notes
- All your notes appear in a grid below the creation form
- Each note displays its name, description, and image (if added)
- Click "Delete note" to remove a note permanently
- Notes are private - only you can see your own notes

## 🛠️ Development Setup

### Prerequisites
- Node.js 18+ and npm
- AWS CLI configured (for backend deployment)
- AWS Amplify CLI

### Local Development
```bash
# Install dependencies
npm install

# Start development server
npm run dev

# Build for production
npm run build

# Run linting
npm run lint
```

### Backend Setup
This app requires AWS Amplify backend to be deployed:

```bash
# Install Amplify CLI
npm install -g @aws-amplify/cli

# Deploy backend
npx amplify sandbox

# The deployment will generate amplify_outputs.json needed for the app
```

## 🔧 Technical Details

### Key Components
- **App.jsx** - Main application with authentication wrapper
- **Authenticator** - AWS Amplify authentication component
- **Note Management** - CRUD operations using GraphQL
- **Image Upload** - Direct upload to S3 storage

### Security Features
- Owner-based authorization (users only see their own notes)
- Secure file upload with user-specific S3 paths
- JWT token-based authentication
- HTTPS encryption for all communications

### File Structure
```
src/
  ├── App.jsx          # Main application component
  ├── main.jsx         # React app entry point
  ├── App.css          # Application styles
  └── index.css        # Global styles

amplify/
  ├── auth/            # Authentication configuration
  ├── data/            # Database schema and API
  ├── storage/         # File storage configuration
  └── backend.ts       # Backend configuration
```

## 🚨 Current Status

The app is fully functional but requires AWS backend deployment to run. The missing `amplify_outputs.json` file is generated during backend deployment and contains the necessary AWS service endpoints and configurations.

## 📄 License

This project is part of a personal portfolio demonstrating modern full-stack development with AWS Amplify.
