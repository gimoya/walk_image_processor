# Walk Image Processor

## Usage Examples

### Basic Usage
```bash
# Generate markdown documentation
wip -t "Meine Wanderung" -l "Alpenregion" -c

# Generate with custom output file
wip -t "Meine Wanderung" -l "Alpenregion"

# Generate with compression
wip -c -t "Wanderung"

# Generate with compression and quality settings
wip -c -m 1.5 -q 90 -t "Wanderung"
```

### Advanced Usage
```bash
# Custom template and output
wip -T scientific -t "Forschungswanderung" -l "Nationalpark" -o "bericht.md"

# Compression with custom settings
wip -c -m 1.5 -q 95 -t "Qualitätswanderung"

# Browser print workflow
wip -t "Meine Wanderung" -l "Alpen"
# ... edit the markdown file ...
# ... preview formatting by opening walk_documentation.html in browser ...
# ... use browser Print (Ctrl+P) → Save as PDF ...
```

### Command Line Options
- `-t, --title`: Document title
- `-l, --location`: Location/area name  
- `-d, --date`: Date (DD-MM-YYYY format)
- `-o, --output`: Output markdown file
- `-T, --template`: Template format or custom file
- `--top-sheet`: Custom top sheet HTML file (default: htmlsheets/top_sheet.html)
- `-c, --compress`: Enable image compression
- `-m, --max-size`: Maximum image size in MB
- `-q, --quality`: JPEG quality (1-100)
- `--dry-run`: Test run without creating files

## **How Max Size Works:**

### **Default Behavior:**
- **Default value**: 2.0 MB
- **Range**: 0.5 - 10.0 MB
- **Only active when**: `-c` (compress) flag is used

### **What Happens:**
1. **Without `-c`**: Max size is ignored, no compression occurs
2. **With `-c`**: Images larger than the specified size get compressed

### **Example Workflow:**
```bash
# Image is 5.2 MB, max size set to 2.0 MB
wip -c -m 2.0

# Result: Image gets compressed to ≤2.0 MB
# Process: Starts with quality 95, reduces quality until target size reached
```

### **Compression Logic:**
```python
<code_block_to_apply_changes_from>
```

### **Real Example:**
```bash
# Image: 8.7 MB
wip -c -m 1.5

# Output:
# BACKUP created: image.jpg.backup
# COMPRESSED image.jpg: 8.7MB → 1.4MB (84% reduction, auto-quality: 45)
```

## **Complete Workflow:**

### **Step-by-Step Process:**
1. **Generate**: `wip` creates both `.md` and `.html` files
2. **Edit**: Manually edit the `.md` file (text, structure, etc.)
3. **Preview**: Open `.html` file in browser to check formatting
4. **Print**: Use browser's Print function (Ctrl+P) to save as PDF

### **Files Created:**
- `walk_documentation.md` - For manual editing
- `walk_documentation.html` - For previewing and printing
- `walk_documentation.pdf` - Generated via browser Print → Save as PDF

### **Print Instructions:**
1. Open `walk_documentation.html` in your browser
2. Press `Ctrl+P` (or Cmd+P on Mac)
3. Choose "Save as PDF" as destination
4. Set margins to "Minimum" or "None" for best results
5. Click "Save"

**Key Point**: The `-m` flag only works when combined with `-c` (compress). It's the target size for compression, not a file size limit.