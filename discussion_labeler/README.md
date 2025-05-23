# GitHub Discussion Auto-Labeler

Automatically labels GitHub discussions using AI to analyze content and apply appropriate tags based on discussion content.

## Features

- Automatically applies labels to new GitHub discussions
- Uses Azure OpenAI with Prompty for advanced content analysis
- Supports both GitHub token and GitHub App authentication methods
- Can be run locally or as a GitHub Action with scheduled monitoring

## Setup

### Prerequisites

- Python 3.10+
- GitHub token or GitHub App credentials
- Azure OpenAI service (for AI-based labeling)
- Prompty library for AI integration

### Installation

1. Clone this repository
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Create a `.env` file with your credentials based on the environment variables listed below

### Environment Variables

| Variable | Description |
|----------|-------------|
| `TOKEN` | GitHub personal access token |
| `APP_ID` | GitHub App ID |
| `APP_PRIVATE_KEY` | GitHub App private key (content as string) |
| `APP_PRIVATE_KEY_PATH` | Alternative: path to the private key file |
| `APP_INSTALLATION_ID` | GitHub App installation ID |
| `DEFAULT_REPO` | Repository to monitor in format `owner/repo` (default: "golclinics/discussions") |
| `AZURE_OPENAI_ENDPOINT` | Azure OpenAI API endpoint |
| `AZURE_OPENAI_KEY` | Azure OpenAI API key |
| `AZURE_OPENAI_API_VERSION` | Azure OpenAI API version |
| `RUN_INTERVAL_MINUTES` | How often to check for new discussions (in minutes) |
| `REQUEST_TIMEOUT` | API request timeout in seconds (default: 30) |
| `SECRET_KEY` | Secret key for secure operations |

## Usage

### Running Locally

To run the script locally and continuously monitor for new discussions:

```bash
python basic.py
```

This will start a monitoring process that checks for new unlabeled discussions at the specified interval.

### Running a Single Labeling Process

To run a one-time labeling process without continuous monitoring:

```bash
python -c "import basic; basic.process_discussions()"
```

You can also specify a custom repository:

```bash
python -c "import basic; basic.process_discussions('owner/repo')"
```

### Creating Repository Labels

To create the labels defined in `tags.json` in your repository:

```bash
python new-labels.py
```

This script also supports an interactive mode that prompts you to add labels to a specific discussion.

### GitHub Action

This repo includes a GitHub Action workflow that automatically runs when new discussions are created.

To set up the GitHub Action:
1. Configure repository secrets with the environment variables listed above
2. The Action will run automatically when new discussions are created
3. The workflow can also be triggered manually via the workflow_dispatch event

## Customizing Labels

Edit the `tags.json` file to customize the available labels:

```json
{
  "tags": [
    {"name": "label-name", "description": "Label description", "color": "hex-color"}
  ]
}
```

## License

MIT
