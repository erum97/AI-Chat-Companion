# 🇵🇰 Chat Companion — Pakistan Travel RAG App

A beginner-friendly Streamlit application that acts as an AI travel companion for foreign tourists visiting Pakistan.

The app uses a simple **RAG (Retrieval-Augmented Generation)** approach:

1. The visitor asks a question.
2. The app searches its small Pakistan travel knowledge base using TF-IDF.
3. The most relevant information is retrieved.
4. The retrieved information is added to the prompt.
5. Groq generates a friendly answer using that context.

This project intentionally avoids LangChain and a vector database so a complete beginner can understand the basic RAG flow.

---

## 📁 Project structure

Create these files in the **root (top level) of the same GitHub repository**:

```text
your-repository/
├── app.py
├── requirements.txt
├── README.md
└── .gitignore
```

There is no need to create folders for this beginner version.

### What each file does

| File | Purpose |
|---|---|
| `app.py` | The complete Streamlit application |
| `requirements.txt` | Python packages that Streamlit Community Cloud installs |
| `README.md` | Project documentation and beginner instructions |
| `.gitignore` | Prevents files such as API secrets from being uploaded |

---

# 1. Create the GitHub repository

You do **not** need Google Colab, VS Code, or a terminal.

### Step 1

Open GitHub:

https://github.com/

Sign in to your GitHub account.

### Step 2

Click **+** in the top-right corner and choose **New repository**.

### Step 3

Give the repository a simple name, for example:

```text
pakistan-travel-chat-companion
```

You can make it public or private.

For a first project, a public repository is usually the easiest option for Streamlit Community Cloud.

### Step 4

Click **Create repository**.

---

# 2. Create `app.py` on GitHub

Open your new repository.

Click:

**Add file → Create new file**

In the filename box, type:

```text
app.py
```

Paste the complete `app.py` code supplied with this project.

Then click:

**Commit changes**

### Important

`app.py` must be directly in the main/root area of the repository.

Correct:

```text
pakistan-travel-chat-companion/app.py
```

Avoid putting it inside another folder for this beginner setup.

---

# 3. Create `requirements.txt`

In the same GitHub repository, click:

**Add file → Create new file**

Filename:

```text
requirements.txt
```

Paste:

```text
streamlit>=1.35.0
groq>=0.11.0
scikit-learn>=1.4.0
```

Click:

**Commit changes**

### Why are these packages needed?

- `streamlit` → creates the web app.
- `groq` → connects the app to the Groq API.
- `scikit-learn` → performs the simple TF-IDF retrieval used by the RAG system.

Streamlit Community Cloud reads `requirements.txt` and installs the listed packages when deploying the app.

---

# 4. Create `README.md`

GitHub normally creates a README automatically when you create a repository, but you can replace it with this project README.

If you need to create it manually:

**Add file → Create new file**

Filename:

```text
README.md
```

Paste this documentation.

Then click:

**Commit changes**

---

# 5. Create `.gitignore`

In the same repository:

**Add file → Create new file**

Filename:

```text
.gitignore
```

Notice that the filename starts with a dot.

Paste:

```text
# Python
__pycache__/
*.py[cod]
*.pyo
*.pyd
.Python

# Virtual environments
.venv/
venv/
env/
ENV/

# Streamlit secrets - NEVER upload this file
.streamlit/secrets.toml

# Local/editor files
.vscode/
.idea/
.DS_Store

# Test/coverage files
.pytest_cache/
.coverage
htmlcov/
```

Click:

**Commit changes**

---

# 6. Understand the RAG part

You may hear the word **RAG** and think you need a complicated AI system.

You don't for this project.

The basic flow in `app.py` is:

```text
User question
      ↓
TF-IDF retrieval
      ↓
Relevant Pakistan travel information
      ↓
Groq prompt
      ↓
AI answer
```

The travel information is stored in `KNOWLEDGE_BASE` near the top of `app.py`.

For example, the knowledge base contains sections for:

- Visa & entry
- Clothing & cultural etiquette
- Useful Urdu
- Religious respect
- Money & ATMs
- Getting around cities
- Photography & security
- Emergency contacts

The app retrieves the most relevant sections before asking Groq for the final response.

This is a simple form of RAG and is intentionally easy to understand.

---

# 7. Get a Groq API key

The application needs a Groq API key to generate AI answers.

Go to the Groq Console:

https://console.groq.com/

Sign in or create an account.

Create an API key.

### VERY IMPORTANT

Do **not** paste your API key into `app.py`.

Do **not** put it in `requirements.txt`.

Do **not** put it in `README.md`.

Do **not** commit it to GitHub.

If an API key is accidentally published, treat it as compromised and replace/revoke it.

---

# 8. Add the Groq key using Streamlit Secrets

Streamlit Community Cloud provides a Secrets area specifically for credentials.

After deployment:

1. Open your Streamlit app.
2. Open the app's settings.
3. Find **Secrets**.
4. Paste:

```toml
GROQ_API_KEY = "PASTE_YOUR_REAL_GROQ_KEY_HERE"
```

You can optionally specify the Groq model:

```toml
GROQ_API_KEY = "PASTE_YOUR_REAL_GROQ_KEY_HERE"
GROQ_MODEL = "llama-3.3-70b-versatile"
```

Replace the placeholder with your actual API key.

Do not add the key to GitHub.

The code reads it using:

```python
st.secrets["GROQ_API_KEY"]
```

---

# 9. Deploy on Streamlit Community Cloud

Open:

https://share.streamlit.io/

Sign in using GitHub.

If Streamlit asks for GitHub permission, authorize the connection.

### Step 1 — Create the app

Click:

**Create app**

Choose:

**Yup, I have an app.**

