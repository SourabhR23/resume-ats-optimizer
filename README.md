# 🧠 Resume ATS Agent (CrewAI + OpenAI)

An intelligent multi-agent resume optimization system that transforms your resume into an ATS-friendly document perfectly tailored to target job descriptions. Powered by CrewAI and OpenAI's GPT-4o-mini.

## 📋 Overview

This project uses **CrewAI's multi-agent framework** to orchestrate a workflow of specialized AI agents that:

1. **Parse** your resume and clean the text
2. **Rewrite** your resume with ATS-optimized keywords and formatting
3. **Refine** bullet points with powerful action verbs and metrics
4. **Evaluate** your resume with an ATS score (0-100) and actionable recommendations

Perfect for job seekers who want to maximize their chances of passing Applicant Tracking Systems!

## ✨ Features

- 🤖 **Multi-Agent Architecture**: 4 specialized CrewAI agents working in sequential workflow
- 📄 **Multi-Format Support**: Upload resumes in PDF, DOCX, or TXT format
- 🎯 **Job-Specific Optimization**: Tailor your resume to specific job descriptions
- 📊 **ATS Scoring**: Get realistic ATS scores (0-100) with keyword analysis
- 💡 **Actionable Recommendations**: Quick wins and missing keywords suggestions
- 🌐 **Interactive Web UI**: Built with Streamlit for easy use
- 📥 **Multiple Outputs**: Download cleaned, optimized, and final versions in TXT or DOCX

## 🖼️ Demo

### Application Interface

![ATS Resume Agent - Main Interface](file_tools\demo.png)

### Agents Specification

#### 🔍 **Agent 1: Parser Agent**
**Role:** Resume Parsing Specialist  
**Purpose:** Extract and clean resume text from various file formats  
**Input:** Raw resume file (PDF/DOCX/TXT)  
**Output:** Clean, normalized resume text  
**Configuration:**
- Model: `gpt-4o-mini`
- Temperature: 0.0 (deterministic)
- Max Iterations: 1
- Max Execution Time: 120 seconds

**Responsibilities:**
- Removes PDF/DOCX encoding artifacts and noise
- Normalizes bullet points to consistent format (-)
- Cleans up extra whitespace and formatting
- Preserves all important content and structure
- Handles multi-page resumes efficiently

**Example Transformation:**
```
Input (Raw):  "Worked as a developer  at company. Made websites"
Output:       "- Worked as a developer at company
               - Made websites"
```

---

#### ✍️ **Agent 2: ATS Writer Agent**
**Role:** ATS Optimization Writer  
**Purpose:** Rewrite resume for ATS system compatibility and job requirements  
**Input:** 
- Cleaned resume text
- Target job title
- Job description (Requirements)

**Output:** ATS-optimized resume with strategic keyword placement  
**Configuration:**
- Model: `gpt-4o-mini`
- Temperature: 0.3 (creative but consistent)
- Max Iterations: 1
- Max Execution Time: 120 seconds

**Responsibilities:**
- Analyzes job description for critical keywords
- Extracts must-have skills and requirements
- Strategically places keywords throughout resume
- Rewrites weak bullets into powerful statements
- Adds quantifiable metrics and achievements
- Uses strong action verbs (Engineered, Architected, Optimized, etc.)
- Ensures ATS keyword scanning compatibility
- Target: 80+ ATS score

**Optimization Techniques:**
| Technique | Example Before | Example After |
|-----------|---|---|
| Action Verbs | "Worked on projects" | "Architected scalable solutions" |
| Quantification | "Improved performance" | "Reduced query time by 60%" |
| Keywords | Generic skills | Job-specific technologies |
| Metrics | Vague achievements | "Increased revenue by $500K" |

---

#### ✨ **Agent 3: Refiner Agent**
**Role:** Bullet Point Refiner  
**Purpose:** Enhance bullet points with maximum impact using power language  
**Input:** ATS-optimized resume  
**Output:** Resume with polished, high-impact bullet points  
**Configuration:**
- Model: `gpt-4o-mini`
- Temperature: 0.2 (consistency with slight creativity)
- Max Iterations: 1
- Max Execution Time: 120 seconds

**Responsibilities:**
- Identifies weak or vague bullet points
- Strengthens action verbs for greater impact
- Adds missing metrics and business outcomes
- Ensures consistent formatting and style
- Improves readability and flow
- Optimizes bullet length (ideally 1-2 lines)
- Aligns bullets with job requirements

**Enhancement Examples:**
```
❌ WEAK:      "Worked on team projects"
✅ STRONG:    "Led cross-functional team of 5 engineers on $2M project, 
               delivering 2 weeks ahead of schedule"

❌ WEAK:      "Improved system"
✅ STRONG:    "Optimized database queries from 2.5s to 300ms using indexing, 
               improving user experience for 100K+ daily users"

❌ WEAK:      "Good communication skills"
✅ STRONG:    "Mentored 3 junior developers, resulting in 2 promotions 
               and improved team retention by 40%"
```

