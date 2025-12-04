# Recipe Companion

An intelligent recipe recommendation system powered by AI that learns your dietary preferences, respects your restrictions, and helps you achieve your nutritional goals.

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![Streamlit](https://img.shields.io/badge/Streamlit-1.0%2B-red)
![OpenAI](https://img.shields.io/badge/OpenAI-GPT--4o--mini-green)
![License](https://img.shields.io/badge/License-MIT-yellow)

**Created by:** Tony DiRubbo, Saketh Kilaru, Ishaan Lodhi, Luis Riviere

## Overview

Recipe Companion is a sophisticated Streamlit application that combines multiple AI agents to provide personalized recipe recommendations. The system maintains user profiles with dietary preferences, analyzes pantry inventory through image recognition, and suggests recipes aligned with individual health objectives.

### Key Features

- **Multi-Agent Architecture**: Leverages specialized AI agents for different aspects of recipe recommendation
- **Visual Pantry Detection**: Upload photos of your fridge/pantry to automatically detect available ingredients
- **Persistent User Profiles**: Remembers your preferences, restrictions, and dietary goals across sessions
- **Goal-Oriented Suggestions**: Tailors recommendations to support cutting, bulking, or general health objectives
- **Allergy & Restriction Aware**: Filters recipes based on dietary restrictions and allergies
- **Excel-Based Memory**: Stores user data in a structured Excel workbook for easy management
- **Beautiful UI**: Elegant, recipe-book inspired interface with custom styling

## Architecture

### Agent System

The application employs a sophisticated multi-agent system:

```
┌─────────────────────────────────────────────┐
│         Conversational Agent (Main)          │
│         Orchestrates all interactions        │
└────────────────┬────────────────────────────┘
                 │
    ┌────────────┴────────────┬─────────────┬──────────────┐
    │                         │             │              │
┌───▼────────────┐  ┌────────▼─────┐  ┌───▼──────┐  ┌────▼─────┐
│ Memory Agent   │  │ API Agent    │  │Ingredient│  │Objective │
│                │  │              │  │  Agent   │  │  Agent   │
│ Stores user    │  │ Fetches      │  │          │  │          │
│ profiles &     │  │ recipes from │  │ Ranks by │  │ Ranks by │
│ preferences    │  │ database     │  │ ingredient│ │nutritional│
│                │  │              │  │preferences│ │  goals   │
└────────────────┘  └──────────────┘  └──────────┘  └──────────┘
                                              │              │
                                    ┌─────────▼──────────────▼───┐
                                    │   Dietary Restriction      │
                                    │        Agent                │
                                    │                             │
                                    │  Final filter for allergies │
                                    │    and restrictions         │
                                    └─────────────────────────────┘
```

### Components

- **`conversational_agent.py`**: Main orchestrator that coordinates all other agents
- **`memory_agent.py`**: Manages persistent storage of user profiles in Excel
- **`api_agent.py`**: Interfaces with recipe database/API
- **`ingredient_agent.py`**: Uses GPT-4o-mini to rank recipes based on ingredient preferences
- **`objective_agent.py`**: Optimizes recipe selection for nutritional goals
- **`dietary_agent.py`**: Ensures compliance with dietary restrictions and allergies
- **`streamlit_app.py`**: Frontend interface with custom styling
- **`models.py`**: Data models for Recipe and UserProfile

## Getting Started

### Prerequisites

- Python 3.8 or higher
- OpenAI API key
- Excel file support (via openpyxl)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/recipe-companion.git
   cd recipe-companion
   ```

2. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

3. **Set up your OpenAI API key**
   
   Create a `.streamlit/secrets.toml` file:
   ```toml
   OPENAI_API_KEY = "your-api-key-here"
   ```

4. **Run the application**
   ```bash
   streamlit run streamlit_app.py
   ```

## Requirements

```
streamlit
openai
openpyxl
```

## Usage

### Basic Interaction

1. **Set Your Profile**: Enter your name in the sidebar
2. **Upload Pantry Photo** (Optional): Take a photo of your fridge/pantry
3. **Ask for Recipes**: Type natural language requests like:
   - "I want a high-protein dinner"
   - "Show me vegan recipes with chickpeas"
   - "I'm on a cutting diet, what should I eat?"
   - "Clear my inventory"

### Supported Dietary Preferences

- **Restrictions**: Vegan, Vegetarian, Gluten-free, Pescatarian, Lacto-ovo vegetarian
- **Objectives**: Cutting, Bulking, Healthier eating
- **Allergies**: Any food allergen can be specified
- **Preferences**: Likes/dislikes for specific ingredients

### Memory System

The application maintains user profiles with:
- Dietary restrictions and allergies
- Liked and disliked ingredients
- Nutritional objectives
- Pantry inventory
- Conversation history

All data is stored in `MemoryFiles/TestWorkBook.xlsx` for persistence across sessions.

## UI Features

- **Elegant Design**: Warm, kitchen-inspired color palette with custom fonts
- **Responsive Layout**: Optimized for desktop and mobile viewing
- **Recipe Cards**: Beautiful presentation of recipe suggestions with nutritional information
- **Chat Interface**: Natural conversation flow with message history
- **Visual Feedback**: Smooth animations and hover effects

## Project Structure

```
recipe-companion/
├── streamlit_app.py           # Main Streamlit application
├── conversational_agent.py    # Orchestration logic
├── memory_agent.py            # User profile persistence
├── api_agent.py              # Recipe database interface
├── ingredient_agent.py       # Ingredient-based ranking
├── objective_agent.py        # Nutritional goal optimization
├── dietary_agent.py          # Restriction/allergy filtering
├── models.py                 # Data models
├── requirements.txt          # Python dependencies
└── MemoryFiles/             # User profile storage
    └── TestWorkBook.xlsx     # Sample Excel database
```

## Configuration

### Environment Variables

Set in `.streamlit/secrets.toml`:
- `OPENAI_API_KEY`: Your OpenAI API key for GPT-4o-mini access

### Excel Database Schema

The Excel workbook uses three columns:
- `UserName`: Unique user identifier
- `DietRules`: Comma-separated dietary restrictions
- `ConvSummary`: JSON-encoded user preferences and history

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request. For major changes, please open an issue first to discuss what you would like to change.

### Development Guidelines

1. Maintain the multi-agent architecture pattern
2. Ensure all agents are properly integrated with the conversational agent
3. Follow the existing code style and documentation standards
4. Test with various dietary restrictions and preferences
5. Update the Excel schema documentation if modifying the memory system

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgments

- OpenAI for GPT-4o-mini API
- Streamlit for the excellent web framework
- The open-source community for inspiration and support

## Support

For issues, questions, or suggestions, please open an issue on GitHub or contact the maintainers.

---

**Created by Tony DiRubbo, Saketh Kilaru, Ishaan Lodhi, and Luis Riviere**

*Eat well, live better!*
