
### 🚀 Powered by ADG System
The original version of this document offers a superior layout and faster navigation. 
**Check it out here:** [Full Documentation Interface](https://draggame-adg-frontend.hf.space/docs/adg_doc_cca559f0da66e3b44151ebed98a51e1f)
---

# **Project Overview**

## **Project Title**  
AutoDoc Workflow Automation

---

## **Project Goal**  
The AutoDoc Workflow Automation project is designed to streamline and automate the generation of project documentation. By leveraging GitHub Actions and a configuration-driven approach, this project simplifies the process of maintaining up-to-date and comprehensive documentation for software repositories. It addresses the common challenge of keeping documentation synchronized with code changes, reducing manual effort and improving project maintainability.

---

## **Core Logic & Principles**  
The project operates as a GitHub Actions workflow triggered by specific events, such as code pushes to the `main` branch or manual dispatches. The workflow is defined in the `.github/workflows/autodoc.yml` file and integrates with a reusable workflow hosted in the `Drag-GameStudio/ADG` repository.

### Key Components:
1. **Workflow Triggering**:
   - The workflow is activated on two events:
     - Pushes to the `main` branch.
     - Manual workflow dispatch via GitHub Actions.

2. **Reusable Workflow Integration**:
   - The project uses a reusable workflow (`reuseble_agd.yml`) from the `Drag-GameStudio/ADG` repository. This modular approach enhances reusability and consistency across projects.

3. **Configuration-Driven Customization**:
   - The `autodocconfig.yml` file provides a flexible configuration system that allows users to customize the documentation generation process. Key settings include:
     - **Project Metadata**: Define the project name and language.
     - **File Exclusions**: Specify files and directories to ignore during documentation generation (e.g., Python bytecode, cache files, logs, version control files, and IDE settings).
     - **Build Settings**: Control logging behavior, such as saving logs and setting log verbosity.
     - **Structure Settings**: Configure the inclusion of introductory links, text, and order in the generated documentation.
     - **Global File Usage**: Enable or disable the use of a global configuration file.
     - **Documentation Part Size**: Set the maximum size for each part of the generated documentation.

4. **Security**:
   - The workflow uses a secret (`ADG_API_TOKEN`) to securely authenticate with external services or APIs, ensuring that sensitive information is not exposed.

---

## **Key Features**  
- **Automated Documentation Generation**: Automatically generates and updates project documentation upon code changes or manual triggers.  
- **Customizable Configuration**: Provides a flexible YAML-based configuration file (`autodocconfig.yml`) for tailoring the documentation process.  
- **File and Directory Exclusion**: Allows users to exclude specific files and directories from the documentation process, ensuring only relevant content is included.  
- **Integration with Reusable Workflows**: Leverages a reusable workflow to standardize and simplify the automation process.  
- **Secure Token Management**: Utilizes GitHub Secrets for secure handling of API tokens and other sensitive information.  
- **Structured Documentation Output**: Supports the inclusion of introductory links, text, and ordered sections for better readability.  
- **Scalable Documentation Size**: Configurable maximum size for documentation parts to accommodate large projects.  

---

## **Dependencies**  
To run the AutoDoc Workflow Automation project, the following dependencies are required:  
- **GitHub Actions**: The workflow is designed to run on GitHub's CI/CD platform.  
- **Reusable Workflow**: Hosted at `Drag-GameStudio/ADG/.github/workflows/reuseble_agd.yml`.  
- **GitHub Secrets**: Requires the `ADG_API_TOKEN` secret for secure authentication.  
- **YAML Configuration**: The `autodocconfig.yml` file must be present in the repository root for customization.  

Optional tools or libraries may be required depending on the specific implementation of the reusable workflow. Refer to the documentation in the `Drag-GameStudio/ADG` repository for further details.  

--- 

This project provides a robust and efficient solution for automating documentation workflows, ensuring that project documentation remains accurate, organized, and up-to-date with minimal manual intervention.
## Executive Navigation Tree

- 📄 AutoDoc
  - [Workflow](#autodoc-workflow)
  - [Config](#autodoc-config)
<a name="autodoc-workflow"></a>
## AutoDoc Workflow Configuration (`.github/workflows/autodoc.yml`)

This file defines the GitHub Actions workflow for automating the documentation generation process in the repository. It triggers the `AutoDoc` workflow on specific events and delegates the execution to a reusable workflow.

### Workflow Trigger Events
The workflow is configured to execute under the following conditions:
- **Push to the `main` branch**: Automatically triggers the workflow when changes are pushed to the `main` branch.
- **Manual Dispatch**: Allows manual execution of the workflow via the GitHub Actions interface.

### Workflow Structure
The workflow is defined with the following key components:

#### 1. **Workflow Name**
   - **Name**: `AutoDoc`
   - This is the identifier for the workflow in the GitHub Actions UI.

#### 2. **Trigger Events**
   - **Push**: Monitors the `main` branch for changes.
   - **Workflow Dispatch**: Enables manual execution.

#### 3. **Job: `run`**
   - **Permissions**: Grants `write` access to repository contents for the job.
   - **Reusable Workflow**: Delegates execution to a reusable workflow located at:
     ```
     Drag-GameStudio/ADG/.github/workflows/reuseble_agd.yml@main
     ```
   - **Secrets**:
     - `ADG_API_TOKEN`: A secret token required for the reusable workflow. It is securely passed from the repository's secrets configuration.

---

### Data Contract for `.github/workflows/autodoc.yml`

| Entity             | Type       | Role                                   | Notes                                                                 |
|---------------------|------------|----------------------------------------|-----------------------------------------------------------------------|
| `name`             | String     | Workflow identifier                   | Displays as `AutoDoc` in GitHub Actions.                             |
| `on.push.branches` | Array      | Trigger condition                     | Executes workflow on pushes to the `main` branch.                    |
| `on.workflow_dispatch` | Boolean | Trigger condition                     | Allows manual triggering of the workflow.                            |
| `jobs.run.permissions.contents` | String | Permissions for the job           | Grants `write` access to repository contents.                        |
| `jobs.run.uses`    | String     | Reusable workflow reference           | Points to the reusable workflow in the `Drag-GameStudio/ADG` repo.   |
| `jobs.run.secrets.ADG_API_TOKEN` | Secret | Authentication token for the job | Passed securely from repository secrets.                             |

---
<a name="autodoc-config"></a>
## AutoDoc Configuration (`autodocconfig.yml`)

This file defines the configuration settings for the AutoDoc tool, specifying project details, file exclusions, build preferences, and structural settings.

### Key Configuration Sections

#### 1. **Project Metadata**
   - **Project Name**: `"Project"` (used as a unique identifier for the documentation).
   - **Language**: `"en"` (documentation language is set to English).

#### 2. **File Exclusions**
   - A comprehensive list of file patterns and directories to ignore during the documentation generation process. These include:
     - **Python Bytecode and Cache**: Files like `*.pyc`, `*.pyo`, `__pycache__`, etc.
     - **Environment and IDE Settings**: Directories like `venv`, `.vscode`, `.idea`, etc.
     - **Databases and Binary Data**: Files like `*.sqlite3`, `*.db`, `data`, etc.
     - **Logs and Coverage Reports**: Files like `*.log`, `.coverage`, `htmlcov`, etc.
     - **Version Control and Static Assets**: Directories like `.git`, `static`, `migrations`, etc.
     - **Miscellaneous**: Files like `*.pdb`, `*.md`, etc.

#### 3. **Build Settings**
   - **`save_logs`**: `false` (logs are not saved after execution).
   - **`log_level`**: `2` (sets the verbosity level of logs).

#### 4. **Structure Settings**
   - **`include_intro_links`**: `true` (introductory links are included in the documentation).
   - **`include_intro_text`**: `true` (introductory text is included in the documentation).
   - **`include_order`**: `true` (documentation sections are ordered).
   - **`use_global_file`**: `true` (global configuration file is used).
   - **`max_doc_part_size`**: `5000` (maximum size of each documentation part in characters).

---

### Data Contract for `autodocconfig.yml`

| Entity                   | Type       | Role                                   | Notes                                                                 |
|---------------------------|------------|----------------------------------------|-----------------------------------------------------------------------|
| `project_name`           | String     | Unique project identifier             | Set to `"Project"`.                                                  |
| `language`               | String     | Documentation language                | Set to English (`"en"`).                                             |
| `ignore_files`           | Array      | Patterns to exclude during processing | Covers cache, environment, logs, version control, and miscellaneous. |
| `build_settings.save_logs` | Boolean  | Log retention setting                 | Logs are not saved (`false`).                                        |
| `build_settings.log_level` | Integer  | Log verbosity level                   | Set to `2` (medium verbosity).                                       |
| `structure_settings.include_intro_links` | Boolean | Include intro links in docs         | Set to `true`.                                                       |
| `structure_settings.include_intro_text` | Boolean | Include intro text in docs          | Set to `true`.                                                       |
| `structure_settings.include_order` | Boolean | Include section ordering             | Set to `true`.                                                       |
| `structure_settings.use_global_file` | Boolean | Use global configuration file        | Set to `true`.                                                       |
| `structure_settings.max_doc_part_size` | Integer | Max size of doc parts (characters)   | Set to `5000`.                                                       |

---

> **Note**: The configuration and workflow files are tightly coupled. The `autodoc.yml` workflow relies on the `autodocconfig.yml` file for execution parameters and file exclusions. Ensure both files are synchronized for optimal functionality.

    