---

#### 📊 **Agent 4: Evaluator Agent**
**Role:** ATS Evaluator  
**Purpose:** Score resume and provide actionable improvement recommendations  
**Input:**
- Final refined resume
- Target job title
- Job description

**Output:** JSON evaluation with ATS score (0-100) and detailed breakdown  
**Configuration:**
- Model: `gpt-4o-mini`
- Temperature: 0.0 (deterministic scoring)
- Max Iterations: 1
- Max Execution Time: 120 seconds

**Responsibilities:**
- Scans for keyword matches with job description
- Evaluates resume structure and formatting
- Analyzes action verb diversity and strength
- Checks for quantifiable metrics
- Assesses format compatibility with ATS systems
- Identifies missing critical keywords
- Suggests quick wins for score improvement

**Scoring Breakdown (0-100):**
| Category | Criteria | Weight |
|----------|----------|--------|
| **Keyword Match** | Presence of job-specific keywords | 25% |
| **Structure** | Proper formatting, sections, readability | 20% |
| **Action Verbs** | Use of strong, varied power verbs | 20% |
| **Metrics** | Quantifiable achievements and results | 20% |
| **Format** | ATS-compatible formatting, no fancy fonts | 15% |

**Evaluation Output Example:**
```json
{
  "overall_score": 82,
  "breakdown": {
    "keyword_match": 85,
    "structure": 80,
    "action_verbs": 85,
    "metrics_quantification": 78,
    "format_compatibility": 82
  },
  "missing_keywords": [
    "Cloud Architecture",
    "Kubernetes",
    "Microservices",
    "CI/CD"
  ],
  "quick_wins": [
    "Add cloud platform experience (AWS/GCP/Azure)",
    "Mention containerization (Docker/Kubernetes)",
    "Quantify team leadership experience",
    "Add more metrics to achievements"
  ]
}
```

## 📦 Project Structure

```
Resume_ATS_Agent/
├── __init__.py              # Package initialization
├── agents.py                # CrewAI agent definitions (4 agents)
├── crew.py                  # Crew orchestration and pipeline
├── tasks.py                 # Task definitions for each agent
├── streamlit_app.py         # Web UI application
├── utils.py                 # Utility functions (TXT to DOCX conversion)
├── requirements.txt         # Python dependencies
├── README.md               # Project documentation
├── docs/
│   ├── IMAGES.md           # Image guide & specifications
│   └── images/             # Image directory (add demo images here)
│       ├── app-demo.png
│       ├── agent-workflow.png
│       ├── output-tabs.png
│       └── ats-score.png
├── file_tools/
│   ├── __init__.py
│   └── file_loader.py      # File parsing (PDF, DOCX, TXT support)
└── ...
```

### Information Flow

```
┌─────────────────────────────────────────────────────────────┐
│                    STREAMLIT INTERFACE                      │
│  • File Upload (PDF/DOCX/TXT)                              │
│  • Job Title Input                                          │
│  • Job Description Input                                    │
└────────────────────┬────────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────────┐
│              FILE LOADER (file_tools/)                       │
│  • Detect file format                                       │
│  • Extract text from PDF/DOCX                              │
│  • Handle encoding issues                                   │
└────────────────────┬────────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────────┐
│         CREW ORCHESTRATION (crew.py)                        │
│  • Initialize 4 agents                                      │
│  • Create sequential tasks                                  │
│  • Execute pipeline with CrewAI                            │
└────────────────────┬────────────────────────────────────────┘
                     │
        ┌────────────┼────────────┬────────────┐              
        │            │            │            │              
        ▼            ▼            ▼            ▼              
    ┌────────┐  ┌────────┐  ┌────────┐  ┌────────┐           
    │Parser  │→ │Writer  │→ │Refiner │→ │Evaluator
    │Agent   │  │Agent   │  │Agent   │  │Agent   │
    └────────┘  └────────┘  └────────┘  └────────┘           
        │            │            │            │              
        └────────────┼────────────┼────────────┘              
                     │                                        
                     ▼                                        
        ┌────────────────────────────┐                       
        │  OpenAI API Calls (GPT-4o) │                       
        │  • Parallel calls          │                       
        │  • Token optimization      │                       
        └────────────────────────────┘                       
                     │                                        
        ┌────────────┼────────────┬────────────┐              
        │            │            │            │              
        ▼            ▼            ▼            ▼              
    ┌────────┐  ┌────────┐  ┌────────┐  ┌────────┐           
    │Cleaned │  │Optimized│  │Refined │  │Evaluation
    │Resume  │  │Resume   │  │Resume  │  │Score    │
    └────────┘  └────────┘  └────────┘  └────────┘
        │            │            │            │              
        └────────────┼────────────┼────────────┘              
                     │                                        
                     ▼                                        
        ┌────────────────────────────┐                       
        │  Utils (convertDOCX)       │                       
        │  Generate multiple formats │                       
        └────────────────────────────┘                       
                     │                                        
                     ▼                                        
        ┌────────────────────────────┐                       
        │  STREAMLIT OUTPUT TABS     │                       
        │  1. Cleaned Resume (TXT)   │                       
        │  2. Optimized Resume (TXT) │                       
        │  3. Refined Resume (TXT/DOCX) │                    
        │  4. ATS Evaluation (JSON)  │                       
        └────────────────────────────┘                       
```

