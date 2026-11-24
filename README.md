# Shopping Agent

[![Firebase](https://img.shields.io/badge/Firebase-Auth%20%26%20Firestore-ffca28)](https://firebase.google.com/) 
[![Gemini](https://img.shields.io/badge/AI-Google%20Gemini-4285f4)](https://ai.google.dev/) 
[![Cloud Run](https://img.shields.io/badge/Hosted-Google%20Cloud%20Run-4285f4)](https://cloud.google.com/run)

Shopping Agent is a user-authenticated AI shopping assistant built with Firebase Authentication, Cloud Firestore, and the Gemini API from Google AI Studio. It lets users sign in, submit shopping queries, store their activity, and receive AI-generated assistance.

The application is designed for deployment on Google Cloud Run, providing a scalable and production-oriented serverless setup.

## Features

- Secure user authentication with Firebase Authentication
- Persistent shopping queries and user activity in Cloud Firestore
- AI-powered product recommendations and shopping support through Gemini
- Personalized conversational experience for signed-in users
- Serverless, scalable deployment with Google Cloud Run
- Centralized API-key and environment configuration for production
- Responsive experience for desktop and mobile browsers

## How It Works

```text
User
  | signs in
  v
Firebase Authentication
  |
  v
Shopping Agent application
  |     |
  |     |-- Save/read query history
  |     v
  |  Cloud Firestore
  |
  |-- Send shopping prompt
  v
Gemini API / Google AI Studio
  |
  v
AI-generated shopping response
```

1. A user creates or signs into an account through Firebase Authentication.
2. Shopping queries are sent through the application to the Gemini API.
3. Gemini generates relevant shopping recommendations and responses.
4. Supported queries and application data can be stored in Cloud Firestore.
5. The application is hosted on Google Cloud Run.

## Technology Stack

| Area | Technology |
| --- | --- |
| Authentication | Firebase Authentication |
| Database | Cloud Firestore |
| AI | Gemini API through Google AI Studio |
| Deployment | Google Cloud Run |
| Containerization | Docker |
| Cloud Platform | Google Cloud Platform |

## Repository Contents

The repository contains:

```text
.
├── README.md              # Project documentation
└── shopping-agent.zip     # Archived application source
```

The source application is currently distributed in `shopping-agent.zip`. Extract it before making local changes:

```bash
unzip shopping-agent.zip
```

On Windows, use File Explorer or:

```bat
Expand-Archive shopping-agent.zip -DestinationPath shopping-agent
```

The extracted folder should contain the application source and its own setup instructions.

## Prerequisites

- A Google account
- A Firebase project
- A Google Cloud project
- A Gemini API key from Google AI Studio
- Docker for local container testing
- Google Cloud CLI for Cloud Run deployment
- Node.js or Python only if the extracted application stack requires it

## Firebase Setup

1. Create or select a Firebase project in the [Firebase Console](https://console.firebase.google.com/).
2. Enable a sign-in method under **Authentication**.
3. Create a Firestore database in **Firestore Database**.
4. Configure Firebase security rules so users can only access their own data.
5. Add the Firebase web configuration to the extracted application.

Use environment variables or Firebase-hosted configuration instead of committing private credentials or API keys.

Example variable names may include:

```env
GEMINI_API_KEY=your_gemini_api_key
FIREBASE_API_KEY=your_firebase_api_key
FIREBASE_AUTH_DOMAIN=your-project.firebaseapp.com
FIREBASE_PROJECT_ID=your-project-id
FIREBASE_STORAGE_BUCKET=your-project.firebasestorage.app
FIREBASE_MESSAGING_SENDER_ID=your_messaging_sender_id
FIREBASE_APP_ID=your_firebase_app_id
```

The exact configuration names depend on the extracted source and framework.

## Local Development

The repository only exposes an archived source package. After extracting `shopping-agent.zip`, enter the extracted project directory and follow its package scripts or dependency instructions.

A typical JavaScript setup is:

```bash
npm install
npm run dev
```

A typical Docker setup is:

```bash
docker build -t shopping-agent .
docker run --env-file .env -p 8080:8080 shopping-agent
```

Use the start command documented inside the extracted source. Do not assume framework-specific commands until they are verified in the extracted project files.

## Firestore Data Model

The implementation may use a structure similar to:

```text
users/{userId}
  profile

queries/{queryId}
  userId
  prompt
  response
  createdAt

users/{userId}/queries/{queryId}
  prompt
  response
  createdAt
```

A subcollection under the authenticated user's document is recommended when Firestore rules must ensure strict per-user ownership.

## Security Recommendations

- Never commit Gemini or Firebase service credentials.
- Store secrets in environment variables or Google Secret Manager.
- Add Firestore rules that restrict reads and writes to the authenticated owner.
- Validate and sanitize user input on the server.
- Apply request limits and rate limiting to protect the Gemini API quota.
- Keep Firebase and IAM permissions limited to the minimum required access.
- Do not expose Firebase Admin credentials in browser code.
- Review generated recommendations rather than presenting them as guaranteed product facts.

## Cloud Run Deployment

Authenticate with Google Cloud:

```bash
gcloud auth login
gcloud config set project YOUR_PROJECT_ID
```

A typical source-based deployment is:

```bash
gcloud run deploy shopping-agent \
  --source . \
  --region YOUR_REGION \
  --allow-unauthenticated
```

Configure Gemini and Firebase values as Cloud Run environment variables or Secret Manager secrets. Update the Firebase allowed domains and application configuration when using a custom domain.

## Testing Checklist

- A new user can sign up and sign in.
- Signed-out users cannot access protected data.
- A signed-in user can submit a shopping query.
- Gemini returns an appropriate response.
- The query and response are saved to the correct Firestore location.
- Users cannot read or modify another user's records.
- Missing environment variables produce clear errors.
- The container starts on the configured Cloud Run port.
- API quota or Gemini service errors are handled gracefully.

## Production Considerations

- Add structured application logging and request tracing.
- Configure monitoring and alerting in Google Cloud.
- Set explicit Cloud Run CPU, memory, concurrency, and timeout values.
- Rate-limit unauthenticated or abusive requests.
- Cache repeated queries only when the resulting responses are safe to reuse.
- Separate development, staging, and production Firebase projects.
- Use Secret Manager for production API keys and service credentials.
- Add automated tests for authentication, Firestore access, and AI request handling.

## Limitations

- Gemini recommendations may be incomplete or outdated.
- Product availability and pricing should be verified with current retailers.
- The current public repository does not include the extracted application source directly; setup details should be confirmed from `shopping-agent.zip`.
- Cloud Run and Gemini usage may incur Google Cloud charges.
- Publicly deployed AI endpoints should include authentication and abuse protection.

## Developer

**Nirbhaysingh A. Chauhan**  
GitHub: [@chauhanlegentyr-droid](https://github.com/chauhanlegentyr-droid)

## Contributing

1. Fork the repository.
2. Extract and update the archived application source.
3. Create a focused feature branch.
4. Add tests for authentication, Firestore, and Gemini integration.
5. Document configuration and deployment changes.
6. Open a pull request with testing steps and screenshots where relevant.

## License

No license has been specified in this repository. Obtain permission from the owner before reuse or redistribution.
