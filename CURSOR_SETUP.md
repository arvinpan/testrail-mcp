# Quick Setup Guide for Cursor

## Configure Cursor to Use Instawork TestRail MCP (with Sections Support)

1. Open Cursor Settings: `Cmd+,` (Mac) or `Ctrl+,` (Windows/Linux)

2. Navigate to: **Features > Model Context Protocol**

3. Click **Edit Config** (or add to your existing config)

4. Add this configuration:

```json
{
  "mcpServers": {
    "testrail": {
      "command": "uvx",
      "args": [
        "--from",
        "git+https://github.com/Instawork/testrail-mcp.git",
        "testrail-mcp"
      ],
      "env": {
        "TESTRAIL_URL": "https://instawork.testrail.io",
        "TESTRAIL_USERNAME": "your-email@instawork.com",
        "TESTRAIL_API_KEY": "your-api-key-here"
      }
    }
  }
}
```

5. Replace the environment variables:
   - `TESTRAIL_URL`: Your TestRail instance URL
   - `TESTRAIL_USERNAME`: Your TestRail email
   - `TESTRAIL_API_KEY`: Get from TestRail > My Settings > API Keys

6. Save and restart Cursor

7. Verify it's working by asking Cursor:
   ```
   Using TestRail MCP, get sections for project ID 123
   ```

## Available Section Tools

Now that sections support is added, you can use:

- `get_section(section_id)` - Get details of a specific section
- `get_sections(project_id, suite_id?)` - List all sections in a project/suite
- `add_section(project_id, name, description, suite_id?, parent_id?)` - Create new section
- `update_section(section_id, name?, description?)` - Update existing section
- `delete_section(section_id, soft)` - Delete a section
- `move_section(section_id, parent_id?, after_id?)` - Move section in hierarchy

## Troubleshooting

If you see errors:

1. **Check uvx is installed**:
   ```bash
   which uvx
   # If not found: curl -LsSf https://astral.sh/uv/install.sh | sh
   ```

2. **Test the MCP directly**:
   ```bash
   uvx --from git+https://github.com/Instawork/testrail-mcp.git testrail-mcp
   ```

3. **Check Cursor logs**: Cursor > View > Output > Select "MCP" from dropdown

4. **Verify credentials**: Test your API key at https://instawork.testrail.io/index.php?/api/v2/get_projects
