# Contributing to Glitch Overlays

Thank you for your interest in contributing to the preservation and documentation of Glitch overlays! This project welcomes contributions that help others understand, use, and preserve these historical game assets.

## 🎯 Types of Contributions Welcome

### Documentation Improvements
- **Usage examples** - How to implement overlays in modern projects
- **Technical guides** - Converting .fla/.swf files to modern formats
- **Historical context** - Game mechanics and original implementation details
- **Categorization** - Better organization of the 211+ overlay files
- **Tutorial content** - Step-by-step guides for specific use cases

### Code Examples
- **Conversion scripts** - Tools to convert Flash files to modern formats
- **Implementation examples** - Using overlays in React, Vue, Unity, etc.
- **Integration helpers** - Libraries or utilities for working with these assets
- **Modern recreations** - CSS/JS versions of popular overlays

### Asset Analysis
- **File documentation** - Detailed descriptions of what each overlay does
- **Dependency mapping** - Which overlays work together
- **Quality assessments** - Condition and usability of different files
- **Missing asset identification** - Gaps in the collection

## 🛠️ Working with Flash Files

### Development Environment Setup

#### For .fla Source Files
1. **Adobe Animate** (recommended) or **Adobe Flash Professional**
   - Latest version preferred for better compatibility
   - Can export to modern formats (HTML5 Canvas, WebGL, etc.)

2. **OpenFL** (open-source alternative)
   ```bash
   haxelib install openfl
   haxelib install lime
   openfl create DisplayingABitmap
   ```

3. **Adobe Flash Builder** (for ActionScript editing)

#### For .swf Compiled Files
1. **Ruffle** (open-source Flash Player)
   ```bash
   # Web version
   npm install @ruffle-rs/ruffle
   
   # Desktop version
   # Download from https://ruffle.rs/
   ```

2. **JPEXS Free Flash Decompiler**
   - Extract assets, scripts, and animations
   - Convert to various formats
   - Download from https://github.com/jindrapetrik/jpexs-decompiler

3. **Adobe Flash Player** (legacy, security concerns)

### File Structure Analysis

#### .fla Files (Flash Source)
```
overlay_name.fla
├── Library/           # Symbols, graphics, sounds
├── Scene 1/          # Main timeline
├── ActionScript/     # Code (if any)
└── Properties/       # Document settings
```

#### Common Elements to Document
- **Frame rate** - Usually 12 or 24 fps
- **Dimensions** - Pixel size and aspect ratio  
- **Color mode** - RGB vs indexed color
- **ActionScript version** - AS2 vs AS3
- **External dependencies** - Shared libraries or classes

## 📝 Documentation Standards

### File Documentation Template
When documenting an overlay, include:

```markdown
## overlay_name.fla

**Category**: [UI/Effects/Characters/etc.]
**Dimensions**: [width x height px]  
**Duration**: [seconds or "static"]
**Frame Rate**: [fps]
**Dependencies**: [list any required files]

### Description
[What this overlay does in the game]

### Technical Details
- ActionScript Version: [AS2/AS3/None]
- Transparency: [Yes/No]
- Audio: [Yes/No]
- Looping: [Yes/No]

### Modern Usage Examples
[How to use this in contemporary projects]

### Conversion Notes
[Specific challenges or tips for converting this file]
```

### Code Example Standards
```javascript
// Always include context and complete examples
// Bad:
overlay.play();

// Good:
// Using Ruffle to display a Glitch overlay in modern web app
import { RufflePlayer } from '@ruffle-rs/ruffle';

const player = RufflePlayer.newest();
player.src = './overlays/rainbow_goodjob.swf';
player.width = 200;
player.height = 150;
document.getElementById('overlay-container').appendChild(player);
```

## 🔄 Modern Conversion Guidelines

### Converting to Web Technologies

#### CSS Animations
For simple effects:
```css
.glitch-rainbow {
  animation: rainbow-fade 2s ease-in-out;
  /* Recreate the original timing and easing */
}

@keyframes rainbow-fade {
  0% { opacity: 0; transform: scale(0.8); }
  50% { opacity: 1; transform: scale(1.1); }
  100% { opacity: 1; transform: scale(1.0); }
}
```

