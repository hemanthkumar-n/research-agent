# Research Agent System 🔬

An intelligent multi-agent system for career research, skill analysis, and personalized career guidance powered by AI.

---

## 📋 Table of Contents

- [Overview](#overview)
- [System Architecture](#system-architecture)
- [Features](#features)
- [Installation](#installation)
- [Configuration](#configuration)
- [Agent Components](#agent-components)
- [Tools & Capabilities](#tools--capabilities)
- [Usage Examples](#usage-examples)
- [API Keys Required](#api-keys-required)
- [Project Structure](#project-structure)
- [Development](#development)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)

---

## 🎯 Overview

The Research Agent System is a comprehensive multi-agent platform designed to help users navigate their career journey through:

- **Resume Analysis**: Extract skills and experience from resumes using AI
- **Role Mapping**: Match skills to optimal career paths using O*NET data
- **Short-Term Skill Analysis**: Identify trending skills from current job market data
- **Long-Term Career Forecasting**: Predict 10-year employment trends and projections
- **Skill Gap Evaluation**: Compare your skills against market requirements
- **Personalized Recommendations**: Get actionable learning paths and career advice

---

## 🏗️ System Architecture

```
research-agent/
├── agents/                    # Specialized AI agents
│   ├── __init__.py
│   ├── base.py               # Base agent with memory
│   ├── coordinator.py        # Team orchestrator
│   ├── resume_extractor.py   # Resume parsing agent
│   ├── role_mapper.py        # Career path matching agent
│   ├── short_term_skills_agent.py  # Job market trend analyzer
│   ├── long_term_forecast_agent.py # Employment projections
│   └── evaluator_recommender.py    # Skill gap analyzer
│
├── tools/                    # Agent capabilities
│   ├── __init__.py
│   ├── resume_tools.py      # PDF/text extraction
│   ├── onet_tools.py        # O*NET API integration
│   ├── adzuna_tools.py      # Job posting retrieval
│   ├── bls_tools.py         # Bureau of Labor Statistics API
│   ├── skill_extraction.py  # NLP skill analysis
│   ├── llm_analysis.py      # Gemini AI integration
│   └── cache_tools.py       # Performance caching
│
├── memory/                   # Persistent storage
│   └── memory_manager.py    # Cross-agent memory
│
├── cache/                    # Cached analysis results
│   └── skills/              # 24-hour skill data cache
│
├── output/                   # Generated reports
│   └── analysis_*.json      # JSON output files
│
├── config/                   # Configuration
│   ├── __init__.py
│   └── settings.py          # Environment settings
│
├── .env.example             # Environment variables template
├── requirements.txt         # Python dependencies
├── main.py                  # Entry point
└── README.md               # This file
```

---

## ✨ Features

### 🎓 Resume Intelligence
- **Multi-format Support**: PDF and text resume parsing
- **AI-Powered Extraction**: Uses Google Gemini for accurate data extraction
- **Skill Detection**: Identifies technical and soft skills automatically
- **Experience Timeline**: Extracts job history with dates and responsibilities

### 🎯 Career Mapping
- **O*NET Integration**: Access to 900+ standardized occupations
- **Skill Matching**: Fuzzy matching algorithm for optimal career fit
- **SOC Code Mapping**: Industry-standard occupation classification
- **Multiple Recommendations**: Get top 5 career matches with confidence scores

### 📊 Market Analysis
- **Real-Time Job Data**: Pulls from Adzuna's 90-day job posting database
- **AI Skill Extraction**: Gemini 2.0 identifies trending technologies
- **Skill Classification**: Categorizes into languages, frameworks, tools, cloud, databases, concepts
- **Frequency Analysis**: Shows demand percentage for each skill
- **Smart Caching**: 24-hour cache for performance optimization

### 🔮 Career Forecasting
- **10-Year Projections**: BLS employment data through 2034
- **Growth Rate Analysis**: Annual job growth percentages
- **Salary Trends**: Average wage projections by occupation
- **Industry Insights**: Sector-specific growth patterns

### 🎯 Personalized Guidance
- **Skill Gap Analysis**: Compare your skills vs. market requirements
- **Priority Recommendations**: Critical vs. nice-to-have skills
- **Learning Pathways**: Actionable steps with timeframes
- **Match Scoring**: Percentage-based skill compatibility

---

## 🚀 Installation

### Prerequisites
- Python 3.10 or higher
- pip package manager
- Virtual environment (recommended)

### Setup

1. **Clone the repository**
```bash
git clone https://github.com/yourusername/research-agent.git
cd research-agent
```

2. **Create virtual environment**
```bash
# Windows
python -m venv venv
venv\Scripts\activate

# macOS/Linux
python3 -m venv venv
source venv/bin/activate
```

3. **Install dependencies**
```bash
pip install -r requirements.txt
```

4. **Configure environment variables**
```bash
# Copy the example file
cp .env.example .env

# Edit .env with your API keys
notepad .env  # Windows
nano .env     # macOS/Linux
```

---

## 🔑 Configuration

### Required API Keys

Create a `.env` file in the project root:

```bash
# Google Gemini AI (Required for resume parsing and skill analysis)
# Get your key: https://makersuite.google.com/app/apikey
GOOGLE_API_KEY=your_gemini_api_key_here
GEMINI_API_KEY=your_gemini_api_key_here  # Alternative name

# Adzuna Job Search API (Required for job market data)
# Register: https://developer.adzuna.com/
ADZUNA_APP_ID=your_adzuna_app_id
ADZUNA_APP_KEY=your_adzuna_app_key

# BLS API (Optional but recommended for better forecasts)
# Register: https://data.bls.gov/registrationEngine/
BLS_API_KEY=your_bls_api_key  # Optional

# O*NET Web Services (Optional, has fallback data)
# Register: https://services.onetcenter.org/
ONET_API_KEY=your_onet_api_key  # Optional
```

### API Limits & Pricing

| Service | Free Tier | Rate Limit | Notes |
|---------|-----------|------------|-------|
| **Gemini AI** | Generous | 60 requests/min | Best for analysis |
| **Adzuna** | 1,000/month | 25/day (v1) | Use caching |
| **BLS API** | 500/day | With key | Free registration |
| **O*NET** | Unlimited | Reasonable use | Fallback built-in |

---

## 🤖 Agent Components

### 1. Resume Extractor Agent
**Purpose**: Extracts structured data from resumes

**Capabilities**:
- PDF and text file parsing
- AI-powered information extraction
- Skill keyword detection
- Experience timeline analysis

**Usage**:
```bash
python -m agents.resume_extractor
```

**Output**:
```json
{
  "name": "John Doe",
  "email": "john@example.com",
  "skills": ["Python", "AWS", "Docker"],
  "experience": [...],
  "education": [...]
}
```

---

### 2. Role Mapper Agent
**Purpose**: Maps skills to optimal career paths

**Capabilities**:
- Fuzzy skill matching
- O*NET occupation database integration
- SOC code assignment
- Confidence scoring

**Usage**:
```bash
python -m agents.role_mapper
```

**Output**:
```json
{
  "top_matches": [
    {
      "title": "Software Developer",
      "soc_code": "15-1252.00",
      "match_score": 0.87,
      "category": "Computer and Mathematical"
    }
  ]
}
```

---

### 3. Short-Term Skills Agent
**Purpose**: Analyzes current job market trends

**Capabilities**:
- Real-time job posting analysis (90 days)
- AI skill extraction (Gemini 2.5)
- Skill classification and ranking
- 24-hour intelligent caching

**Usage**:
```bash
python -m agents.short_term_skills_agent
```

**Output**:
```json
{
  "role": "Data Scientist",
  "top_skills": [
    {
      "name": "Python",
      "type": "language",
      "frequency": 89,
      "mention_count": 107
    }
  ],
  "confidence": 0.92
}
```

---

### 4. Long-Term Forecast Agent
**Purpose**: Provides 10-year employment projections

**Capabilities**:
- BLS employment projections
- Growth rate analysis
- Salary trend forecasting
- Industry sector insights

**Usage**:
```bash
python -m agents.long_term_forecast_agent
```

**Output**:
```json
{
  "soc_code": "15-2051",
  "projections": [
    {
      "year": 2025,
      "employment": 750000,
      "growth_rate": 5.2
    }
  ]
}
```

---

### 5. Evaluator & Recommender Agent
**Purpose**: Analyzes skill gaps and provides guidance

**Capabilities**:
- Skill gap identification
- Priority classification
- Learning pathway recommendations
- Match scoring

**Usage**:
```bash
python -m agents.evaluator_recommender
```

**Output**:
```json
{
  "match_score": 75,
  "critical_gaps": [
    {
      "skill": "AWS",
      "priority": "high",
      "action": "Complete AWS Solutions Architect course",
      "timeframe": "2-3 months"
    }
  ]
}
```

---

## 🛠️ Tools & Capabilities

### Resume Tools (`resume_tools.py`)
- PDF extraction using Gemini
- Text file parsing
- Skill keyword detection
- Data normalization

### O*NET Tools (`onet_tools.py`)
- Occupation search
- Skill requirements lookup
- SOC code validation
- Career family classification

### Adzuna Tools (`adzuna_tools.py`)
- Job posting retrieval
- Multi-region search
- Pagination handling
- Metadata extraction

### BLS Tools (`bls_tools.py`)
- Employment projections API
- Time series data retrieval
- Growth rate calculations
- Salary statistics

### Skill Extraction (`skill_extraction.py`)
- Keyword-based extraction
- NLP skill detection
- Skill categorization
- Frequency analysis

### LLM Analysis (`llm_analysis.py`)
- Gemini 2.5 integration
- Skill gap analysis
- Trend insights
- Recommendation generation

### Cache Tools (`cache_tools.py`)
- 24-hour TTL caching
- JSON storage
- Automatic cleanup
- Cache statistics

---

## 💡 Usage Examples

### Complete Career Analysis Pipeline

```python
# 1. Extract resume
from agents.resume_extractor import create_resume_extractor_agent

resume_agent = create_resume_extractor_agent()
resume_data = resume_agent.run("Extract skills from my_resume.pdf")

# 2. Map to roles
from agents.role_mapper import create_role_mapper_agent

mapper = create_role_mapper_agent()
roles = mapper.run(f"Map these skills: {resume_data['skills']}")

# 3. Analyze market trends
from agents.short_term_skills_agent import create_short_term_skills_agent

skills_agent = create_short_term_skills_agent()
market_data = skills_agent.run(f"Analyze skills for {roles['top_matches'][0]['title']}")

# 4. Get long-term forecast
from agents.long_term_forecast_agent import create_long_term_forecast_agent

forecast_agent = create_long_term_forecast_agent()
projections = forecast_agent.run(f"Forecast for {roles['top_matches'][0]['soc_code']}")

# 5. Evaluate and recommend
from agents.evaluator_recommender import create_evaluator_recommender_agent

evaluator = create_evaluator_recommender_agent()
recommendations = evaluator.run({
    "user_skills": resume_data['skills'],
    "required_skills": market_data['top_skills'],
    "job_title": roles['top_matches'][0]['title']
})
```

### Individual Agent Usage

```python
# Just analyze job market for a specific role
from main import analyze_role_skills

result = analyze_role_skills(
    job_title="Machine Learning Engineer",
    use_cache=True,
    use_gemini=True
)

print(f"Top Skills: {result['top_skills'][:5]}")
```

---

## 🧪 Development

### Running Tests

```bash
# Run all tests
pytest

# Run specific test file
pytest tests/test_resume_tools.py

# Run with coverage
pytest --cov=agents --cov=tools
```

### Code Quality

```bash
# Format code
black agents/ tools/

# Lint
flake8 agents/ tools/

# Type checking
mypy agents/ tools/
```

### Adding New Agents

1. Create agent file in `agents/`
2. Inherit from `BaseAgent`
3. Define tools and instructions
4. Add to coordinator if needed

```python
from agents.base import BaseAgent

def create_my_agent() -> BaseAgent:
    instructions = """Your agent instructions..."""
    tools = [tool1, tool2]
    
    return BaseAgent(
        name="My Agent",
        role="Description",
        context="context_key",
        instructions=instructions,
        tools=tools,
        add_memory=True
    )
```

---

## 🔧 Troubleshooting

### Common Issues

**Issue**: `ModuleNotFoundError: No module named 'agents'`
```bash
# Solution: Add project root to Python path
export PYTHONPATH="${PYTHONPATH}:$(pwd)"
# Or run as module
python -m agents.agent_name
```

**Issue**: API key errors
```bash
# Verify .env file exists and has correct keys
cat .env | grep API_KEY

# Reload environment
source .env  # Linux/Mac
# Or restart your terminal
```

**Issue**: Gemini model not found
```python
# Use the correct model name
model = genai.GenerativeModel('gemini-2.0-flash-exp')
# NOT: 'gemini-1.5-pro' or 'models/gemini-1.5-pro'
```

**Issue**: Cache not clearing
```bash
# Manually clear cache
python -c "from tools.cache_tools import clear_cache; clear_cache()"
```

---

## 📊 Performance Tips

1. **Enable Caching**: Use `use_cache=True` for repeated queries
2. **Batch Requests**: Analyze multiple roles together when possible
3. **Use API Keys**: Register for BLS and O*NET keys for better limits
4. **Optimize Prompts**: Shorter prompts = faster Gemini responses
5. **Monitor Quotas**: Track API usage to avoid rate limits

---

## 🤝 Contributing

We welcome contributions! Here's how:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit changes (`git commit -m 'Add amazing feature'`)
4. Push to branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Contribution Guidelines

- Follow PEP 8 style guide
- Add docstrings to all functions
- Include unit tests for new features
- Update README with new capabilities
- Keep commits atomic and well-described

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgments

- **O*NET**: Occupational data from the U.S. Department of Labor
- **BLS**: Employment projections from Bureau of Labor Statistics
- **Adzuna**: Job posting data
- **Google**: Gemini AI for intelligent analysis
- **Contributors**: All developers who helped build this system

---

## 📞 Support

- **Issues**: [GitHub Issues](https://github.com/yourusername/research-agent/issues)
- **Discussions**: [GitHub Discussions](https://github.com/yourusername/research-agent/discussions)
- **Email**: support@yourproject.com

---

## 🗺️ Roadmap

- [ ] Add LinkedIn profile integration
- [ ] Implement course recommendation engine
- [ ] Create web dashboard UI
- [ ] Add resume builder tool
- [ ] Integrate salary negotiation assistant
- [ ] Multi-language support
- [ ] Real-time job alerts
- [ ] Portfolio analysis features

---
