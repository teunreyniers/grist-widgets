# Grist Custom Widgets

Custom widgets for Grist spreadsheets.

## URL Filter Widget

A custom widget that reads query parameters from the URL and applies them as filters to the Grist page.

### Features

- ✅ Reads query parameters from the URL
- ✅ Applies filters to the Grist table automatically
- ✅ Displays active filters in a user-friendly interface
- ✅ Supports multiple simultaneous filters
- ✅ Works with any column names

### Usage

1. **Add the widget to your Grist document:**
   - Open your Grist document
   - Add a new Custom Widget section
   - Set the widget URL to where you're hosting `url-filter-widget.html`
   - Grant the widget "Read table" access

2. **Apply filters via URL:**
   Add query parameters to your Grist document URL:
   ```
   ?columnName=value&anotherColumn=value2
   ```

3. **Example:**
   ```
   ?Status=Active&Priority=High&Department=Sales
   ```
   This will filter the table to show only rows where:
   - Status column equals "Active"
   - Priority column equals "High"
   - Department column equals "Sales"

### Hosting Options

#### Option 1: GitHub Pages (Recommended)
1. Push this repository to GitHub
2. Enable GitHub Pages in repository settings
3. Use the GitHub Pages URL in your Grist widget

#### Option 2: Local Development
1. Serve the file locally:
   ```bash
   python3 -m http.server 8000
   ```
2. Use `http://localhost:8000/url-filter-widget.html` in Grist
   (Note: This only works for local Grist instances)

#### Option 3: Any Static Hosting
Upload `url-filter-widget.html` to any static hosting service (Netlify, Vercel, etc.)

### Technical Details

- Uses the [Grist Custom Widget API](https://support.getgrist.com/widget-custom/)
- Filters are applied using the `grist.setOptions()` method
- Query parameters are parsed using the Web URL API
- No external dependencies beyond the Grist plugin API

### Filter Syntax

- Column names are case-sensitive
- Values are matched as strings
- Multiple filters are combined with AND logic
- Reserved parameters (starting with `_`, `access`, `doc`) are ignored

### Troubleshooting

**Filters not working:**
- Ensure column names in the URL match exactly (case-sensitive)
- Check that the widget has "Read table" access
- Open browser console to see error messages

**Widget not loading:**
- Check that the hosting URL is accessible
- Ensure HTTPS is used for hosted Grist instances
- Verify the Grist plugin API script is loading

### License

MIT
