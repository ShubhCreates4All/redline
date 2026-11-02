# 02: Upload, browser-parse, save to library

**What to build:** A signed-in user can upload a contract/lease/freelance-agreement/ToS document, have it parsed entirely in their browser, and see the extracted text saved as a new entry in their personal library — with the original file never transmitted or stored.

**Blocked by:** 01

**Status:** ready-for-agent

- [ ] A user can upload a document from the authenticated app
- [ ] The file is parsed client-side in the browser; only the extracted text is sent to the backend
- [ ] The extracted text is persisted as a new library entry scoped to the uploading user
- [ ] The user can see the new entry in a list of their library entries
- [ ] No original file bytes are ever transmitted past the browser or stored anywhere
- [ ] One user cannot see another user's library entries
