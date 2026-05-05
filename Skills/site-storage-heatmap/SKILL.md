---
name: "site-storage-heatmap"
description: "Generates an interactive HTML site map showing storage breakdown and hot/cold activity heatmap across all document libraries, lists, and site pages. Includes site-wide summary stacked bars and per-library click-through drill-downs. Saves the file as {FirstName}-Site-Storage-Heatmap.html in the \"storage heatmap\" folder inside the site's document library, then navigates the user to it."
---
# Site Storage Heatmap

Generate an interactive HTML site map with storage sizes and hot/cold activity heatmaps for a SharePoint site, then navigate the user to the output.

## Steps

### 1. Get the Current User's First Name
- Call `get_user_info(query="@currentUser")` to resolve the current user.
- Extract the **first name** from the resolved display name (e.g., "Adam Harmetz" → "Adam").
- The output filename will be: `{FirstName}-Site-Storage-Heatmap.html`

### 2. Discover All Containers
- Call `discover_sharepoint_lists` with `filterType="all"` and `includeHidden=false` to get every list, library, and page library on the site.
- Categorize each container:
  - **Document Libraries**: templateType 101
  - **Lists**: templateType 100
  - **Site Pages**: templateType 119
  - **Calendar**: templateType 106
- Record each container's `id`, `title`, `itemCount`, and `serverRelativeUrl`.

### 3. Collect File-Level Data from Each Non-Empty Library
- For every document library (templateType 101) with itemCount > 0, call `list_items` with:
  - `viewFields: ["FileLeafRef", "File_x0020_Size", "File_x0020_Type", "Modified"]`
  - `itemType: "files"`, `recursive: true`, `rowLimit` set to the library's `itemCount`
- For Site Pages (templateType 119), also query with `viewFields: ["FileLeafRef", "Modified"]` to get page modification dates.
- Parallelize all independent list_items calls.

### 4. Aggregate Per-Library Stats
For each library, compute:
- **Total size** (sum of `File_x0020_Size` in bytes)
- **File count**
- **File type breakdown**: group by `File_x0020_Type` → `{ ext: { count, size } }`
- **Recency buckets** based on `Modified` date relative to today:
  - **Hot**: modified ≤ 7 days ago
  - **Warm**: modified ≤ 30 days ago
  - **Cool**: modified ≤ 90 days ago
  - **Cold**: modified > 90 days ago
- Track both file count AND storage per recency bucket.

For lists (no file sizes), classify each list as hot/warm/cool/cold based on the list's `lastModified` date from the discovery response. Count list items per recency bucket.

### 5. Compute Site-Wide Rollup
Sum across ALL containers (libraries + lists + pages):
- Grand total items (files + list items + pages)
- Total storage (libraries only)
- Aggregate recency: total hot / warm / cool / cold counts
- Separate recency breakdowns for: Document Libraries, Lists, Site Pages

### 6. Generate the Interactive HTML
Build a self-contained HTML file with embedded CSS and JavaScript containing:

#### Root Banner
- Site name, total item count, container count, page count
- "Total Library Storage: X" badge

#### Site-Wide Heatmap Panel (below root, above branches)
- 3-column grid: one for Document Libraries, one for Lists, one for Site Pages
- Each column has a **stacked horizontal bar** (hot=red #E74856, warm=orange #FF8C00, cool=blue #50E6FF, cold=grey #A0AEC0) showing file/item counts per recency tier
- Below each bar: storage per tier (for libraries) or counts (for lists/pages)
- Bottom legend row: grand totals per tier across the entire site

#### 3-Column Site Map (below heatmap)
- **Column 1 (wider)**: Document Libraries — all libraries merged together (including expense libraries), sorted by total size descending. Each leaf card shows: name, size badge, file count badge. Clickable.
- **Column 2**: Lists — each list with item count badge. Not clickable.
- **Column 3**: Site Pages — each page name. Not clickable.
- Empty containers grayed out.

#### Click-Through Modal (JavaScript)
When a library leaf is clicked, show a modal overlay with:
- **Summary cards**: File count, Total size, File type count
- **Activity Heatmap**: 4 horizontal bars (hot/warm/cool/cold) showing file counts + storage per tier
- **Storage by File Type**: horizontal bars per extension showing % of total, file count, and size
- Close on Escape, click outside, or ✕ button

#### Styling
- Use Segoe UI font, #f5f5f5 background
- Branch headers: blue gradient for doc libs, green for lists, purple for pages
- Responsive grid that stacks on mobile
- Hover effects on clickable leaves (translateX + shadow)
- Modal with backdrop blur

### 7. Save the HTML File
- Save as `{FirstName}-Site-Storage-Heatmap.html`
- Target location: the site's document library, inside a folder called **"storage heatmap"**
  - Use `create_text_file` with `relativeFolderPath="storage heatmap"`
  - If the folder doesn't exist, create it first with `create_folder`

### 8. Navigate the User
- After saving, call `navigate_to_url` to take the user to the document library where the file was saved.
- Provide the direct file URL so the user can open it.
- Remind the user: **"Download and open in your browser for full interactivity — SharePoint strips JavaScript from inline HTML previews."**

## Example

**User**: "Generate a storage heatmap for this site"

**Result**: File saved as `Adam-Site-Storage-Heatmap.html` in the "storage heatmap" folder, user navigated to the library, with a note to download for JS interactivity.

## Constraints
- Always get the current user's first name — never hardcode.
- Always get the current date via `get_datetime_info` before computing recency buckets — never assume today's date.
- Parallelize list_items calls for all non-empty libraries to minimize latency.
- Use `execute_code` with `outputDataRef: true` for all large intermediate data.
- Keep the HTML fully self-contained (no external dependencies).
- File type colors: use a rotating palette of Fluent-style colors.
- Recency colors are fixed: hot=#E74856, warm=#FF8C00, cool=#50E6FF, cold=#A0AEC0.
