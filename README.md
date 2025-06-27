# 🤖 AI Resume Builder

> **Create professional, ATS-optimized resumes in minutes with the power of AI**

[![Live Demo](https://img.shields.io/badge/Live%20Demo-Visit%20Site-blue?style=for-the-badge)](https://rainbow-clafoutis-fa50f5.netlify.app/)
[![YouTube](https://img.shields.io/badge/YouTube-Tutorials-red?style=for-the-badge&logo=youtube)](https://www.youtube.com/playlist?list=PLrZbkNpNVSwz55T6S0GUK-EWWjnT9OOhs)
[![GitHub](https://img.shields.io/badge/GitHub-Repository-black?style=for-the-badge&logo=github)](https://github.com/HorizonHnk/AI-Resume-Builder.git)

![AI Resume Builder Architecture](https://github.com/HorizonHnk/AI-Resume-Builder/blob/main/Smart%20Resume%20Builder.png?raw=true)

## 🚀 Features

### ✨ **AI-Powered Content Generation**
- **Smart Summaries**: Generate compelling professional summaries tailored to your experience
- **Bullet Point Enhancement**: Transform basic job descriptions into impactful achievement statements
- **Skills Suggestions**: Get relevant skill recommendations based on job descriptions
- **Job-Specific Optimization**: Tailor your resume content for specific positions

### 🎯 **ATS Optimization**
- **Compatibility Analysis**: Score your resume against ATS systems (0-100 scale)
- **Keyword Matching**: Identify missing keywords from job descriptions
- **Format Optimization**: Ensure your resume passes through applicant tracking systems
- **Improvement Suggestions**: Get actionable recommendations to boost your ATS score

### 📄 **Professional Templates**
- **Modern Professional**: Clean, contemporary design for tech and business roles
- **Creative Design**: Eye-catching layout for creative professionals
- **Executive**: Sophisticated template for senior-level positions
- **Real-time Preview**: See changes instantly as you edit

### 💾 **Cloud Storage & Management**
- **Firebase Integration**: Secure cloud storage for all your resumes
- **Auto-save**: Never lose your work with automatic saving
- **Resume Library**: Manage multiple resumes for different job applications
- **Version Control**: Track changes and maintain resume versions

### 📤 **Export Options**
- **PDF Export**: High-quality PDF generation with professional formatting
- **Word Document**: Editable .docx files for further customization
- **Direct Download**: One-click download functionality
- **Print Optimization**: Perfect formatting for both digital and print use

## 🛠️ Tech Stack

### **Frontend**
- ![React](https://img.shields.io/badge/React-19.1.0-blue?logo=react) - Modern UI library
- ![Vite](https://img.shields.io/badge/Vite-7.0.0-purple?logo=vite) - Lightning-fast build tool
- ![TailwindCSS](https://img.shields.io/badge/TailwindCSS-4.1.11-cyan?logo=tailwindcss) - Utility-first CSS framework
- ![Lucide React](https://img.shields.io/badge/Lucide-Icons-orange) - Beautiful SVG icons

### **Backend & Services**
- ![Firebase](https://img.shields.io/badge/Firebase-11.9.1-orange?logo=firebase) - Authentication & Database
- ![Firestore](https://img.shields.io/badge/Firestore-Database-yellow?logo=firebase) - NoSQL cloud database
- ![Google AI](https://img.shields.io/badge/Gemini%20AI-Content%20Generation-blue?logo=google) - AI-powered content generation

### **Document Processing**
- ![DOCX](https://img.shields.io/badge/DOCX-Word%20Export-blue) - Word document generation
- ![File Saver](https://img.shields.io/badge/FileSaver-Download-green) - Client-side file downloads

## 🏗️ Code Architecture & Implementation

### **Component Architecture**

The application follows a **modular component architecture** with clear separation of concerns:

```javascript
// Main App Structure
App.jsx (Root)
├── AuthProvider (Context)
├── ErrorBoundary (Error Handling)
├── ProtectedRoute (Route Guard)
├── DashboardHeader (Navigation)
└── ResumeBuilder (Main Component)
```

### **Core Components Breakdown**

#### 🔐 **Authentication System**
```javascript
// src/contexts/AuthContext.jsx
const AuthContext = createContext();

export function AuthProvider({ children }) {
  const [currentUser, setCurrentUser] = useState(null);
  const [loading, setLoading] = useState(true);
  
  // Firebase Auth Methods
  async function signup(email, password, displayName) {
    const result = await createUserWithEmailAndPassword(auth, email, password);
    await updateProfile(result.user, { displayName });
    return result;
  }
  
  // Google OAuth Integration
  async function loginWithGoogle() {
    return await signInWithPopup(auth, googleProvider);
  }
}
```

**Key Features:**
- **Real-time Auth State**: Uses `onAuthStateChanged` for persistent sessions
- **Error Handling**: Comprehensive error messages for all auth scenarios
- **Google OAuth**: Seamless Google sign-in integration
- **Profile Management**: Display name and email management

#### 📝 **Resume Builder Component**
```javascript
// src/components/ResumeBuilder.jsx
const ResumeBuilder = () => {
  // State Management
  const [resumeData, setResumeData] = useState({
    personalInfo: { name: '', email: '', phone: '', location: '', summary: '' },
    experience: [], education: [], projects: [], certifications: [], skills: []
  });
  
  // AI Integration
  const callGeminiAPI = async (prompt, type) => {
    const response = await fetch(geminiUrl, {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({
        contents: [{ parts: [{ text: prompt }] }],
        generationConfig: { temperature: 0.7, topK: 40, topP: 0.95 }
      })
    });
    return response.json();
  };
  
  // Auto-save Implementation
  useEffect(() => {
    const timeoutId = setTimeout(async () => {
      if (currentResumeId && resumeData) {
        await ResumeFirestoreService.updateResume(currentResumeId, resumeData);
      }
    }, 3000);
    return () => clearTimeout(timeoutId);
  }, [resumeData, currentResumeId]);
};
```

**Advanced Features:**
- **Real-time Preview**: Live updates as user types
- **Smart Auto-save**: Debounced saving every 3 seconds
- **Section Management**: Dynamic addition/removal of resume sections
- **Template System**: Switchable professional templates
- **Validation**: Real-time form validation with error states

### **🤖 AI Integration Deep Dive**

#### **Gemini AI Service**
```javascript
// AI Content Generation Pipeline
const generateAIContent = async (section, context) => {
  let prompt = '';
  const jobAnalysis = aiSuggestions.jobAnalysis;
  
  switch (section) {
    case 'summary':
      prompt = `Create a professional resume summary for: ${context}
      Target Role: ${jobAnalysis?.role_summary}
      Experience Level: ${jobAnalysis?.experience_level}
      Key Requirements: ${jobAnalysis?.key_requirements?.join(', ')}
      Make it compelling and 2-3 sentences. Return ONLY the summary text.`;
      break;
      
    case 'experience':
      prompt = `Generate 3-4 professional bullet points for: ${context}
      Optimize for: ${jobAnalysis?.role_summary}
      Include keywords: ${jobAnalysis?.suggested_keywords?.join(', ')}
      Use action verbs and quantify achievements.`;
      break;
  }
  
  return await callGeminiAPI(prompt, section);
};
```

**AI Features Implementation:**
- **Context-Aware Generation**: Uses job description for targeted content
- **Fallback System**: Provides default content when API fails
- **JSON Response Parsing**: Handles both structured and text responses
- **Rate Limiting**: Built-in request throttling

#### **ATS Optimization Engine**
```javascript
// ATS Analysis Implementation
const analyzeATS = async () => {
  const resumeText = generateResumeText();
  const prompt = `
    Analyze this resume against the job description for ATS optimization.
    
    Job Description: ${jobDescription}
    Resume Content: ${resumeText}
    
    Provide analysis in JSON format:
    {
      "score": 65,
      "strengths": ["Relevant experience", "Good use of action verbs"],
      "improvements": ["Add more keywords", "Include quantified achievements"],
      "keywords": {
        "present": ["JavaScript", "React", "Problem solving"],
        "missing": ["Python", "AWS", "Agile methodology"]
      }
    }
  `;
  
  const analysis = await callGeminiAPI(prompt, 'ats');
  return parseGeminiJSON(analysis);
};
```

### **🔥 Firebase Integration**

#### **Firestore Database Service**
```javascript
// src/services/firestoreService.js
export class ResumeFirestoreService {
  
  // Optimized Query (No Composite Index Required)
  static async getUserResumes(userId) {
    const resumesQuery = query(
      collection(db, RESUMES_COLLECTION),
      where('userId', '==', userId)
    );
    
    const querySnapshot = await getDocs(resumesQuery);
    const resumes = [];
    
    querySnapshot.forEach((doc) => {
      const data = doc.data();
      resumes.push({
        id: doc.id,
        ...data,
        createdAt: data.createdAt?.toDate() || new Date(),
        updatedAt: data.updatedAt?.toDate() || new Date()
      });
    });
    
    // Client-side sorting (avoids Firestore composite index)
    return resumes.sort((a, b) => b.updatedAt - a.updatedAt);
  }
  
  // Auto-save with Debouncing
  static autoSaveTimeout = null;
  
  static autoSave(resumeId, resumeData, delay = 2000) {
    if (this.autoSaveTimeout) clearTimeout(this.autoSaveTimeout);
    
    this.autoSaveTimeout = setTimeout(async () => {
      try {
        if (resumeId) {
          await this.updateResume(resumeId, resumeData);
          console.log('💾 Auto-saved resume');
        }
      } catch (error) {
        console.error('❌ Auto-save failed:', error);
      }
    }, delay);
  }
}
```

**Database Schema:**
```javascript
// Firestore Collections Structure
resumes/ {
  resumeId: {
    userId: string,
    title: string,
    resumeData: {
      personalInfo: {...},
      experience: [...],
      education: [...],
      projects: [...],
      certifications: [...],
      skills: [...]
    },
    createdAt: timestamp,
    updatedAt: timestamp,
    isTemplate: boolean
  }
}

users/ {
  userId: {
    profile: {...},
    preferences: {...},
    updatedAt: timestamp
  }
}
```

### **📄 Document Export System**

#### **PDF Generation**
```javascript
// Professional PDF Export
const exportToPDF = () => {
  const resumeElement = document.getElementById('resume-preview');
  const currentTemplate = templates[selectedTemplate];
  
  const htmlContent = `
    <!DOCTYPE html>
    <html>
    <head>
      <style>
        body { font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif; }
        .header { 
          background: ${currentTemplate.headerBg}; 
          color: white; 
          padding: 1.5rem; 
        }
        .section-title { 
          border-bottom: 2px solid #e5e7eb; 
          padding-bottom: 0.25rem; 
        }
        @media print { 
          body { -webkit-print-color-adjust: exact; } 
        }
      </style>
    </head>
    <body>${generateFormattedContent()}</body>
    </html>
  `;
  
  const blob = new Blob([htmlContent], { type: 'text/html' });
  const url = URL.createObjectURL(blob);
  window.open(url, '_blank');
};
```

#### **Word Document Export**
```javascript
// Advanced Word Export with DOCX library
const exportToWord = async () => {
  const doc = new Document({
    styles: { paragraphStyles: [/* Custom styles */] },
    sections: [{
      children: await generateWordContent()
    }]
  });
  
  const blob = await Packer.toBlob(doc);
  saveAs(blob, `${resumeData.personalInfo.name}_Resume.docx`);
};

// Word Content Generation
const generateWordContent = async () => {
  const children = [];
  
  // Header with styling
  children.push(new Paragraph({
    children: [new TextRun({
      text: resumeData.personalInfo.name,
      bold: true, size: 36, color: "FFFFFF"
    })],
    alignment: AlignmentType.CENTER,
    shading: { type: ShadingType.SOLID, color: "2563EB" }
  }));
  
  return children;
};
```

### **🎨 Template System**

#### **Dynamic Template Configuration**
```javascript
// Template System Implementation
const templates = {
  modern: {
    name: 'Modern Professional',
    colors: 'bg-gradient-to-br from-blue-50 to-indigo-50 border-l-4 border-blue-500',
    headerBg: 'bg-blue-600',
    textColor: 'text-gray-800',
    accentColor: '#2563eb'
  },
  creative: {
    name: 'Creative Design',
    colors: 'bg-gradient-to-br from-purple-50 to-pink-50 border-l-4 border-purple-500',
    headerBg: 'bg-purple-600',
    textColor: 'text-gray-800',
    accentColor: '#9333ea'
  }
};

// Dynamic Template Application
const applyTemplate = (templateKey) => {
  const template = templates[templateKey];
  return {
    containerClass: template.colors,
    headerStyle: { backgroundColor: template.accentColor },
    textClass: template.textColor
  };
};
```

### **⚡ Performance Optimizations**

#### **Code Splitting & Lazy Loading**
```javascript
// vite.config.js - Advanced Bundling
export default defineConfig({
  build: {
    rollupOptions: {
      output: {
        manualChunks(id) {
          if (id.includes('node_modules')) {
            if (id.includes('react') || id.includes('react-dom')) {
              return 'react-vendor';
            }
            if (id.includes('firebase')) {
              return 'firebase-vendor';
            }
            if (id.includes('docx') || id.includes('file-saver')) {
              return 'export-vendor';
            }
            return 'vendor';
          }
        }
      }
    },
    chunkSizeWarningLimit: 1000
  }
});
```

#### **State Management Optimization**
```javascript
// Optimized State Updates
const updatePersonalInfo = useCallback((field, value) => {
  setResumeData(prev => ({
    ...prev,
    personalInfo: { ...prev.personalInfo, [field]: value }
  }));
  validateField('personal', field, value);
}, []);

// Debounced Auto-save
const debouncedSave = useMemo(
  () => debounce(async (data) => {
    await ResumeFirestoreService.updateResume(currentResumeId, data);
  }, 3000),
  [currentResumeId]
);
```

### **🛡️ Error Handling & Validation**

#### **Comprehensive Error Boundary**
```javascript
// Error Boundary Implementation
class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false, error: null };
  }

  static getDerivedStateFromError(error) {
    return { hasError: true, error };
  }

  componentDidCatch(error, errorInfo) {
    console.error('Error Boundary caught:', error, errorInfo);
    // Send to monitoring service
  }

  render() {
    if (this.state.hasError) {
      return <ErrorFallback error={this.state.error} />;
    }
    return this.props.children;
  }
}
```

#### **Form Validation System**
```javascript
// Real-time Validation
const validateField = (section, field, value) => {
  const errors = { ...validationErrors };
  const key = `${section}.${field}`;

  if (!value.trim()) {
    if (['name', 'email'].includes(field)) {
      errors[key] = `${field.charAt(0).toUpperCase() + field.slice(1)} is required`;
    }
  } else {
    if (field === 'email' && !validateEmail(value)) {
      errors[key] = 'Please enter a valid email address';
    } else if (field === 'phone' && value && !validatePhone(value)) {
      errors[key] = 'Please enter a valid phone number';
    } else {
      delete errors[key];
    }
  }

  setValidationErrors(errors);
};

// Email Validation Regex
const validateEmail = (email) => {
  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  return emailRegex.test(email);
};
```

### **📱 Responsive Design System**

#### **Mobile-First Approach**
```javascript
// Responsive Layout Implementation
const ResponsiveLayout = () => {
  const [sidebarOpen, setSidebarOpen] = useState(false);
  const [isMobile, setIsMobile] = useState(false);

  useEffect(() => {
    const checkMobile = () => {
      setIsMobile(window.innerWidth < 1024);
    };
    
    window.addEventListener('resize', checkMobile);
    checkMobile();
    
    return () => window.removeEventListener('resize', checkMobile);
  }, []);

  return (
    <div className="flex flex-col lg:flex-row min-h-screen">
      {/* Mobile Sidebar Overlay */}
      {sidebarOpen && isMobile && (
        <div className="lg:hidden fixed inset-0 z-40 bg-black bg-opacity-50" 
             onClick={() => setSidebarOpen(false)} />
      )}
      
      {/* Responsive Editor Panel */}
      <div className={`
        fixed lg:relative inset-y-0 left-0 z-50 lg:z-0
        w-full sm:w-96 lg:w-1/2 xl:w-2/5
        transform transition-transform duration-300 ease-in-out lg:transform-none
        ${sidebarOpen ? 'translate-x-0' : '-translate-x-full lg:translate-x-0'}
      `}>
        {/* Editor Content */}
      </div>
    </div>
  );
};
```

### **🔍 Advanced Features**

#### **Real-time Collaboration (Future)**
```javascript
// WebSocket Integration for Real-time Updates
const useRealtimeUpdates = (resumeId) => {
  useEffect(() => {
    if (!resumeId) return;
    
    const unsubscribe = onSnapshot(
      doc(db, 'resumes', resumeId),
      (doc) => {
        if (doc.exists()) {
          const data = doc.data();
          setResumeData(data.resumeData);
        }
      }
    );
    
    return unsubscribe;
  }, [resumeId]);
};
```

#### **Advanced Analytics**
```javascript
// Usage Analytics Implementation
const trackUserAction = (action, metadata = {}) => {
  // Firebase Analytics
  logEvent(analytics, action, {
    timestamp: new Date().toISOString(),
    userId: currentUser?.uid,
    ...metadata
  });
};

// Track AI Usage
const trackAIUsage = (feature, success) => {
  trackUserAction('ai_feature_used', {
    feature,
    success,
    timestamp: Date.now()
  });
};
```

## 🏗️ Project Structure

```
AI-Resume-Builder/
├── 📁 src/
│   ├── 📁 components/              # React Components
│   │   ├── 🔐 LoginPage.jsx        # Authentication UI
│   │   │   ├── Email/Password form
│   │   │   ├── Google OAuth button
│   │   │   ├── Form validation
│   │   │   └── Error handling
│   │   ├── 📝 SignupPage.jsx       # User Registration
│   │   │   ├── Multi-step form
│   │   │   ├── Password strength indicator
│   │   │   ├── Terms acceptance
│   │   │   └── Email verification
│   │   ├── 🏠 WelcomePage.jsx      # Landing Page
│   │   │   ├── Hero section with animations
│   │   │   ├── Feature showcase
│   │   │   ├── Testimonials carousel
│   │   │   ├── Pricing tiers
│   │   │   └── Footer with links
│   │   └── 🔧 ResumeBuilder.jsx    # Main Builder (2000+ lines)
│   │       ├── State management (12 useState hooks)
│   │       ├── AI integration (5 different prompts)
│   │       ├── Real-time preview
│   │       ├── Auto-save functionality
│   │       ├── Template system (3 templates)
│   │       ├── Export system (PDF/Word)
│   │       ├── ATS optimization
│   │       ├── Form validation
│   │       └── Mobile responsive design
│   │
│   ├── 📁 contexts/                # React Context API
│   │   └── 🔐 AuthContext.jsx      # Authentication State
│   │       ├── Firebase Auth integration
│   │       ├── User session management
│   │       ├── Error handling (10+ error types)
│   │       ├── Google OAuth setup
│   │       └── Auth state persistence
│   │
│   ├── 📁 firebase/                # Firebase Configuration
│   │   └── ⚙️ config.js            # Firebase Setup
│   │       ├── Environment variables
│   │       ├── Auth configuration
│   │       ├── Firestore setup
│   │       ├── Google provider config
│   │       └── Error handling
│   │
│   ├── 📁 services/                # External Services
│   │   └── 🗄️ firestoreService.js  # Database Operations
│   │       ├── CRUD operations for resumes
│   │       ├── User profile management
│   │       ├── Auto-save with debouncing
│   │       ├── Query optimization
│   │       ├── Error handling
│   │       └── Data validation
│   │
│   ├── 📁 pages/api/               # API Routes
│   │   └── 🤖 gemini.js            # AI API Integration
│   │       ├── Gemini API calls
│   │       ├── Request validation
│   │       ├── Error handling
│   │       ├── Fallback responses
│   │       └── Rate limiting
│   │
│   ├── 📱 App.jsx                  # Main Application
│   │   ├── Error boundary
│   │   ├── Route protection
│   │   ├── Loading states
│   │   ├── Offline mode handling
│   │   └── Header with user menu
│   │
│   ├── 🚀 main.jsx                 # Application Entry Point
│   │   ├── React 19 integration
│   │   ├── StrictMode wrapper
│   │   └── DOM rendering
│   │
│   └── 🎨 index.css                # Global Styles
│       ├── Tailwind CSS imports
│       ├── Custom animations
│       └── Print styles
│
├── 📄 package.json                # Dependencies & Scripts
│   ├── 25+ production dependencies
│   ├── 15+ development dependencies
│   ├── Build scripts
│   └── ESLint configuration
│
├── ⚙️ vite.config.js              # Build Configuration
│   ├── Plugin configuration
│   ├── Code splitting setup
│   ├── Bundle optimization
│   └── Development server config
│
├── 🌍 .env                        # Environment Variables
│   ├── Firebase configuration
│   ├── Gemini API key
│   └── Development settings
│
└── 📝 README.md                   # Documentation
    ├── Setup instructions
    ├── API documentation
    ├── Architecture overview
    └── Contributing guidelines
```

### **Code Quality & Best Practices**

#### **ESLint Configuration**
```javascript
// eslint.config.js
export default [
  js.configs.recommended,
  ...tseslint.configs.recommended,
  {
    files: ['**/*.{js,jsx,ts,tsx}'],
    languageOptions: {
      ecmaVersion: 2020,
      globals: globals.browser,
    },
    plugins: {
      'react-hooks': reactHooks,
      'react-refresh': reactRefresh,
    },
    rules: {
      ...reactHooks.configs.recommended.rules,
      'react-refresh/only-export-components': ['warn', { allowConstantExport: true }],
    },
  },
];
```

#### **TypeScript Integration (Future)**
```typescript
// types/resume.ts
interface ResumeData {
  personalInfo: PersonalInfo;
  experience: Experience[];
  education: Education[];
  projects: Project[];
  certifications: Certification[];
  skills: string[];
}

interface PersonalInfo {
  name: string;
  email: string;
  phone?: string;
  location?: string;
  summary?: string;
}

interface Experience {
  id: string;
  company: string;
  position: string;
  duration: string;
  description: string;
}
```

### **Testing Strategy**

#### **Unit Testing Setup**
```javascript
// __tests__/components/ResumeBuilder.test.jsx
import { render, screen, fireEvent, waitFor } from '@testing-library/react';
import { ResumeBuilder } from '../components/ResumeBuilder';
import { AuthProvider } from '../contexts/AuthContext';

describe('ResumeBuilder', () => {
  test('renders personal information form', () => {
    render(
      <AuthProvider>
        <ResumeBuilder />
      </AuthProvider>
    );
    
    expect(screen.getByLabelText(/full name/i)).toBeInTheDocument();
    expect(screen.getByLabelText(/email/i)).toBeInTheDocument();
  });
  
  test('auto-saves on content change', async () => {
    const mockSave = jest.fn();
    jest.spyOn(ResumeFirestoreService, 'updateResume').mockImplementation(mockSave);
    
    render(<ResumeBuilder />);
    
    fireEvent.change(screen.getByLabelText(/full name/i), { 
      target: { value: 'John Doe' } 
    });
    
    await waitFor(() => expect(mockSave).toHaveBeenCalled(), { timeout: 4000 });
  });
});
```

#### **Integration Testing**
```javascript
// __tests__/integration/auth.test.jsx
describe('Authentication Flow', () => {
  test('complete signup process', async () => {
    render(<App />);
    
    fireEvent.click(screen.getByText(/get started/i));
    fireEvent.change(screen.getByLabelText(/email/i), { 
      target: { value: 'test@example.com' } 
    });
    fireEvent.change(screen.getByLabelText(/password/i), { 
      target: { value: 'password123' } 
    });
    fireEvent.click(screen.getByText(/create account/i));
    
    await waitFor(() => {
      expect(screen.getByText(/resume builder/i)).toBeInTheDocument();
    });
  });
});
```

### **Performance Monitoring**

#### **Bundle Analysis**
```javascript
// Bundle size analysis
import { defineConfig } from 'vite';
import { visualizer } from 'rollup-plugin-visualizer';

export default defineConfig({
  plugins: [
    visualizer({
      filename: 'dist/stats.html',
      open: true,
      gzipSize: true,
      brotliSize: true,
    }),
  ],
});
```

#### **Performance Metrics**
```javascript
// Performance monitoring
const measurePerformance = (name, fn) => {
  return async (...args) => {
    const start = performance.now();
    const result = await fn(...args);
    const end = performance.now();
    
    console.log(`${name} took ${end - start} milliseconds`);
    
    // Send to analytics
    trackUserAction('performance_metric', {
      operation: name,
      duration: end - start,
      timestamp: Date.now()
    });
    
    return result;
  };
};

// Usage
const saveResumeWithMetrics = measurePerformance(
  'save_resume',
  ResumeFirestoreService.saveResume
);
```

## 🚦 Getting Started

### Prerequisites

Before you begin, ensure you have the following installed:
- **Node.js** (v16 or higher)
- **npm** or **yarn** package manager
- **Firebase account** (for authentication and database)
- **Google AI API key** (for Gemini AI integration)

### 📦 Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/HorizonHnk/AI-Resume-Builder.git
   cd AI-Resume-Builder
   ```

2. **Install dependencies**
   ```bash
   npm install
   # or
   yarn install
   ```

3. **Set up environment variables**
   
   Create a `.env` file in the root directory:
   ```env
   # Gemini AI Configuration
   GEMINI_API_KEY=your_gemini_api_key_here
   
   # Firebase Configuration
   VITE_FIREBASE_API_KEY=your_firebase_api_key
   VITE_FIREBASE_AUTH_DOMAIN=your_project.firebaseapp.com
   VITE_FIREBASE_PROJECT_ID=your_project_id
   VITE_FIREBASE_STORAGE_BUCKET=your_project.appspot.com
   VITE_FIREBASE_MESSAGING_SENDER_ID=your_sender_id
   VITE_FIREBASE_APP_ID=your_app_id
   
   # Environment
   NODE_ENV=development
   ```

4. **Start the development server**
   ```bash
   npm run dev
   # or
   yarn dev
   ```

5. **Open your browser**
   
   Navigate to `http://localhost:5173` to see the application running.

### 🔥 Firebase Setup

1. **Create a Firebase project** at [Firebase Console](https://console.firebase.google.com/)

2. **Enable Authentication**
   - Go to Authentication > Sign-in method
   - Enable Email/Password and Google sign-in

3. **Set up Firestore Database**
   - Go to Firestore Database
   - Create database in production mode
   - Set up security rules:
   ```javascript
   rules_version = '2';
   service cloud.firestore {
     match /databases/{database}/documents {
       match /resumes/{resumeId} {
         allow read, write: if request.auth != null && request.auth.uid == resource.data.userId;
       }
       match /users/{userId} {
         allow read, write: if request.auth != null && request.auth.uid == userId;
       }
     }
   }
   ```

4. **Get your Firebase config** from Project Settings > General > Your apps

### 🤖 Google AI (Gemini) Setup

1. **Get API key** from [Google AI Studio](https://makersuite.google.com/app/apikey)
2. **Add the key** to your `.env` file as `GEMINI_API_KEY`

## 📱 Usage

### **Creating Your First Resume**

1. **Sign up/Login** - Create an account or sign in with Google
2. **Add Personal Information** - Fill in your basic details
3. **Paste Job Description** - Add the target job description for AI optimization
4. **Generate AI Content** - Use AI suggestions for summaries, bullet points, and skills
5. **Customize Sections** - Add experience, education, projects, and certifications
6. **Choose Template** - Select from professional templates
7. **Export** - Download as PDF or Word document

### **AI Features**

> **💡 Pro Tip**: Always paste the job description first to get the most relevant AI suggestions!

- **Smart Summaries**: Click "AI Suggest" next to the summary field
- **Enhanced Descriptions**: Use "AI Enhance" on experience and project descriptions
- **Skill Recommendations**: Get relevant skills based on job requirements
- **ATS Analysis**: Check your resume's ATS compatibility score

## 🎥 Video Tutorials

Watch our comprehensive tutorial series on YouTube:

[![YouTube Tutorials](https://img.shields.io/badge/Watch%20Tutorials-YouTube-red?style=for-the-badge&logo=youtube)](https://www.youtube.com/playlist?list=PLrZbkNpNVSwz55T6S0GUK-EWWjnT9OOhs)

**Tutorial Topics:**
- Getting started with AI Resume Builder
- Advanced AI features and optimization
- Export options and best practices
- ATS optimization strategies

## 🤝 Contributing

We welcome contributions from the community! Here's how you can help:

### **Ways to Contribute**
- 🐛 **Report bugs** by opening an issue
- 💡 **Suggest features** or improvements
- 🔧 **Submit pull requests** for bug fixes or new features
- 📝 **Improve documentation** and tutorials
- 🎨 **Design new templates** or improve existing ones

### **Development Process**

1. **Fork the repository**
2. **Create a feature branch**
   ```bash
   git checkout -b feature/amazing-feature
   ```
3. **Make your changes**
4. **Commit your changes**
   ```bash
   git commit -m 'Add some amazing feature'
   ```
5. **Push to the branch**
   ```bash
   git push origin feature/amazing-feature
   ```
6. **Open a Pull Request**

## 🔧 Build & Deployment

### **Development Build**
```bash
npm run dev
```

### **Production Build**
```bash
npm run build
```

### **Preview Production Build**
```bash
npm run preview
```

### **Deploy to Netlify**
1. Connect your GitHub repository to Netlify
2. Set environment variables in Netlify dashboard
3. Deploy automatically on every push to main branch

## 📊 Performance

- ⚡ **Fast Loading**: Optimized with Vite for instant development
- 📱 **Responsive Design**: Works perfectly on all devices
- 🔄 **Real-time Updates**: Live preview as you type
- 💾 **Auto-save**: Never lose your work
- 🌐 **PWA Ready**: Installable as a web app

## 🛡️ Security

- 🔐 **Firebase Authentication**: Secure user management
- 🔒 **Data Encryption**: All data encrypted in transit and at rest
- 👤 **User Privacy**: Data is private and only accessible by the user
- 🛠️ **Security Rules**: Firestore rules prevent unauthorized access

## 📈 Analytics & Monitoring

- 📊 **Usage Analytics**: Track feature usage and performance
- 🐛 **Error Monitoring**: Automatic error reporting and logging
- 📈 **Performance Metrics**: Monitor app performance and optimization

## 🌟 Roadmap

### **Upcoming Features**
- [ ] **LinkedIn Integration** - Import profile data directly
- [ ] **Cover Letter Generator** - AI-powered cover letters
- [ ] **Multiple Languages** - Support for international users
- [ ] **Team Collaboration** - Share and collaborate on resumes
- [ ] **Advanced Analytics** - Detailed resume performance metrics
- [ ] **More Templates** - Industry-specific templates
- [ ] **Mobile App** - Native iOS and Android applications

## 📞 Support & Contact

### **Get Help**
- 📺 **Video Tutorials**: [YouTube Channel](https://www.youtube.com/playlist?list=PLrZbkNpNVSwz55T6S0GUK-EWWjnT9OOhs)
- 📧 **Email Support**: [hnk3693@gmail.com](mailto:hnk3693@gmail.com)
- 🐛 **Bug Reports**: [GitHub Issues](https://github.com/HorizonHnk/AI-Resume-Builder/issues)
- 💬 **Feature Requests**: [GitHub Discussions](https://github.com/HorizonHnk/AI-Resume-Builder/discussions)

### **Connect With Us**
- 🌐 **Live Demo**: [rainbow-clafoutis-fa50f5.netlify.app](https://rainbow-clafoutis-fa50f5.netlify.app/)
- 📺 **YouTube**: [Tutorial Playlist](https://www.youtube.com/playlist?list=PLrZbkNpNVSwz55T6S0GUK-EWWjnT9OOhs)
- 💻 **GitHub**: [Repository](https://github.com/HorizonHnk/AI-Resume-Builder.git)

## 📝 License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- 🤖 **Google AI** for providing the Gemini API
- 🔥 **Firebase** for authentication and database services
- ⚡ **Vite** for the amazing build tool
- 🎨 **Tailwind CSS** for the utility-first CSS framework
- 🖼️ **Lucide React** for beautiful icons
- 👥 **Open Source Community** for inspiration and support

---

<div align="center">

### 🌟 **Star this repository if you found it helpful!** 🌟

**Made with ❤️ by [HorizonHnk](https://github.com/HorizonHnk)**

[![GitHub stars](https://img.shields.io/github/stars/HorizonHnk/AI-Resume-Builder?style=social)](https://github.com/HorizonHnk/AI-Resume-Builder/stargazers)
[![GitHub forks](https://img.shields.io/github/forks/HorizonHnk/AI-Resume-Builder?style=social)](https://github.com/HorizonHnk/AI-Resume-Builder/network/members)
[![GitHub watchers](https://img.shields.io/github/watchers/HorizonHnk/AI-Resume-Builder?style=social)](https://github.com/HorizonHnk/AI-Resume-Builder/watchers)

</div>
