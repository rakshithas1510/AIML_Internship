# 📄 Resume Ranker AI

An intelligent, open-source tool that uses AI and semantic similarity to automatically evaluate and rank candidate resumes against a provided job description. It drastically speeds up the initial screening process for recruiters and helps job seekers tailor their applications.

## ✨ Features

  * **Multiple File Support:** Upload multiple resumes and job descriptions in one go.
  * **Format Compatibility:** Supports both **PDF (`.pdf`)** and **Word (`.docx`)** file formats.
  * **Automatic JD Detection:** The application automatically identifies the Job Description file from the batch of uploaded files.
  * **Similarity Scoring:** Calculates a precise match score for each resume against the JD using state-of-the-art Natural Language Processing (NLP) models.
  * **Ranked Output:** Displays the results in a ranked table (DataFrame) showing the match score for each resume.
  * **Visualization & Export:** Generates a score chart and allows you to **download the full results as a CSV file**.
  * **Web Interface:** Uses a user-friendly **Gradio** interface for easy interaction.

## 💻 Technologies Used

| Category | Tool/Library |
| :--- | :--- |
| **Interface** | Gradio |
| **NLP/AI** | Sentence-Transformers, scikit-learn |
| **File Handling** | pdfplumber, python-docx |
| **Data & Plotting** | Pandas, NumPy, Matplotlib |

## 🚀 Installation and Setup

Follow these steps to get a local copy of the project up and running.

### 1\. Clone the Repository

```bash
git clone <YOUR-GITHUB-REPO-URL>
cd resume-ranker-ai
```

### 2\. Create a Virtual Environment (Recommended)

```bash
# For Windows
python -m venv venv
.\venv\Scripts\activate

# For macOS/Linux
python3 -m venv venv
source venv/bin/activate
```

### 3\. Install Dependencies

You will need the following libraries to run the `resume_ai.ipynb` notebook.

```bash
pip install gradio sentence-transformers pdfplumber python-docx scikit-learn matplotlib
```

*(**Note**: For production, it's best practice to create a `requirements.txt` file and install using `pip install -r requirements.txt`)*

### 4\. Run the Application

Since the core logic is in a Jupyter Notebook with a Gradio interface, you can run it directly:

```bash
jupyter notebook resume_ai.ipynb
# OR, if you convert it to a Python script (app.py)

# Run the Gradio app directly
python app.py
```

## 🛠️ Usage

1.  Access the Gradio application via your browser (usually at `http://127.0.0.1:7860`).
2.  Click the **"Upload Resumes and Job Descriptions"** file input box.
3.  Upload all your candidate resumes and the Job Description (JD) file at once. The system will automatically detect the JD.
4.  The application will process the files and display the:
      * **Resume Match Results** table (DataFrame).
      * **Score Chart** visualization.
      * A link to **Download CSV** of the ranked results.
