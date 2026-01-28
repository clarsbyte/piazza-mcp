# Piazza MCP Server

An MCP (Model Context Protocol) server that allows Claude Code to interact with Piazza, enabling you to fetch posts and course information directly from your terminal.

## Prerequisites

- Python 3.10+
- A Piazza account
- Claude Code CLI

## Installation

1. Clone or download this repository

2. Create a virtual environment and install dependencies:
   ```bash
   python -m venv env

   # Windows
   env\Scripts\activate

   # macOS/Linux
   source env/bin/activate

   pip install -r requirements.txt
   ```

## Configuration

### Getting Your Course IDs

To find a course ID:

1. Log in to Piazza in your browser
2. Navigate to the course you want to add
3. Look at the URL - it will look like: `https://piazza.com/class/abc123xyz`
4. The course ID is the part after `/class/` (e.g., `abc123xyz`)

### Setting Up Claude Code

Create or edit the `.mcp.json` file in your project directory:

```json
{
  "mcpServers": {
    "piazza": {
      "command": "/path/to/your/env/bin/python",
      "args": ["/path/to/piazza-mcp/main.py"],
      "env": {
        "PIAZZA_EMAIL": "your-email@example.com",
        "PIAZZA_PASSWORD": "your-piazza-password",
        "PIAZZA_COURSES": "{\"course_id_1\":\"Course Name 1\",\"course_id_2\":\"Course Name 2\"}"
      }
    }
  }
}
```

**Windows example:**
```json
{
  "mcpServers": {
    "piazza": {
      "command": "C:\\path\\to\\env\\Scripts\\python.exe",
      "args": ["C:\\path\\to\\piazza-mcp\\main.py"],
      "env": {
        "PIAZZA_EMAIL": "student@university.edu",
        "PIAZZA_PASSWORD": "yourpassword",
        "PIAZZA_COURSES": "{\"mjz1kp056nb6t3\":\"CSE 12\",\"mk06sxvpt521xv\":\"ECON 1\"}"
      }
    }
  }
}
```

**macOS/Linux example:**
```json
{
  "mcpServers": {
    "piazza": {
      "command": "/home/user/piazza-mcp/env/bin/python",
      "args": ["/home/user/piazza-mcp/main.py"],
      "env": {
        "PIAZZA_EMAIL": "student@university.edu",
        "PIAZZA_PASSWORD": "yourpassword",
        "PIAZZA_COURSES": "{\"mjz1kp056nb6t3\":\"CSE 12\",\"mk06sxvpt521xv\":\"ECON 1\"}"
      }
    }
  }
}
```

### Environment Variables

| Variable | Description |
|----------|-------------|
| `PIAZZA_EMAIL` | Your Piazza account email |
| `PIAZZA_PASSWORD` | Your Piazza account password |
| `PIAZZA_COURSES` | JSON object mapping course IDs to course names |

## Available Tools

Once configured, Claude Code will have access to these tools:

### `list_courses`
Returns the list of configured courses.

**Example usage in Claude Code:**
```
"What courses do I have configured?"
"List my Piazza courses"
```

### `fetch_posts`
Fetches recent posts from a specified course.

**Parameters:**
- `course_id` (required): The Piazza course ID
- `n` (optional): Number of posts to fetch (default: 10)

**Example usage in Claude Code:**
```
"Show me the last 5 posts from CSE 12"
"What are the recent questions on ECON 1?"
"Check the latest 3 posts on my physics class"
```

## Usage Examples

After configuration, simply start Claude Code in a directory with the `.mcp.json` file:

```bash
claude
```

Then you can ask natural language questions like:

- "What are my Piazza courses?"
- "Show me the last 3 posts on ECON 1"
- "Are there any new questions about the midterm in CSE 12?"
- "What's the latest instructor answer on PHYS 2A?"
