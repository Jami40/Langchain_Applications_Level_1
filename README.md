# Level 1 Applications

> A growing collection of practical Python, AI, and automation applications.

[![Python](https://img.shields.io/badge/Python-3.11%2B-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebooks-F37626?logo=jupyter&logoColor=white)](https://jupyter.org/)
[![LangChain](https://img.shields.io/badge/LangChain-Applications-1C3C3C?logo=chainlink&logoColor=white)](https://www.langchain.com/)
[![VS Code](https://img.shields.io/badge/Developed%20with-VS%20Code-007ACC?logo=visualstudiocode&logoColor=white)](https://code.visualstudio.com/)

## Overview

`Level_1_Applications` is the workspace for building and organizing multiple small applications and experiments. Each application is kept in its own folder so it can evolve independently while sharing a clear workspace structure and common development practices.

The current projects focus on:

- 🤖 Conversational AI and chatbot applications
- 🧾 Structured data extraction from unstructured text
- 🧪 Small, focused experiments that can become standalone applications

## Applications

| Application | Description | Entry point |
|---|---|---|
| 🤖 **ChatBot** | Simple and advanced LangChain chatbots with conversation and session memory | [`ChatBot/`](./ChatBot/) |
| 🧾 **Data Extraction** | Extract structured information from unstructured text | [`Data_Extraction/Key_Data_Extraction.ipynb`](./Data_Extraction/Key_Data_Extraction.ipynb) |

### ChatBot

The `ChatBot` folder currently contains:

- [`Simple_Chatbot.ipynb`](./ChatBot/Simple_Chatbot.ipynb) — a chatbot with stored conversation memory
- [`Advanced-Chatbot.ipynb`](./ChatBot/Advanced-Chatbot.ipynb) — a chatbot with session-based and limited memory
- [`messages.json`](./ChatBot/messages.json) — local conversation data used by the applications

## Workspace structure

```text
Level_1_Applications/
├── ChatBot/
│   ├── Advanced-Chatbot.ipynb
│   ├── Simple_Chatbot.ipynb
│   └── messages.json
├── Data_Extraction/
│   └── Key_Data_Extraction.ipynb
├── .env                  # Local secrets; never commit
├── .gitignore
├── requirements.txt      # Shared starting dependencies
└── README.md
```

> Add each new application in a dedicated, clearly named folder. Give it a focused README when its setup or usage differs from the workspace defaults.

## Development setup

### 1. Open the workspace

Open this folder in VS Code:

```text
E:\Level_1_Applications
```

### 2. Activate the Python environment

The current notebooks use the Conda environment `llmapp`:

```powershell
conda activate llmapp
```

The project folder and the environment can be in different locations. The project is stored at `E:\Level_1_Applications`; Conda may store `llmapp` under the Anaconda installation directory.

### 3. Install dependencies

Run these commands from the workspace root:

```powershell
Set-Location -Path E:\Level_1_Applications
conda activate llmapp
python -m pip install -r requirements.txt
python -m pip install ipykernel
```

Using `python -m pip` ensures packages are installed into the currently active Python environment.

### 4. Select the VS Code interpreter and notebook kernel

Select the same environment in both places:

1. **Command Palette** → **Python: Select Interpreter** → `llmapp (Python 3.11)`
2. Open a notebook → click the kernel selector at the top-right → choose `llmapp (Python 3.11)`

Verify the active interpreter before troubleshooting package errors:

```powershell
where.exe python
python -c "import sys; print(sys.executable); print(sys.version)"
```

The executable should point to the `llmapp` environment, for example:

```text
D:\Anaconda\envs\llmapp\python.exe
```

## Environment variables and secrets

Create a local `.env` file in the workspace root:

```text
E:\Level_1_Applications\.env
```

For Groq-powered applications, add:

```env
GROQ_API_KEY=your_groq_api_key_here
```

Load environment variables in Python:

```python
from dotenv import load_dotenv

load_dotenv()
```

Never commit API keys, passwords, tokens, or other secrets. The workspace `.gitignore` already excludes `.env`.

## Running a notebook

1. Activate `llmapp`.
2. Open the required `.ipynb` file in VS Code.
3. Confirm that the notebook kernel is `llmapp (Python 3.11)`.
4. Restart the kernel after installing or upgrading a package.
5. Run cells from top to bottom.

For the Groq chatbot, the model initialization is:

```python
from langchain_groq import ChatGroq

chatbot = ChatGroq(model="openai/gpt-oss-120b")
```

## Dependency management

The root [`requirements.txt`](./requirements.txt) currently contains the shared LangChain chatbot dependencies. When a new application needs additional packages:

1. Add only the required package and a compatible version.
2. Document application-specific setup in that application's folder.
3. Reinstall with `python -m pip install -r requirements.txt`.
4. Restart the notebook kernel.

As the workspace grows, applications with substantially different dependencies should use their own `requirements.txt` or environment rather than creating conflicts in the shared environment.

## Adding a new application

Use this workflow:

```text
1. Create a descriptive folder: New_Application/
2. Add the source code or notebook.
3. Add a local README.md if setup or usage is application-specific.
4. Add or update dependency documentation.
5. Keep secrets in the root .env file or an application-local ignored file.
6. Update the Applications table in this README.
```

Recommended application layout:

```text
New_Application/
├── README.md
├── src/                 # Reusable application code, when needed
├── notebooks/           # Exploratory notebooks, when needed
├── data/                # Non-sensitive sample data, when needed
└── requirements.txt     # Only if dependencies should be isolated
```

## Troubleshooting

### `No module named ipykernel`

Install the kernel package into the selected environment:

```powershell
conda activate llmapp
python -m pip install ipykernel
```

Then restart VS Code's notebook kernel.

### `No module named langchain_groq`

Install the workspace dependencies using the same interpreter selected by the notebook:

```powershell
conda activate llmapp
python -m pip install -r requirements.txt
```

### The package is installed but the notebook cannot import it

The terminal and notebook are using different Python interpreters. Recheck both the VS Code interpreter and the notebook kernel, then verify with:

```python
import sys
print(sys.executable)
```

## Documentation

- 📘 [Python environment guidance](./Python_Environment_Guide.docx)
- 📦 [Workspace dependencies](./requirements.txt)

## Security

Do not share or commit `.env` files, API keys, generated credentials, private datasets, or other sensitive material. Replace exposed credentials immediately.