## 🚀 Getting Started

### Prerequisites

- Python 3.9+
- OpenAI API key
- pip (Python package manager)

### Installation

1. **Clone or download the project**
```bash
cd Resume_ATS_Agent
```

2. **Create a virtual environment (optional but recommended)**
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. **Install dependencies**
```bash
pip install -r requirements.txt
```

4. **Set your OpenAI API key**

The project expects your OpenAI API key to be set. You can do this by:
- Setting the environment variable: `OPENAI_API_KEY`
- Or updating it directly in `agents.py` (already configured)

### Usage

#### Option 1: Web UI (Recommended)

```bash
streamlit run streamlit_app.py
```

Then:
1. Open your browser to `http://localhost:8501`
2. Upload your resume (PDF, DOCX, or TXT)
3. Enter your target job title
4. Paste the job description
5. Click "Run ATS Agent"
6. Review results in the tabs and download outputs

#### Option 2: Programmatic Usage

```python
from crew import run_pipeline

# Prepare inputs
raw_resume = "Your resume text here..."
job_title = "Senior Software Engineer"
job_description = "Your job description here..."

# Run the pipeline
cleaned, rewritten, final_resume, evaluation = run_pipeline(
    raw_resume_text=raw_resume,
    job_title=job_title,
    job_description=job_description
)

print("Cleaned Resume:", cleaned)
print("Rewritten Resume:", rewritten)
print("Final Resume:", final_resume)
print("Evaluation:", evaluation)
```

## 📊 Output Tabs

### 1. Cleaned Resume
- Original resume with artifacts removed
- Normalized formatting and bullet points
- Raw text output

### 2. Rewritten (ATS-optimized)
- Keywords strategically placed
- Action verbs enhanced
- Metrics added where possible
- ATS-optimized structure

### 3. Final (Refined Bullets)
- Polished bullet points with strong action verbs
- Quantified achievements
- Download as TXT or DOCX

### 4. ATS Evaluation
- **Overall ATS Score** (0-100)
- **Scoring Breakdown**:
  - Keyword matching
  - Section structure
  - Action verb usage
  - Metrics quantification
  - Format compatibility
- **Missing Keywords**: Keywords from job description not in resume
- **Quick Wins**: Easy improvements to boost your score

## ⚙️ Dependencies

```
crewai>=0.80.0                 # Multi-agent orchestration
crewai-tools>=0.12.0           # CrewAI tools
python-dotenv>=1.0.1           # Environment variable management
requests>=2.31.0               # HTTP client
pypdf>=4.2.0                   # PDF parsing
python-docx>=1.1.2             # DOCX file handling
streamlit>=1.36.0              # Web UI framework
pydantic>=2.8.2                # Data validation
openai                         # OpenAI API (via crewai)
```

## 🔑 Key Technologies

- **CrewAI**: Multi-agent framework for orchestrating AI workflows
- **OpenAI GPT-4o-mini**: Fast, capable language model for resume optimization
- **Streamlit**: Easy-to-build interactive web applications
- **Python-docx**: Creating and editing DOCX files programmatically
- **PyPDF**: Parsing PDF documents

## ⚠️ Security Notes

- Your OpenAI API key is embedded in `agents.py`. For production use:
  - Move it to a `.env` file
  - Use environment variable loading
  - Never commit API keys to version control
  - Use `.gitignore` to exclude sensitive files

## 🛠️ Troubleshooting

### "Could not extract any text from the file"
- Ensure your resume file is readable
- Try converting it to a different format (PDF → DOCX, etc.)
- Check that the file isn't corrupted or scannedimage

### "OpenAI API key not working"
- Verify your API key is valid
- Check your OpenAI account credits
- Ensure the key has API access enabled

### Streamlit connection errors
- Check that Streamlit is properly installed
- Try running with `streamlit run streamlit_app.py --logger.level=debug`

## 📝 Example Workflow

1. **Input Resume**: "Senior Developer with 5 years experience..."
2. **Job Title**: "Machine Learning Engineer"
3. **Job Description**: "Looking for experience in Python, TensorFlow, AWS..."
4. **Output**:
   - Parsed resume: Clean, normalized text
   - ATS Resume: Added ML keywords, quantified metrics
   - Refined: Enhanced bullets like "Developed ML pipeline using TensorFlow, reducing inference time by 40%"
   - Score: 82/100 - Excellent match!

## 🤝 Contributing

Feel free to fork, modify, and improve this project for your needs!

---

**Made with ❤️ using CrewAI and OpenAI**
