# Developer Setup Guide

## Prerequisites

Before you can run this notes app locally, you'll need:

1. **Node.js 18+** and **npm**
2. **AWS CLI** configured with your credentials
3. **AWS Amplify CLI** for backend deployment

## Quick Start

### 1. Clone and Install Dependencies
```bash
git clone <repository-url>
cd notesapp
npm install
```

### 2. AWS Setup (Required for Full Functionality)

#### Option A: Deploy Your Own Backend
```bash
# Install Amplify CLI globally
npm install -g @aws-amplify/cli

# Configure AWS credentials (if not already done)
amplify configure

# Deploy the backend
npx amplify sandbox

# This will generate amplify_outputs.json with your AWS endpoints
```

#### Option B: Use Mock Configuration (Development Only)
The repository includes a mock `amplify_outputs.json` for development purposes. This allows you to:
- Build the application
- See the UI and authentication forms
- Test frontend functionality

**Note**: With mock configuration, actual backend features won't work (authentication, data storage, etc.)

### 3. Start Development Server
```bash
npm run dev
```

Visit `http://localhost:5173` to see the application.

## Available Scripts

```bash
npm run dev      # Start development server
npm run build    # Build for production
npm run preview  # Preview production build
npm run lint     # Run ESLint
```

## Project Structure

```
notesapp/
├── src/                    # React source code
│   ├── App.jsx            # Main application component
│   ├── main.jsx           # React entry point
│   ├── App.css            # Application styles
│   └── index.css          # Global styles
├── amplify/               # AWS Amplify backend configuration
│   ├── auth/              # Authentication setup
│   ├── data/              # Database schema and API
│   ├── storage/           # File storage configuration
│   └── backend.ts         # Backend configuration
├── public/                # Static assets
├── amplify_outputs.json   # AWS configuration (generated)
└── package.json           # Dependencies and scripts
```

## Backend Configuration

### Authentication (`amplify/auth/resource.ts`)
- Email-based authentication using AWS Cognito
- User registration and sign-in functionality

### Data Model (`amplify/data/resource.ts`)
```typescript
Note {
  name: string       // Required: Note title
  description: string // Required: Note content
  image: string      // Optional: Image filename
  owner: string      // Auto-assigned: User who created the note
}
```

### Storage (`amplify/storage/resource.ts`)
- AWS S3 bucket for image storage
- User-specific access paths: `media/{user-id}/*`
- Supports PNG and JPEG image uploads

## Environment Variables

When deploying to production, ensure you have:
- AWS credentials configured
- Proper IAM permissions for Amplify services
- Region set to your preferred AWS region

## Deployment

### Local Development
```bash
npx amplify sandbox  # Starts local backend
npm run dev          # Starts frontend
```

### Production
```bash
npx amplify deploy   # Deploys backend to AWS
npm run build        # Builds frontend
```

## Troubleshooting

### Common Issues

1. **Missing amplify_outputs.json**
   ```bash
   # Deploy backend to generate the file
   npx amplify sandbox
   ```

2. **AWS Authentication Errors**
   ```bash
   # Reconfigure AWS credentials
   amplify configure
   ```

3. **Build Failures**
   ```bash
   # Clear node_modules and reinstall
   rm -rf node_modules package-lock.json
   npm install
   ```

4. **CORS Issues**
   - Check your AWS Amplify backend configuration
   - Ensure proper authentication mode is set

### Development Tips

- Use browser developer tools to debug authentication flows
- Check AWS CloudWatch logs for backend errors
- Monitor AWS AppSync API in the AWS Console
- Use AWS S3 console to verify file uploads

## Architecture Benefits

This setup provides:
- **Type Safety**: TypeScript integration with AWS services
- **Real-time Data**: GraphQL subscriptions for live updates
- **Secure by Default**: Owner-based authorization
- **Scalable**: Serverless architecture scales automatically
- **Cost Effective**: Pay only for what you use

## Next Steps

1. Deploy your own AWS backend
2. Customize the UI components
3. Add new features (search, categories, sharing)
4. Set up CI/CD pipeline for automated deployments
5. Add comprehensive testing (unit, integration, e2e)

## Support

For AWS Amplify specific issues:
- [AWS Amplify Documentation](https://docs.amplify.aws/)
- [AWS Amplify GitHub](https://github.com/aws-amplify/amplify-js)

For React/Vite issues:
- [React Documentation](https://reactjs.org/)
- [Vite Documentation](https://vitejs.dev/)