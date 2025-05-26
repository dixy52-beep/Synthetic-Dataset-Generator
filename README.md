# Synthetic Dataset Generator (with Gemini AI & Hugging Face)

Generate structured datasets using Google's Gemini AI and automatically upload them to your Hugging Face account. This application, designed to run in Google AI Studio, simplifies the process of creating synthetic data based on your specifications.

## Overview

This tool leverages the power of Gemini AI to generate datasets tailored to your needs. You provide a descriptive prompt, define the structure or initial examples, specify the number of rows, and the application handles the generation and uploads the resulting dataset to your Hugging Face Hub repository.

## Features

*   **AI-Powered Data Generation:** Utilizes Gemini AI for flexible and context-aware data synthesis.
*   **Structured Output:** Creates datasets in a structured format (e.g., CSV, JSON Lines - *specify if known, otherwise keep general*).
*   **Hugging Face Integration:** Automatically uploads the generated dataset to your Hugging Face account.
*   **Customizable Prompts:** Define the dataset's goal, initial structure/examples, and further context through a simple prompt format.
*   **User-Friendly:** Designed for ease of use within Google AI Studio.

## How it Works

1.  **Input:** You provide your Hugging Face username, a Hugging Face API token (with write permissions), a descriptive prompt, and the desired number of rows for the dataset.
2.  **Processing:** The application sends your prompt and requirements to the Gemini AI model.
3.  **Generation:** Gemini AI generates the data based on your input.
4.  **Formatting:** The generated data is formatted into a structured dataset.
5.  **Upload:** The dataset is uploaded to a new repository (or an existing one, *specify behavior if known*) on your Hugging Face Hub account.

## Requirements

*   Access to Google AI Studio (or a Python environment capable of running Gemini API calls).
*   A Hugging Face account.
*   A Hugging Face API token with `write` permissions. You can generate one from your Hugging Face account settings (Settings -> Access Tokens -> New token with "write" role).
*   Python (if running locally).
*   Required Python libraries (these will likely be managed by AI Studio, but if a `requirements.txt` is included, mention it):
    *   `google-generativeai`
    *   `huggingface_hub`
    *   (Potentially `pandas` or other data manipulation libraries)

## Setup & Installation

1.  **Download:** Obtain the application files (e.g., the `.zip` archive).
2.  **Extract:** Unzip the archive to your desired location.
3.  **Google AI Studio:**
    *   Upload or open the project files (e.g., Python script or notebook) in Google AI Studio.
    *   Ensure your AI Studio environment is configured with access to the Gemini API.
4.  **(Optional) Local Setup:**
    *   If running locally, ensure Python is installed.
    *   Install required dependencies:
        ```bash
        pip install google-generativeai huggingface_hub pandas # Add other libraries if needed
        ```
    *   Set up your Google API Key for Gemini as an environment variable or within the script as per Google's SDK guidelines.

## Usage

1.  **Run the Application:**
    *   **In AI Studio:** Execute the main script or notebook.
    *   **(If applicable) Locally:** Run the main Python script from your terminal (e.g., `python your_script_name.py`).

2.  **Provide Inputs:** The application will prompt you for the following information:
    *   **Hugging Face Username:** Your username on Hugging Face (e.g., `my-hf-username`).
    *   **Hugging Face Token:** Your Hugging Face API token with write permissions.
    *   **Prompt:** A string defining the dataset you want to generate, following the format:
        `"Overall Goal of the Dataset" / "Column Definitions or First Set of Examples" / "Further Context or Second Set of Examples"`
    *   **Number of Rows:** The desired number of data entries in the dataset.

### Prompt Format Explained:

The prompt is structured into three parts, separated by a `/` (forward slash):

*   **`Overall Goal of the Dataset`**: Describe the purpose or theme of the dataset.
    *   *Example:* `"Generate a list of fictional book titles and their authors"`
*   **`Column Definitions or First Set of Examples`**: Define the structure of your data. This could be column names, data types, or a few illustrative examples.
    *   *Example (Column Names):* `"title: string, author: string, genre: string, publication_year: integer"`
    *   *Example (Illustrative Examples):* `"The Azure Dragon, Ada Quill, Fantasy, 2023 / Whispers of the Void, Lex Syntax, Sci-Fi, 2021"`
*   **`Further Context or Second Set of Examples`**: Provide additional information, constraints, or more examples to guide Gemini AI in generating relevant and diverse data.
    *   *Example:* `"Ensure genres are diverse, including Fantasy, Sci-Fi, Mystery, Romance. Publication years should be between 1980 and 2024. Authors should have unique-sounding names."`

**Full Prompt Example:**

`"Generate a list of fictional book titles and their authors" / "title: string, author: string, genre: string, publication_year: integer" / "Ensure genres are diverse, including Fantasy, Sci-Fi, Mystery, Romance. Publication years should be between 1980 and 2024. Authors should have unique-sounding names."`

**Number of Rows Example:** `100`

## Configuration

*   **Hugging Face Token:** This is a critical piece of information. Ensure it is kept secure and has the necessary `write` permissions for uploading datasets. It's recommended to provide this at runtime when prompted, or use environment variables if running locally (`HF_TOKEN`).
*   **Gemini API Key:** If running outside of AI Studio where it's typically pre-configured, you'll need to set up your Google API Key for the Gemini API according to the `google-generativeai` library documentation (often via the `GOOGLE_API_KEY` environment variable).

## Output

*   A new dataset repository will be created under your Hugging Face account. The repository name might be derived from the "goal" part of your prompt or follow a predefined naming convention (e.g., `gemini-generated-dataset-<timestamp>`).
*   The dataset will contain the structured data generated by Gemini AI, typically in a common format like CSV or JSON Lines.
*   The application should provide a link or the name of the Hugging Face repository where the dataset has been uploaded.

## Example Scenario

**Input:**

*   **HF Username:** `testuser`
*   **HF Token:** `hf_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx`
*   **Prompt:** `"Create a dataset of customer support tickets for an e-commerce platform" / "ticket_id: string, customer_email: email, issue_description: string, status: (Open|Closed|Pending), priority: (Low|Medium|High)" / "Issues should relate to orders, shipping, returns, or account problems. Ensure a mix of statuses and priorities."`
*   **Number of Rows:** `50`

**Expected Output:**

*   A message indicating successful dataset generation and upload.
*   A new dataset repository on Hugging Face (e.g., `testuser/customer-support-tickets-ecommerce`) containing a file (e.g., `dataset.csv`) with 50 rows matching the described structure and context.

## Troubleshooting

*   **Authentication Errors (Hugging Face):** Double-check your Hugging Face token for typos and ensure it has `write` permissions.
*   **API Errors (Gemini):** Ensure your Gemini API setup is correct (especially if running locally) and that you haven't exceeded any usage quotas. Check the error messages from the AI Studio or console for more details.
*   **Incorrect Output Format:** Refine your prompt, especially the "Column Definitions or First Set of Examples" part, to be more specific about the desired structure.
*   **Low-Quality Data:** Experiment with the "Further Context" part of your prompt to provide clearer instructions and constraints to Gemini AI. Breaking down complex requests into simpler parts in the prompt can also help.

## Contributing

*(Optional: Add guidelines if you want others to contribute. For example: "Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.")*

## License

MIT ATTRIBUTION REQUIRED (Davide Brunori 2025)