### Step 2 — Select your GitHub repository

Choose:

- Your GitHub username
- Repository: `pakistan-travel-chat-companion`
- Branch: usually `main`
- Main file path:

```text
app.py
```

### Step 3 — Add Secrets

Before deploying, open:

**Advanced settings**

Find the **Secrets** field.

Paste:

```toml
GROQ_API_KEY = "YOUR_REAL_GROQ_API_KEY"
GROQ_MODEL = "llama-3.3-70b-versatile"
```

Do not put quotation marks around the key name itself. Keep the quotation marks around the key value.

### Step 4 — Deploy

Click:

**Deploy**

Streamlit will install the packages from `requirements.txt` and start `app.py`.

The first deployment can take a few minutes.

After deployment, Streamlit gives your app a public `streamlit.app` URL.

---

# 10. Test the app

Open your Streamlit app URL.

Try these questions:

```text
What should I wear when visiting Pakistan?
```

```text
How do I apply for a Pakistani tourist visa?
```

```text
What should I carry when travelling to Hunza?
```

```text
Can I photograph a check-post?
```

```text
What are some useful Urdu phrases?
```

```text
What emergency numbers should I know?
```

You should see:

1. Your question.
2. A generated answer.
3. A **Knowledge used for this answer** section showing which RAG passages were retrieved.

That source display is useful when you are learning how RAG works.

---

# 11. How the important code works

## The knowledge base

Near the top of `app.py`:

```python
KNOWLEDGE_BASE = [
    {
        "title": "Visa & entry",
        "text": "..."
    }
]
```

Each item is a small piece of information that the AI can use.

You can add more items later.

---

## TF-IDF retrieval

The app converts the knowledge-base text into searchable numerical vectors:

```python
VECTORIZER = TfidfVectorizer(stop_words="english")
DOCUMENT_MATRIX = VECTORIZER.fit_transform(DOCUMENTS)
```

When a visitor asks a question, this function searches for relevant passages:

```python
retrieve_context(question)
```

It returns the most relevant pieces.

---

## Sending context to Groq

The retrieved information is added to the system prompt.

Conceptually:

```text
User question
+
Relevant knowledge
+
Safety instructions
        ↓
      Groq
        ↓
    Final answer
```

This helps the model answer from the travel information instead of relying only on its general knowledge.

---

# 12. Why the API key is not in `app.py`

You will see code like:

```python
if "GROQ_API_KEY" not in st.secrets:
    return None
```

and:

```python
Groq(api_key=st.secrets["GROQ_API_KEY"])
```

This means the secret is supplied by Streamlit rather than hard-coded into the program.

That is why `.gitignore` contains:

```text
.streamlit/secrets.toml
```

Never upload a local `secrets.toml` file containing your real key to GitHub.

---

# 13. How to update the app later

You can make changes directly through GitHub's website.

For example:

1. Open your GitHub repository.
2. Open `app.py`.
3. Click the pencil/edit button.
4. Make your change.
5. Click **Commit changes**.

Streamlit Community Cloud watches the connected GitHub repository. When the repository changes, the deployed app can update automatically.

---

# 14. Adding more travel knowledge

To make the RAG system more useful, add another item to `KNOWLEDGE_BASE`.

Example:

```python
{
    "title": "Your new topic",
    "text": (
        "Your carefully checked travel information goes here."
    ),
},
```

Good future topics could include:

- SIM card setup
- Airport arrival tips
- Hotel etiquette
- Food safety
- Train travel
- Domestic flight tips
- Women travelers
- Accessibility
- Weather preparation
- Northern-area road travel

For information that can change quickly, verify it against an official or current source before adding it to the knowledge base.

---

# 15. Important safety principle

This chatbot is a travel assistant, not an immigration officer, police officer, doctor, lawyer, or embassy.

For visa, border, security, emergency, or other high-stakes questions, travelers should verify the current information with the relevant official authority.

For Pakistan visa applications, use the official NADRA Pakistan Online Visa portal:

https://visa.nadra.gov.pk/

Avoid unofficial visa websites.

---

# 16. Common beginner problems

## "The app says the Groq API key is missing"

Check Streamlit:

**App → Settings → Secrets**

Make sure you have:

```toml
GROQ_API_KEY = "your-real-key"
```

Save the secrets and restart/redeploy the app if necessary.

---

## "ModuleNotFoundError"

Check that `requirements.txt` contains:

```text
streamlit>=1.35.0
groq>=0.11.0
scikit-learn>=1.4.0
```

Then allow Streamlit Community Cloud time to reinstall the dependencies.

---

## "The app deployed but the page is blank"

Open the Streamlit app logs.

The error message normally tells you which line or dependency caused the problem.

Check especially:

- `app.py` spelling
- `requirements.txt` spelling
- Secrets
- Python/package errors

---

# 17. Beginner roadmap

You do not need to learn everything at once.

Learn in this order:

### Level 1
Understand:

```text
Streamlit → web page
```

### Level 2
Understand:

```text
Python → application logic
```

### Level 3
Understand:

```text
TF-IDF → retrieves relevant information
```

### Level 4
Understand:

```text
Groq API → generates the final answer
```

### Level 5
Understand:

```text
RAG = retrieval + AI generation
```

Once these five ideas make sense, you will understand the basic architecture of this project.

---

## Official documentation

Streamlit Community Cloud:
https://docs.streamlit.io/deploy/streamlit-community-cloud

Streamlit secrets:
https://docs.streamlit.io/deploy/streamlit-community-cloud/deploy-your-app/secrets-management

Groq quickstart:
https://console.groq.com/docs/quickstart

Pakistan Online Visa:
https://visa.nadra.gov.pk/

