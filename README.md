# Grist URL Filtering for Shared Links

Share filtered views of your Grist data with guests using URL parameters.

## Recommended: Grist Link Keys (No Widget Needed)

Grist has built-in support for URL-based filtering using **Link Keys**:

### Step 1: Create a Shareable Link
Add parameters to your Grist URL:
```
https://your-grist.com/docId/DocName?LinkKey_Status=Active&LinkKey_User=john
```

### Step 2: Access Link Keys in Formulas
In any Grist formula, access the URL parameter:
```python
user.LinkKey.Status    # Returns "Active"
user.LinkKey.User      # Returns "john"
```

### Step 3: Filter with Access Rules
Go to **Document Settings → Access Rules** and add a rule:

| Table | Condition | Permission |
|-------|-----------|------------|
| YourTable | `user.LinkKey.Status == $Status` | Allow Read |
| YourTable | `user.LinkKey.User == $AssignedTo` | Allow Read |

Or for a default "deny all unmatched":
```python
# In Access Rules for table:
rec.Status == user.LinkKey.Status
```

### Step 4: Enable Guest Access
1. Click **Share** → **Manage Users**
2. Enable **Public Access** → set to "Viewer"
3. Now anyone with the link + parameters sees only their filtered data

### Example URLs
```
# Show only "Active" items:
https://docs.getgrist.com/abc123/MyDoc?LinkKey_Status=Active

# Show items for specific user:
https://docs.getgrist.com/abc123/MyDoc?LinkKey_AssignedTo=alice@example.com

# Multiple filters:
https://docs.getgrist.com/abc123/MyDoc?LinkKey_Status=Open&LinkKey_Priority=High
```

---

## Alternative: Filter Helper Widget

If you need more complex filtering logic or want a UI, use the included widget.

### Setup
1. Host `url-filter-widget.html` (GitHub Pages, etc.)
2. Add as Custom Widget in Grist
3. The widget reads `LinkKey_*` parameters and displays active filters

### Files
- `url-filter-widget.html` - Filter display widget
- `README.md` - This documentation

---

## Quick Start Checklist

- [ ] Add `?LinkKey_YourFilter=value` to your Grist URL
- [ ] Create Access Rule using `user.LinkKey.YourFilter`
- [ ] Enable Public/Guest access
- [ ] Share the parameterized URL

## Security Notes

- Link Keys are visible in the URL - don't use for sensitive auth
- Access Rules enforce server-side filtering (secure)
- Guests only see data matching their Link Key values
- Different links = different filtered views of same document