#### JavaScript/Canvas
For complex animations:
```javascript
class GlitchOverlay {
  constructor(canvasId) {
    this.canvas = document.getElementById(canvasId);
    this.ctx = this.canvas.getContext('2d');
    // Load sprite sheets from converted Flash assets
  }
  
  render() {
    // Implement the overlay animation logic
  }
}
```

#### Framework Integration
Document patterns for popular frameworks:
- React/Vue component examples
- Unity/Godot import processes  
- CSS-in-JS implementations

### Quality Standards
- **Performance**: Maintain 60fps when possible
- **Accessibility**: Add alt text and reduce motion options
- **Responsiveness**: Scale appropriately for different screen sizes
- **Browser Support**: Test across modern browsers

## 📋 Contribution Process

### 1. Planning
- **Check existing issues** to avoid duplicate work
- **Open an issue** to discuss major contributions
- **Fork the repository** for your changes

### 2. Development
- **Create descriptive branch names**: `docs/alphabet-overlay-guide`, `convert/rainbow-series-css`
- **Make focused commits** with clear messages
- **Test your examples** thoroughly

### 3. Documentation
- **Update relevant files**: README.md, USAGE.md, FILE_REFERENCE.md
- **Add code comments** explaining complex conversions
- **Include screenshots/demos** for visual changes

### 4. Submission
- **Create a pull request** with detailed description
- **Reference related issues** if applicable
- **Be responsive** to review feedback

## 🧪 Testing Contributions

### Flash File Testing
1. **Open in Adobe Animate** - Verify file loads correctly
2. **Export test** - Try converting to modern format
3. **Document issues** - Note any corruption or problems

### Code Testing  
1. **Cross-browser testing** - Chrome, Firefox, Safari, Edge
2. **Performance testing** - Check memory usage and frame rates
3. **Accessibility testing** - Screen readers and keyboard navigation

### Documentation Testing
1. **Follow your own guides** - Can others reproduce your steps?
2. **Check links** - Ensure all references work
3. **Validate formatting** - Markdown renders correctly

## 🎨 Style Guidelines

### Code Style
- Use **modern JavaScript** (ES6+)
- Follow **consistent indentation** (2 spaces)
- Add **JSDoc comments** for functions
- Use **meaningful variable names**

### Documentation Style
- Write in **clear, accessible language**
- Use **active voice** when possible
- Include **practical examples**
- Keep **paragraphs concise**

### Asset Organization
- Follow **existing naming conventions**
- Group **related files together**  
- Use **descriptive folder structures**
- Maintain **alphabetical ordering** where possible

## 🚀 Getting Started

### Quick Start Checklist
- [ ] Fork the repository
- [ ] Set up Flash development environment OR modern alternative
- [ ] Pick a specific overlay to work with
- [ ] Document your exploration process
- [ ] Share your findings via pull request

### Beginner-Friendly Tasks
1. **File cataloging** - Document what specific overlays do
2. **Screenshot creation** - Visual references for each overlay
3. **Usage examples** - Simple HTML/CSS recreations
4. **Link checking** - Verify all external links work
5. **Typo fixes** - Grammar and spelling improvements

### Advanced Contributions
1. **Conversion tools** - Scripts to automate Flash → modern format
2. **Game engine plugins** - Unity/Godot import helpers
3. **Performance optimization** - Efficient modern implementations
4. **Historical research** - Original game context and mechanics

## 🤝 Community Guidelines

- **Be respectful** - This is a collaborative preservation effort
- **Be patient** - Flash technology has a learning curve
- **Be thorough** - Document your process for others
- **Be creative** - Find new ways to use these assets
- **Be historical** - Preserve the original intent when possible

## 📞 Getting Help

- **Open an issue** for technical questions
- **Check existing documentation** before asking
- **Provide specific details** about your setup and goals
- **Share your attempts** so others can help debug

## 🏆 Recognition

Contributors will be acknowledged in:
- Repository contributor list
- Documentation credits
- Release notes for major contributions

---

Thank you for helping preserve and modernize this important piece of web gaming history! Every contribution, no matter how small, helps keep the spirit of Glitch alive for future developers and creators.