# Copilot Instructions for tpv-landing

## Project Overview
The Prime Visa (TPV) is a multi-page landing website showcasing immigration visa services. The project consists of a main landing site and specialized service pages for Family, Green Card, K1, More Services, and Spousal visas.

## Architecture

### Page Structure
- **Root pages**: `index.htm`, `about.htm`, `family.htm`, `green.htm`, `K1.htm`, `more.htm`, `phresidency.htm`, `spousal.htm`, `privacy.htm`, `terms.htm`
- **Service pages**: Located in `appservices/{service-name}/` directories (family/, green/, k1/, more/, phresidency/, spousal/)
- **Main about page**: Located in `appabout/` directory

### Technology Stack
- **HTML**: Plain HTML5 with semantic structure (no frameworks)
- **SCSS**: Modular architecture with partial imports
- **JavaScript**: Vanilla ES6+ (no frameworks)
- **Styling**: CSS Grid/Flexbox with mobile-first responsive design

## Critical Patterns

### SCSS Organization
Each section has a consistent modular structure:

1. **Core imports** (always first):
   - `_variables.scss` - Colors, typography, spacing (shared across partials)
   - `_mixins.scss` - Reusable style functions
   - `_animations.scss` - Animation definitions

2. **Global/Layout**:
   - `_globals.scss` - Base styles, typography, utility classes
   - `_header.scss` - Navigation and header styles
   - `_footer.scss` - Footer styles

3. **Section-specific** (varies by page):
   - `_hero.scss` - Hero section with banner
   - `_service.scss` - Service cards layout
   - `_community.scss` - Community/testimonials section
   - `_testimonial.scss` - Individual testimonial styling
   - `_schedule.scss` - Schedule/timeline components
   - `_banner.scss`, `_qualify.scss`, `_timeline.scss`, `_cost.scss`, `_care.scss`, `_faqs.scss` - Service-specific sections

**Key convention**: Always import in this order - variables/mixins first, then globals, then features. See [app/scss/style.scss](app/scss/style.scss) and [appservices/family/scss/style.scss](appservices/family/scss/style.scss) for examples.

### JavaScript Patterns
- **DOM manipulation**: Use `querySelector()` / `querySelectorAll()` with specific selectors
- **Event handling**: Direct `addEventListener()` without delegation (appropriate for landing page scale)
- **Data attributes**: Use `data-*` attributes for component logic (e.g., `[data-carousel-button]`, `[data-carousel]`, `[data-slides]`, `[data-active]`)
- **Class toggling**: Manage state with `.classList.add()` / `.remove()` / `.contains()`

Example: Hamburger menu in [app/js/script.js](app/js/script.js) uses `.has-fade`, `.fade-in`, `.fade-out` classes and `.noscroll` on body to prevent scrolling.

### HTML/CSS Classes
- **Utility classes**: `.container`, `.flex`, `.flex-jc-sb` (space-between), `.flex-ai-c` (align-items center)
- **Responsive prefixes**: `.hide-for-desktop`, `.hide-for-mobile`
- **State classes**: `.open`, `.noscroll`, `.fade-in`, `.fade-out`
- **Data-driven components**: Carousel uses `[data-carousel]`, `[data-slides]`, `[data-carousel-button]="next|prev"`

## Developer Workflow

### Building Styles
SCSS compiles to CSS. Files like [style.css](app/scss/style.css) are generated from [style.scss](app/scss/style.scss). When editing styles:
1. Modify the `.scss` partial files
2. Compile/watch SCSS to generate updated `.css`
3. Commit both `.scss` and generated `.css` files

### Adding New Sections
When creating new content sections:
1. Add corresponding `.htm` page at root or in `appservices/{name}/`
2. Create SCSS partial file following naming convention
3. Import partial in the main `style.scss` in correct order
4. Use existing utility classes and variables for consistency
5. Mirror header/footer structure from existing pages

### Image Organization
Images are organized by type in `/images/` and service-specific `/appservices/{service}/images/`:
- `abstract/` - Background/decorative images
- `images/` - Content photography
- `imagesbw/` - Black & white variants
- `logo/`, `logotagline/` - Branding assets
- `social/` - Social media icons
- `FB _ X - Cover Photo/` - Social media templates
- `Service/` - Service-related icons

## Key Files & Conventions
- [style.css](style.css) - Root global styles for navigation/common elements
- [app/scss/](app/scss/) - Main landing page styles
- [appservices/family/scss/](appservices/family/scss/) - Service page template pattern
- Variables are centralized in `_variables.scss` - update here for sitewide changes
- All pages use `<html lang="en">` and `<meta charset="UTF-8">`

## Common Tasks
- **Update branding/colors**: Edit `_variables.scss` in each section
- **Fix responsive layout**: Check `_globals.scss` for breakpoints and utility classes
- **Add animations**: Define in `_animations.scss`, apply via class names in HTML
- **Modify navigation**: Edit [index.htm](index.htm) header structure, styles in [app/scss/_header.scss](app/scss/_header.scss)
- **Carousel changes**: See [app/js/script.js](app/js/script.js) for data-attribute pattern
