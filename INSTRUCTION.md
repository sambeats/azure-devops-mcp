# INSTRUCTION.md

## How to Run the Azure DevOps MCP Server Locally

This guide explains how to set up and run the Azure DevOps MCP Server from source for local development and testing.

---

### 1. Prerequisites
- **Node.js** v20 or higher ([Download](https://nodejs.org/en/download))
- **npm** (comes with Node.js)
- **Azure CLI** ([Install Guide](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest))
- **VS Code** (recommended, but not required)

---

### 2. Azure Login
Before running the server, log in to Azure DevOps using the Azure CLI:

```sh
az login
```

---

### 3. Install Dependencies
Navigate to the `azure-devops-mcp` directory and install dependencies:

```sh
cd azure-devops-mcp
npm install
```

---

### 4. Build the Project
Build the TypeScript source code:

```sh
npm run build
```

---

### 5. Run the MCP Server Locally
You can start the server using the following command:

```sh
npm start
```

Or, to run the server directly (as used in `.vscode/mcp.json` and `mcp.json`):

```sh
node dist/index.js <your-ado-org-name>
```
Replace `<your-ado-org-name>` with your Azure DevOps organization name (e.g., `contoso`).

---

### 6. Example `mcp.json` for Local Testing
To test the MCP server locally, use the following `mcp.json` (place it in the root or in `.vscode/`):

```
{
  "inputs": [
    {
      "id": "ado_org",
      "type": "promptString",
      "description": "Azure DevOps organization name  (e.g. 'contoso')"
    }
  ],
  "servers": {
    "ado": {
      "type": "stdio",
      "command": "mcp-server-azuredevops",
      "args": ["${input:ado_org}"]
    }
  }
}
```

- This configuration will prompt you for your Azure DevOps organization name when starting the server.
- If you want to hardcode the org name for testing, you can replace `"${input:ado_org}"` with your org name, e.g. `["contoso"]`.

---

### 7. Usage
- Start the server as described above.
- In VS Code, switch to Agent Mode in Copilot Chat, select the Azure DevOps MCP server as a tool, and try prompts like `List ADO projects`.

---

### 8. Testing

#### Running Unit Tests
To run the complete test suite including tests for the new attachment tools:

```sh
npm test
```

To run tests with coverage:

```sh
npm run test:coverage
```

To run tests for a specific tool file:

```sh
npm test -- --testPathPattern=workitems.test.ts
```

#### Testing the New Attachment Tools
The following attachment tools have been added and can be tested:

1. **`wit_get_attachments`** - List all attachments for a work item
2. **`wit_download_work_item_attachments`** - Download all attachments to Downloads folder  
3. **`wit_upload_attachment_from_path`** - Upload a file as an attachment
4. **`wit_delete_attachment`** - Delete an attachment by ID or URL fragment

**Example Usage:**
After starting the MCP server and connecting to it via Copilot Chat, you can test with prompts like:

- "List attachments for work item 123 in project MyProject"
- "Download all attachments from work item 456"
- "Upload the file /path/to/document.pdf to work item 789 with comment 'Technical specification'"
- "Delete attachment with ID abc123-def456 from work item 321"

**Manual Testing Script:**
A test script is available at `/scripts/test-attachments.js` that can be run independently to test the attachment functionality:

```sh
node scripts/test-attachments.js
```

Note: Make sure you have:
- Valid Azure DevOps access configured via `az login`
- A real work item ID and project name for testing
- Appropriate file paths for upload testing

#### Test Coverage
The attachment tools have comprehensive test coverage including:
- Successful operations for all CRUD attachment operations
- Error handling for missing files, API failures, and invalid parameters
- Edge cases like work items with no attachments
- Proper validation of required parameters

---

### 9. Troubleshooting
- If you encounter issues, see `docs/TROUBLESHOOTING.md` for help.
- Ensure you have built the project (`npm run build`) before running the server.
- The entry point for the server is `dist/index.js` (created after building).

---

### References
- [README.md](./README.md)
- [docs/GETTINGSTARTED.md](./docs/GETTINGSTARTED.md)
- [docs/TROUBLESHOOTING.md](./docs/TROUBLESHOOTING.md)

---

_This file was generated to help you run and test the Azure DevOps MCP Server locally._
