# Simple Markdown Website

A barebones personal website with zero frameworks - just HTML, CSS, and vanilla JavaScript.

## Structure

```
simple-site/
├── index.html          # Single HTML file with all styling and logic
├── content/            # Your markdown files
│   ├── home.md
│   ├── about.md
│   └── blog.md
└── README.md
```

## How It Works

1. **One HTML file** - Contains all structure, styling, and JavaScript
2. **Markdown files** - Write your content in plain markdown in the `content/` folder
3. **Marked.js** - Loaded from CDN to parse markdown to HTML
4. **Simple routing** - Click navigation links to load different pages

## To Use

### Local Development

Run any simple web server:

```bash
# Python 3
python3 -m http.server 8000

# Python 2
python -m SimpleHTTPServer 8000

# Node.js (if you have npx)
npx serve
```

Then open http://localhost:8000

### Deployment

Upload these files to any static hosting:

- **GitHub Pages** - Free, easy setup
- **Netlify** - Drag and drop the folder
- **Vercel** - Connect your repo or upload
- **Any web host** - Just upload via FTP

No build step required. No dependencies to install.

## Customization

### Add New Pages

1. Create a new `.md` file in `content/` folder (e.g., `projects.md`)
2. Add a link in the nav section of `index.html`:
   ```html
   <li><a href="#" data-page="projects">Projects</a></li>
   ```

### Change Colors

Edit the CSS in the `<style>` tag in `index.html`. Main colors:

- Links: `#0066cc`
- Text: `#333`
- Background: `#fff`
- Code blocks: `#f6f8fa`

### Change Layout

Edit the CSS in `index.html`. The content width is controlled by:
```css
.container {
    max-width: 800px;  /* Change this */
}
```

## Features

- Clean, readable design
- Mobile responsive
- Syntax highlighting for code blocks
- URL-based navigation (back/forward buttons work)
- Fast loading (no frameworks)
- Works offline (once loaded)

## Markdown Support

Supports all standard markdown:

- **Bold** and *italic*
- Headers (h1-h6)
- Links and images
- Code blocks with syntax highlighting
- Lists (ordered and unordered)
- Blockquotes
- And more...

## License

Do whatever you want with this. No attribution required.
