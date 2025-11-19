# Adaptive Learning Path Workflow with LangGraph

This Jupyter notebook implements an interactive adaptive learning path generator using LangGraph, a framework for building stateful, multi-agent workflows. The system guides users through creating personalized learning roadmaps based on their goals, current skill levels, and preferences, leveraging AI (via OpenRouter/Gemini) for content generation.

## Features

- **Interactive Workflow**: Step-by-step guidance through topic selection, goal setting, skill assessment, and preference gathering.
- **AI-Powered Generation**: Uses Gemini models via OpenRouter to create tailored roadmaps, prerequisites, resources, and schedules.
- **Adaptive Feedback Loop**: Allows users to review and provide feedback on generated roadmaps for refinements.
- **Schedule Building and Export**: Generates study schedules and exports them to .ics files for calendar integration.
- **User-Friendly UI**: Includes an ipywidgets-based interface for easy interaction without command-line prompts.
- **Modular Design**: Built with LangGraph nodes and edges for extensible, state-managed workflows.

## Requirements

- Python 3.8+
- Jupyter Notebook or JupyterLab
- Required Python packages:
  - `langgraph`
  - `openai` (for OpenRouter API)
  - `python-dotenv` (for environment variables)
  - `networkx` and `matplotlib` (for graph visualization)
  - `ipywidgets` (for interactive UI)
  - `icalendar` or similar if needed for ICS export (handled internally)

## Installation

1. Clone or download the repository containing this notebook.

2. Install dependencies:
   ```bash
   pip install langgraph openai python-dotenv networkx matplotlib ipywidgets
   ```

3. Set up environment variables:
   - Create a `.env` file in the same directory as the notebook.
   - Add your OpenRouter API key:
     ```
     GEMINI_API_KEY=your_openrouter_api_key_here
     GEMINI_MODEL=google/gemini-2.0-flash-exp:free  # or your preferred model
     ```

4. Ensure Jupyter supports widgets:
   ```bash
   jupyter nbextension enable --py --sys-prefix widgetsnbextension
   ```

## Usage

1. Open the notebook in Jupyter:
   ```bash
   jupyter notebook learning_path_langgraph.ipynb
   ```

2. Run the cells in order:
   - Cells 1-2: Import libraries and define the state class.
   - Cell 3: Define node functions (workflow steps).
   - Cell 4: Create LangGraph nodes.
   - Cell 5: Define workflow edges.
   - Cell 6: Build and visualize the graph.
   - Cell 7: (Commented out) Run the workflow manually with prompts.
   - Cell 8: Launch the interactive UI.

3. Use the UI:
   - Fill in the topic, goal, level, style, time, weeks, and export preference.
   - Click "Fetch Level Descriptions" to get AI-generated level descriptions.
   - Click "Run Workflow" for the full process or "Quick Roadmap" for a streamlined flow.
   - Provide feedback if needed to regenerate roadmaps.

4. Outputs:
   - Roadmap: AI-generated learning plan.
   - Schedule: Study timeline.
   - Resources: Suggested materials.
   - ICS File: Exported calendar events (if enabled).

## How It Works

- **State Management**: Uses a `RoadmapState` class to track user inputs, AI responses, and workflow progress.
- **Nodes**: Each step (e.g., topic input, roadmap generation) is a node that processes state and calls AI when needed.
- **Edges**: Define the flow between nodes, with conditional branching for feedback.
- **AI Integration**: Calls Gemini via OpenRouter for generating content like roadmaps and schedules.
- **UI**: ipywidgets provide a web-based interface, running the workflow in background threads to avoid blocking.

## Troubleshooting

- **API Errors**: Ensure `GEMINI_API_KEY` is set and valid. Check OpenRouter dashboard for usage.
- **Widget Issues**: If UI doesn't load, ensure `ipywidgets` is installed and Jupyter extensions are enabled.
- **Graph Visualization**: If Mermaid fails, falls back to NetworkX plotting.
- **Input Prompts**: In manual run mode, respond to prompts in the console.

