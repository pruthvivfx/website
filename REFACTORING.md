# Code Refactoring Documentation

## CSS Refactoring

### Changes Made
The project's CSS code has been refactored to eliminate significant duplication across multiple stylesheet files.

### Before Refactoring
- 7 CSS files with heavily duplicated code
- Each file contained ~109 lines of CSS
- Total: ~763 lines with ~80% duplication
- Common styles (reset, navigation, buttons, positioning) were copy-pasted across all files

### After Refactoring
- Created `css/base.css` with all common styles (115 lines)
- Refactored 7 page-specific CSS files to import base styles
- Each page-specific CSS now contains only unique overrides (~15-27 lines)
- Total: 253 lines (67% reduction)

### Structure
```
css/
├── base.css           # Common base styles (imported by all pages)
├── style.css          # Home page specific overrides
├── style1.css         # AI section specific overrides
├── style-ai2.css      # AI page 2 specific overrides
├── style-blog.css     # Blog page specific overrides
├── style-game.css     # Gaming page specific overrides
├── style-kri.css      # Kritika's page specific overrides
└── style-creditsai.css # Credits page specific overrides
```

### Using the Base Styles
All page-specific CSS files now import the base styles:
```css
/* Import base styles */
@import url('base.css');

/* Page-specific overrides */
header {
    background-image: url(../your-image.jpg);
}
```

### Base Styles Include
- CSS reset (`*` selector)
- Header layout (height, background positioning)
- Navigation styles (ul, li, hover effects)
- Logo styles
- Main container layout
- Title positioning
- Button styles (.btn, .btn1)
- Button container positioning (.button, .button1)

### Page-Specific Overrides
Each page stylesheet now only contains:
- Background image for the header
- Position adjustments for titles and buttons
- Any unique components for that specific page

## Benefits
1. **Maintainability**: Changes to common styles only need to be made once in `base.css`
2. **Consistency**: All pages share the same base styling automatically
3. **Reduced File Size**: 67% reduction in CSS code (510 lines removed)
4. **Easier Updates**: New pages can quickly adopt the standard styling by importing base.css

## HTML Structure Notes
While HTML refactoring was considered, this is a static HTML site without a templating system. The following patterns are duplicated across HTML files and should be maintained consistently:

### Common HTML Pattern
```html
<header>
    <div class="main">
        <div class="logo">
            <img src="a-removebg-preview.png">
        </div>
        <ul>
            <!-- Navigation links -->
        </ul>
    </div>
    <div class="title">
        <p><h1>Marias Public School</h1></p>
    </div>
</header>
```

When creating new pages, copy this structure and:
1. Link to the appropriate stylesheet (`base.css` is automatically imported)
2. Add the `active` class to the current page's navigation item
3. Customize the page-specific content area

## Future Considerations
For further reducing duplication, consider:
1. Converting to a static site generator (Jekyll, Hugo, 11ty)
2. Using HTML template includes
3. Implementing a JavaScript-based component system
4. Using a CSS preprocessor (Sass, Less) for more advanced CSS management
