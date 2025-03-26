# Secure Voting System

A comprehensive digital voting platform focused on secure voter verification with advanced biometric authentication and ID card scanning.

![Secure Voting System](https://via.placeholder.com/800x400?text=Secure+Voting+System)

## 📋 Table of Contents

- [Overview](#overview)
- [Key Features](#key-features)
- [Tech Stack](#tech-stack)
- [Current Implementation](#current-implementation)
- [Demo](#demo)
- [Installation](#installation)
- [Usage](#usage)
- [System Architecture](#system-architecture)
- [AI Models & Verification](#ai-models--verification)
- [Queue Management System](#queue-management-system)
- [Security Features](#security-features)
- [Future Scaling](#future-scaling)
- [Contributing](#contributing)
- [License](#license)

## 🔍 Overview

The Secure Voting System is a modern, accessible, and highly secure platform designed to streamline the voter verification process before voting on EVM machines. It combines cutting-edge biometric verification with traditional identification methods to ensure that only authorized voters can participate in elections, while maintaining the integrity of the actual voting process which occurs on separate EVM machines.

## ✨ Key Features

- **Dual-factor Authentication**
  - Face recognition verification using advanced ML models
  - ID card scanning and validation with AI-powered verification
  
- **Admin Dashboard**
  - Voter registration and verification management
  - Real-time queue monitoring
  - Verification process analytics
  
- **User Portal**
  - Secure login with biometric verification
  - Real-time queue position tracking
  - Digital verification token generation
  - Queue position notification
  
- **Security Measures**
  - End-to-end encryption
  - Audit trail for all system activities
  - Fallback mechanisms for exceptional cases
  - Secure infrastructure

## 🛠️ Tech Stack

### Frontend
- **React** - JavaScript library for building user interfaces
- **Material-UI** - React component library implementing Google's Material Design
- **React Router** - Routing library for React applications
- **React Webcam** - Camera integration for biometric verification

### Backend & Services
- **authservices.js** - Custom authentication service using local storage (current implementation)
- **Firebase** - Planned for future scaling (Authentication, Firestore, Storage)
  
### AI/ML Components
- **Face-api.js** - JavaScript API for face detection and recognition
  - SSD MobileNet v1 - For fast and accurate face detection
  - Face Landmark 68 - For facial landmarks detection
  - Face Recognition Model - For matching faces against reference images
- **TensorFlow.js** - Machine learning library for facial recognition models
- **Google Gemini API** - For OCR and advanced ID verification:
  - Text extraction from ID cards
  - ID validity checking
  - Information verification against voter database

### Development Tools
- **Vite** - Next-generation frontend tooling
- **ESLint** - Code quality and style checking

## 💻 Current Implementation

The system currently uses a custom implementation of authentication and data storage:

- **Local Authentication** - User data is stored in browser's local storage via `authservices.js`
- **Local Data Persistence** - Election data, voter information, and voting records are stored locally
- **API Simulation** - Backend API endpoints are simulated locally for development purposes

This approach allows for rapid development and testing without external dependencies. The system is designed with a clear separation of concerns to facilitate easy migration to Firebase services in the future.

## 🎮 Demo

For demonstration purposes, you can use the following admin credentials:
- **Email**: admin@voting-system.com
- **Password**: admin123

## 🚀 Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/secure-voting-system.git
   cd secure-voting-system
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Run the development server**
   ```bash
   npm run dev
   ```

## 📖 Usage

### Admin Portal
1. Login using admin credentials
2. Manage voter verification processes
3. Register and verify voters
4. Monitor queue status in real-time
5. View verification analytics and reports

### Voter Portal
1. Register as a new voter (requires ID card)
2. Complete face recognition setup
3. Login with face verification
4. Receive a queue token number
5. Track waiting time in real-time
6. Get verified before proceeding to EVM for actual voting

## 🧠 AI Models & Verification

### Face Detection & Recognition
The system uses a combination of several pre-trained models from face-api.js:

1. **SSD MobileNet v1**
   - Lightweight face detection model optimized for web applications
   - Fast detection with good accuracy even in various lighting conditions
   - Used for initial face detection in the verification flow

2. **Face Landmark 68 Model**
   - Detects 68 specific points on a face
   - Used for precise face alignment and normalization
   - Helps improve recognition accuracy by standardizing face orientation

3. **Face Recognition Model**
   - 128-dimension face embeddings to capture unique facial characteristics
   - Based on a modified version of the FaceNet architecture
   - Used for comparing live faces with stored face templates

### ID Card Verification with Gemini API
The system leverages Google's Gemini API for advanced ID card verification:

1. **Document OCR**
   - Extracts text information from ID cards
   - Recognizes different ID card formats and layouts
   - Processes both printed and handwritten text

2. **ID Validation**
   - Verifies security features on ID cards (when visible)
   - Checks for ID tampering or manipulation
   - Validates ID authenticity based on format and expected features

3. **Information Verification**
   - Cross-references extracted information with voter database
   - Verifies name, ID number, and other identifying information
   - Flags discrepancies for admin review

## 🔢 Queue Management System

To streamline the voting day experience, the system implements a real-time queue management system:

1. **Token Generation**
   - After successful verification, voters receive a unique queue token number
   - Tokens are generated sequentially based on verification completion

2. **Real-time Status Tracking**
   - Voters can track their position in the queue from the app
   - Estimated waiting time is calculated and displayed
   - Notifications are sent as their turn approaches

3. **Admin Monitoring**
   - Admins can view the current queue status in real-time
   - Manage queue flow and adjust processing speed
   - Identify and resolve bottlenecks in the verification process

The queue system integrates with the verification process while maintaining separation from the actual voting, which happens on EVM machines to ensure voting integrity and security.

## 🏗️ System Architecture

The system follows a client-server architecture with local storage currently serving as the backend infrastructure:

```
┌─────────────────┐      ┌───────────────────────┐
│                 │      │                        │
│  React Frontend ├──────┤ authservices.js        │
│                 │      │ (Local Storage)        │
└────────┬────────┘      └───────────────────────┘
         │                         
         │                        
┌────────▼────────┐      
│                 │      
│ Face-api.js &   │      
│ TensorFlow.js   │      
│                 │      
└─────────────────┘      
         │                        
         │                        
┌────────▼────────┐      
│                 │      
│ Gemini API      │      
│ (OCR & ID Check)│      
│                 │      
└─────────────────┘      
```

## 🔒 Security Features

1. **Biometric Authentication**
   - Face recognition using TensorFlow.js and face-api.js
   - Multiple facial angle capture for increased security

2. **Document Verification**
   - ID card scanning and validation using Gemini API
   - Verification against registered voter database

3. **Data Protection**
   - Data encryption in local storage
   - Secure session management
   - No persistent storage of biometric data on client devices

4. **System Security**
   - CORS configuration to prevent unauthorized access
   - Input validation and sanitization
   - Comprehensive audit logging

## ⚠️ Important Note

This system is specifically designed for voter verification and queue management **before** the actual voting process. The actual voting happens on EVM (Electronic Voting Machines) to maintain the highest standards of election integrity and security. This approach provides:

1. **Separation of Concerns**
   - Verification system handles identity confirmation only
   - Actual vote casting happens on separate, secure EVMs

2. **Enhanced Security**
   - Dual-system approach prevents single points of failure
   - Isolated voting system protects against digital attacks

3. **Regulatory Compliance**
   - Adheres to election commission guidelines for electronic voting
   - Maintains paper trail and audit capabilities of EVMs

## 🚀 Future Scaling

The system is designed to be easily scaled with Firebase implementation:

### Planned Firebase Integration
- **Firebase Authentication** - For secure user management
- **Firestore Database** - For scalable, real-time data storage
- **Firebase Storage** - For secure storage of ID cards and biometric templates
- **Firebase Cloud Functions** - For serverless backend operations

When implemented, the architecture will evolve to:

```
┌─────────────────┐      ┌──────────────────┐
│                 │      │                   │
│  React Frontend ├──────┤ Firebase Services │
│                 │      │                   │
└────────┬────────┘      └──────────────────┘
         │                        │
         │                        │
┌────────▼────────┐      ┌────────▼────────┐
│                 │      │                  │
│ Face-api.js &   │      │ Firestore       │
│ TensorFlow.js   │      │ (Database)      │
│                 │      │                  │
└─────────────────┘      └──────────────────┘
         │                        │
         │                        │
┌────────▼────────┐      ┌────────▼────────┐
│                 │      │                  │
│ Gemini API      │      │ Firebase Storage │
│ (OCR & ID Check)│      │ (Assets)         │
│                 │      │                  │
└─────────────────┘      └──────────────────┘
```

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

---

Developed with ❤️ by Brain.freeze() team for secure and transparent elections.
