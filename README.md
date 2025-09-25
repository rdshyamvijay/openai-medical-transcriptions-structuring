# Medical Transcription to Structured Data with ICD-10 Mapping

## Project Description
This project demonstrates how to use the **OpenAI Chat Completions API** to transform free-text medical transcriptions into structured data fields. It extracts **patient age**, **recommended treatment or procedure**, and the **medical specialty**, and then maps the treatment to its most relevant **ICD-10 code(s)**.  

The workflow showcases how large language models (LLMs) can be applied in healthcare data engineering and clinical coding, converting unstructured text into structured, analysis-ready data. While this project is educational and designed for learning purposes, the techniques reflect how AI can support real-world medical documentation and coding.

---

## Features
- Extracts **Age** and **Treatment/Procedure** using OpenAI function calling.
- Retrieves **ICD-10 codes** for the treatment/procedure using a second model call.
- Includes **Medical Specialty** directly from the dataset.
- Outputs results in a clean **pandas DataFrame**.
- Uses environment variables (`.env`) to securely manage API keys.

## Setup Instructions

### 1. Clone the repository
```bash
git clone https://github.com/rdshyamvijay/medical-transcription-icd10-extractor.git
cd medical-transcription-icd10-extractor

2. Create and activate a virtual environment

python -m venv .venv
source .venv/bin/activate   # On Windows: .venv\Scripts\activate

3. Install dependencies

pip install -r requirements.txt

4. Configure environment variables

Copy .env.example to .env:

cp .env.example .env

Edit .env and add your OpenAI API key:

OPENAI_API_KEY=sk-xxxxxx


⸻

How It Works
	1.	Load dataset
A CSV file (data/transcriptions.csv) with two columns:
	•	medical_specialty
	•	transcription
	2.	Extract fields using function calling
The model is asked (via a structured function definition) to always return:
	•	Age
	•	Recommended Treatment/Procedure
	3.	Get ICD-10 codes
A second prompt maps the treatment text to ICD-10 codes.
Example result: "J30.9 - R05 - R09.81"
	4.	Build structured DataFrame
All rows are processed and assembled into df_structured:

Age	Recommended Treatment/Procedure	Medical Specialty	ICD Code
23	She will try Zyrtec…	Allergy / Immunology	J30.9 - R05 - R09.81
41	Operative fixation…	Orthopedic	S86.011A - S86.012A …


	5.	Save results (optional)

df_structured.to_csv("df_structured.csv", index=False)



⸻

Usage

Run the script in a notebook or as a .py file:

python script.py


⸻

Requirements
	•	Python 3.9+
	•	pandas
	•	openai
	•	python-dotenv

⸻

Limitations
	•	ICD-10 mapping is AI-assisted and may not always be accurate. It should not be used for clinical decision-making without human verification.
	•	Prompts are tuned for this dataset; different datasets may need adjustments.

⸻

License

This project is released under the MIT License.

---
