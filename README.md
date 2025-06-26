# 🚀 AI Resume Builder

> **Transform your job search with intelligent, ATS-optimized resume creation powered by Claude AI**

[![React](https://img.shields.io/badge/React-18.0+-blue.svg)](https://reactjs.org/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-3.0+-38B2AC.svg)](https://tailwindcss.com/)
[![Claude API](https://img.shields.io/badge/Claude_API-Integrated-orange.svg)](https://www.anthropic.com/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![YouTube](https://img.shields.io/badge/YouTube-Tutorial-red.svg)](https://www.youtube.com/playlist?list=PLrZbkNpNVSwz55T6S0GUK-EWWjnT9OOhs)

## 📋 Table of Contents

- [✨ Features](#-features)
- [🛠️ Tech Stack](#️-tech-stack)
- [🚀 Quick Start](#-quick-start)
- [📱 Responsive Design](#-responsive-design)
- [🤖 AI Integration](#-ai-integration)
- [📸 Screenshots](#-screenshots)
- [🎯 Usage Guide](#-usage-guide)
- [🔧 Configuration](#-configuration)
- [🧪 Testing](#-testing)
- [🤝 Contributing](#-contributing)
- [📺 Video Tutorials](#-video-tutorials)
- [📄 License](#-license)
- [👨‍💻 Author](#-author)

## ✨ Features

### 🎯 **Core Functionality**
- **AI-Powered Content Generation** - Claude API integration for intelligent resume content
- **ATS Optimization Analysis** - Real-time scoring and keyword analysis
- **Multiple Professional Templates** - Modern, Creative, and Executive designs
- **Live Preview** - See changes instantly as you type
- **PDF Export** - Professional-quality PDF generation
- **Responsive Design** - Works seamlessly on all devices

### 🧠 **Smart AI Features**
- **Job Description Processing** - Intelligent analysis of job requirements
- **Keyword Optimization** - Automatic keyword matching and suggestions
- **Content Enhancement** - AI-powered experience and project descriptions
- **Skills Recommendation** - Role-specific skill suggestions
- **ATS Compatibility Scoring** - Detailed feedback on resume optimization

### 📋 **Resume Sections**
- **Personal Information** - Contact details with validation
- **Professional Summary** - AI-generated summaries
- **Work Experience** - Dynamic experience entries with AI enhancement
- **Projects** - Showcase your technical projects
- **Education** - Academic background
- **Certifications** - Professional credentials
- **Skills** - Technical and soft skills with bulk addition

### 🎨 **User Experience**
- **Form Validation** - Real-time validation with helpful error messages
- **Mobile-First Design** - Optimized for all screen sizes
- **Intuitive Interface** - Clean, professional UI/UX
- **Data Persistence** - Work sessions maintained during use

## 🛠️ Tech Stack

### **Frontend**
- **React 18+** - Modern React with hooks
- **Tailwind CSS** - Utility-first CSS framework
- **Lucide React** - Beautiful, customizable icons
- **Responsive Design** - Mobile-first approach

### **AI Integration**
- **Claude API** - Advanced language model by Anthropic
- **Intelligent Prompting** - Optimized prompt engineering
- **JSON Response Handling** - Structured AI responses

### **Development Tools**
- **Create React App** - Development environment
- **ESLint** - Code linting
- **Prettier** - Code formatting

## 🚀 Quick Start

### Prerequisites

Before you begin, ensure you have the following installed:
- **Node.js** (v14.0.0 or later)
- **npm** or **yarn**
- **Claude API access** (for AI features)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/HorizonHnk/ai-resume-builder.git
   cd ai-resume-builder
   ```

2. **Install dependencies**
   ```bash
   npm install
   # or
   yarn install
   ```

3. **Set up environment variables**
   ```bash
   cp .env.example .env.local
   ```
   
   Add your API keys to `.env.local`:
   ```env
   REACT_APP_CLAUDE_API_KEY=your_claude_api_key_here
   ```

4. **Start the development server**
   ```bash
   npm start
   # or
   yarn start
   ```

5. **Open your browser**
   
   Navigate to `http://localhost:3000` to see the application.

### Build for Production

```bash
npm run build
# or
yarn build
```

## 📱 Responsive Design

The application is fully responsive and optimized for:

| Device Type | Screen Size | Features |
|-------------|-------------|----------|
| **📱 Mobile** | < 640px | Collapsible sidebar, touch-friendly interface |
| **📱 Small** | 640px - 768px | Optimized layouts, improved navigation |
| **💻 Tablet** | 768px - 1024px | Balanced design, dual-column layouts |
| **🖥️ Desktop** | 1024px - 1280px | Side-by-side editor and preview |
| **🖥️ Large** | > 1280px | Full professional experience |

## 🤖 AI Integration

### Claude API Integration

```javascript
// Example AI content generation
const generateAIContent = async (section, context) => {
  const response = await window.claude.complete(prompt);
  return processResponse(response);
};
```

### Smart Features

- **🎯 Job Analysis** - Extracts key requirements, skills, and keywords
- **📝 Content Generation** - Creates tailored resume content
- **🔍 ATS Optimization** - Analyzes and scores resume compatibility
- **💡 Intelligent Suggestions** - Provides actionable improvement recommendations

## 📸 Screenshots

### 🖥️ Desktop Experience
```
┌─────────────────────────────────────────────────────────────┐
│  🎯 AI Resume Builder                    [Templates] [PDF]  │
├─────────────────┬───────────────────────────────────────────┤
│  📝 Editor      │  👁️ Live Preview                          │
│                 │                                           │
│  Job Analysis   │  ┌─────────────────────────────────────┐  │
│  ATS Score      │  │  John Doe                           │  │
│  Personal Info  │  │  john@email.com | (555) 123-4567   │  │
│  Experience     │  │                                     │  │
│  Projects       │  │  Professional Summary               │  │
│  Education      │  │  Experienced developer with...      │  │
│  Certifications │  └─────────────────────────────────────┘  │
│  Skills         │                                           │
└─────────────────┴───────────────────────────────────────────┘
```

### 📱 Mobile Experience
```
┌─────────────────────┐
│ ☰ AI Resume Builder │
│                     │
│ [Process Job Desc.] │
│ [Analyze ATS Score] │
│                     │
│ 📋 Job Analysis     │
│ Score: 85% ✅       │
│                     │
│ [Personal][Exp][+]  │
│                     │
│ Name: John Doe      │
│ Email: john@...     │
│                     │
│ [View Resume] 👁️    │
└─────────────────────┘
```

## 🎯 Usage Guide

### 1. **Job Description Analysis**
```markdown
1. Paste your target job description
2. Click "Process Job Description"
3. Review the extracted requirements and keywords
4. Use insights to optimize your resume content
```

### 2. **Resume Building Process**
```markdown
1. Fill in Personal Information (name, email required)
2. Add Professional Summary (use AI suggestions)
3. Add Work Experience (AI can enhance descriptions)
4. Include Projects and Certifications
5. Add Skills (bulk addition supported)
6. Review Live Preview
```

### 3. **ATS Optimization**
```markdown
1. Complete your resume sections
2. Click "Analyze ATS Score"
3. Review compatibility score and feedback
4. Implement suggested improvements
5. Re-analyze for better scores
```

### 4. **Export and Use**
```markdown
1. Review final resume in Live Preview
2. Switch templates if desired
3. Click "Export PDF" for professional output
4. Use the PDF for job applications
```

## 🔧 Configuration

### Environment Variables

Create a `.env.local` file in the root directory:

```env
# Claude API Configuration
REACT_APP_CLAUDE_API_KEY=your_api_key_here
REACT_APP_API_BASE_URL=https://api.anthropic.com

# Application Settings
REACT_APP_VERSION=1.0.0
REACT_APP_ENVIRONMENT=development
```

### Customization Options

#### Adding New Templates
```javascript
// src/templates/newTemplate.js
export const customTemplate = {
  name: 'Custom Design',
  colors: 'bg-gradient-to-br from-custom-50 to-custom-100',
  headerBg: 'bg-custom-600',
  textColor: 'text-gray-800'
};
```

#### Extending AI Prompts
```javascript
// src/utils/aiPrompts.js
export const customPrompts = {
  summary: (context, jobAnalysis) => `
    Your custom prompt here...
    Context: ${context}
    Job Analysis: ${JSON.stringify(jobAnalysis)}
  `
};
```

## 🧪 Testing

### Running Tests
```bash
npm test
# or
yarn test
```

### Test Coverage
```bash
npm run test:coverage
# or
yarn test:coverage
```

### Manual Testing Checklist

- [ ] **Responsive Design** - Test on different screen sizes
- [ ] **AI Features** - Verify content generation works
- [ ] **Form Validation** - Check error handling
- [ ] **PDF Export** - Ensure proper formatting
- [ ] **ATS Analysis** - Verify scoring accuracy
- [ ] **Data Persistence** - Test session management

## 🤝 Contributing

We welcome contributions! Here's how you can help:

### Getting Started
1. **Fork the repository**
2. **Create your feature branch**
   ```bash
   git checkout -b feature/AmazingFeature
   ```
3. **Commit your changes**
   ```bash
   git commit -m 'Add some AmazingFeature'
   ```
4. **Push to the branch**
   ```bash
   git push origin feature/AmazingFeature
   ```
5. **Open a Pull Request**

### Contribution Guidelines

#### 🐛 Bug Reports
- Use the bug report template
- Include steps to reproduce
- Provide screenshots if applicable
- Test on multiple devices/browsers

#### ✨ Feature Requests
- Use the feature request template
- Explain the problem and proposed solution
- Consider backward compatibility
- Provide mockups or examples

#### 📝 Code Style
- Follow existing code conventions
- Use meaningful variable names
- Add comments for complex logic
- Update documentation as needed

### Areas for Contribution

- 🎨 **New Templates** - Additional professional designs
- 🌐 **Internationalization** - Multi-language support
- 🔌 **API Integrations** - LinkedIn, Indeed, etc.
- 📊 **Analytics** - Usage tracking and insights
- 🧪 **Testing** - Unit and integration tests
- 📚 **Documentation** - Improved guides and tutorials

## 📺 Video Tutorials

Check out our comprehensive video tutorials:

[![YouTube Tutorial Series](https://img.shields.io/badge/YouTube-Watch_Tutorials-red.svg?style=for-the-badge&logo=youtube)](https://www.youtube.com/playlist?list=PLrZbkNpNVSwz55T6S0GUK-EWWjnT9OOhs)

### Tutorial Series Content:
1. **🚀 Getting Started** - Project setup and overview
2. **🎨 UI/UX Design** - Building the interface
3. **🤖 AI Integration** - Claude API implementation
4. **📱 Responsive Design** - Mobile-first development
5. **🎯 ATS Optimization** - Algorithm implementation
6. **📄 PDF Generation** - Export functionality
7. **🚀 Deployment** - Production deployment guide

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

```
MIT License

Copyright (c) 2024 HorizonHnk

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

## 👨‍💻 Author

**HorizonHnk**

- 📧 **Email:** [hhnk3693@gmail.com](mailto:hhnk3693@gmail.com)
- 🐙 **GitHub:** [@HorizonHnk](https://github.com/HorizonHnk)
- 📺 **YouTube:** [Tutorial Playlist](https://www.youtube.com/playlist?list=PLrZbkNpNVSwz55T6S0GUK-EWWjnT9OOhs)
- 💼 **LinkedIn:** [Connect with me](https://linkedin.com/in/horizonhnk)

---

### 🌟 Show Your Support

If this project helped you, please consider:

- ⭐ **Starring this repository**
- 🐛 **Reporting bugs**
- 💡 **Suggesting new features**
- 🤝 **Contributing to the codebase**
- 📺 **Subscribing to our YouTube channel**
- 📢 **Sharing with others**

---

### 🚀 What's Next?

**Upcoming Features:**
- 🌐 Multi-language support
- 🔗 LinkedIn integration
- 📊 Analytics dashboard
- 🎨 More professional templates
- 🤖 Advanced AI features
- 📱 Mobile app version

---

**Made with ❤️ by [HorizonHnk](https://github.com/HorizonHnk)**

> *"Empowering careers through intelligent technology"*
