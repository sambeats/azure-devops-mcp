# MODIFICATIONS.md

## 2025-08-12

### Added Work Item Attachment Tools
- Added four new tools to the MCP server in `src/tools/workitems.ts`:
  - `wit_get_attachments`: List all attachments for a work item.
  - `wit_download_work_item_attachments`: Download all attachments for a work item to the user's Downloads folder.
  - `wit_upload_attachment_from_path`: Upload an attachment to a work item from a file path.
  - `wit_delete_attachment`: Delete an attachment from a work item by ID or URL fragment.
- Registered these tools in the `WORKITEM_TOOLS` object and implemented their handlers in `configureWorkItemTools`.
- Used Azure DevOps Node SDK for all operations, matching the logic from the provided FastAPI reference.
- Fixed parameter order and types for `updateWorkItem` and `createAttachment` to match SDK signatures.

### Next Steps
- Add/extend tests for these tools in `test/src/tools/workitems.test.ts` (not yet implemented in this commit).
- Validate the new tools in your environment.

---

_This file logs all changes made for the work item attachment tool additions._
