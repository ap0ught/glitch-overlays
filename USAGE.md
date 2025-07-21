# Usage Guide for Glitch Overlays

This guide provides practical examples for using Glitch overlay assets in modern projects, from simple web animations to full game development.

## 🚀 Quick Start Examples

### Playing SWF Files in Modern Browsers

#### Using Ruffle (Recommended)
```html
<!DOCTYPE html>
<html>
<head>
    <script src="https://unpkg.com/@ruffle-rs/ruffle"></script>
</head>
<body>
    <embed src="rainbow_goodjob.swf" width="200" height="150">
    <!-- Ruffle will automatically handle the Flash file -->
</body>
</html>
```

#### Programmatic Control
```javascript
import { RufflePlayer } from '@ruffle-rs/ruffle';

// Create overlay player
const overlay = RufflePlayer.newest();
overlay.src = './overlays/rainbow_superharvest.swf';
overlay.style.position = 'absolute';
overlay.style.top = '50px';
overlay.style.left = '100px';

// Add to page
document.getElementById('game-area').appendChild(overlay);

// Control playback
overlay.addEventListener('loadeddata', () => {
    overlay.play();
});
```

## 🎨 Converting Overlays to Modern Formats

### CSS Animations (Simple Effects)

#### Rainbow Celebration Effect
```css
/* Recreating rainbow_goodjob.swf as CSS */
.rainbow-celebration {
    position: absolute;
    width: 200px;
    height: 150px;
    background: linear-gradient(45deg, 
        #ff0000, #ff8000, #ffff00, #80ff00, 
        #00ff00, #00ff80, #00ffff, #0080ff, 
        #0000ff, #8000ff, #ff00ff, #ff0080);
    background-size: 400% 400%;
    animation: rainbow-shimmer 2s ease-in-out, fade-in-scale 1.5s ease-out;
    border-radius: 10px;
    opacity: 0;
}

@keyframes rainbow-shimmer {
    0%, 100% { background-position: 0% 50%; }
    50% { background-position: 100% 50%; }
}

@keyframes fade-in-scale {
    0% { 
        opacity: 0; 
        transform: scale(0.5) rotate(-10deg); 
    }
    50% { 
        opacity: 1; 
        transform: scale(1.2) rotate(5deg); 
    }
    100% { 
        opacity: 1; 
        transform: scale(1) rotate(0deg); 
    }
}
```

#### Letter Overlay System (A-Z)
```css
/* Base letter overlay styling */
.letter-overlay {
    position: absolute;
    font-family: 'Comic Sans MS', cursive;
    font-size: 48px;
    font-weight: bold;
    color: #ffffff;
    text-shadow: 2px 2px 0px #000000;
    animation: letter-pop 0.8s ease-out;
    z-index: 1000;
}

@keyframes letter-pop {
    0% { 
        transform: scale(0) rotate(180deg); 
        opacity: 0; 
    }
    50% { 
        transform: scale(1.3) rotate(10deg); 
        opacity: 1; 
    }
    100% { 
        transform: scale(1) rotate(0deg); 
        opacity: 1; 
    }
}

/* Usage in JavaScript */
function showLetter(letter, x, y) {
    const overlay = document.createElement('div');
    overlay.className = 'letter-overlay';
    overlay.textContent = letter.toUpperCase();
    overlay.style.left = x + 'px';
    overlay.style.top = y + 'px';
    
    document.body.appendChild(overlay);
    
    // Remove after animation
    setTimeout(() => overlay.remove(), 2000);
}
```

### Canvas/JavaScript (Complex Animations)

#### Rook Attack Effect
```javascript
class RookAttackOverlay {
    constructor(canvas) {
        this.canvas = canvas;
        this.ctx = canvas.getContext('2d');
        this.particles = [];
        this.animationFrame = 0;
        this.isPlaying = false;
    }
    
    start() {
        this.isPlaying = true;
        this.createParticles();
        this.animate();
    }
    
    createParticles() {
        // Create swirling feather particles like the original
        for (let i = 0; i < 20; i++) {
            this.particles.push({
                x: this.canvas.width / 2,
                y: this.canvas.height / 2,
                vx: (Math.random() - 0.5) * 10,
                vy: (Math.random() - 0.5) * 10,
                rotation: Math.random() * Math.PI * 2,
                scale: 0.5 + Math.random() * 0.5,
                life: 60 + Math.random() * 40
            });
        }
    }
    
    animate() {
        if (!this.isPlaying) return;
        
        this.ctx.clearRect(0, 0, this.canvas.width, this.canvas.height);
        
        // Draw dark energy effect
        this.ctx.fillStyle = 'rgba(0, 0, 20, 0.7)';
        this.ctx.fillRect(0, 0, this.canvas.width, this.canvas.height);
        
        // Update and draw particles
        this.particles.forEach((particle, index) => {
            particle.x += particle.vx;
            particle.y += particle.vy;
            particle.rotation += 0.1;
            particle.life--;
            
            if (particle.life <= 0) {
                this.particles.splice(index, 1);
                return;
            }
            
            // Draw feather-like particle
            this.ctx.save();
            this.ctx.translate(particle.x, particle.y);
            this.ctx.rotate(particle.rotation);
            this.ctx.scale(particle.scale, particle.scale);
            
            this.ctx.fillStyle = `rgba(100, 100, 100, ${particle.life / 100})`;
            this.ctx.fillRect(-5, -15, 10, 30);
            
            this.ctx.restore();
        });
        
        // Continue animation or stop
        if (this.particles.length > 0) {
            requestAnimationFrame(() => this.animate());
        } else {
            this.isPlaying = false;
        }
    }
}

// Usage
const canvas = document.getElementById('game-canvas');
const rookAttack = new RookAttackOverlay(canvas);
rookAttack.start();
```

## 🎮 Game Development Integration

### Unity Integration

#### SWF to Unity Sprite Animation
```csharp
// C# script for Unity
using UnityEngine;

public class GlitchOverlayPlayer : MonoBehaviour 
{
    [SerializeField] private Sprite[] rainbowFrames;
    [SerializeField] private float frameDuration = 0.083f; // ~12fps
    
    private SpriteRenderer spriteRenderer;
    private int currentFrame = 0;
    private float timer = 0f;
    private bool isPlaying = false;
    
    void Start() 
    {
        spriteRenderer = GetComponent<SpriteRenderer>();
    }
    
    void Update() 
    {
        if (!isPlaying || rainbowFrames.Length == 0) return;
        
        timer += Time.deltaTime;
        
        if (timer >= frameDuration) 
        {
            currentFrame = (currentFrame + 1) % rainbowFrames.Length;
            spriteRenderer.sprite = rainbowFrames[currentFrame];
            timer = 0f;
            
            // Stop after one complete loop
            if (currentFrame == 0 && timer == 0f) 
            {
                isPlaying = false;
            }
        }
    }
    
    public void PlayOverlay() 
    {
        currentFrame = 0;
        timer = 0f;
        isPlaying = true;
    }
}
```

### React Component Integration

#### Overlay Component System
```jsx
import React, { useState, useEffect } from 'react';
import './GlitchOverlay.css';

const GlitchOverlay = ({ 
    type = 'rainbow', 
    trigger = false, 
    onComplete = () => {} 
}) => {
    const [isVisible, setIsVisible] = useState(false);
    const [animationClass, setAnimationClass] = useState('');
    
    useEffect(() => {
        if (trigger) {
            setIsVisible(true);
            setAnimationClass(`overlay-${type}`);
            
            // Auto-hide after animation
            const timer = setTimeout(() => {
                setIsVisible(false);
                setAnimationClass('');
                onComplete();
            }, 2000);
            
            return () => clearTimeout(timer);
        }
    }, [trigger, type, onComplete]);
    
    if (!isVisible) return null;
    
    return (
        <div className={`glitch-overlay ${animationClass}`}>
            {type === 'rainbow' && <RainbowEffect />}
            {type === 'letter' && <LetterEffect />}
            {type === 'fireworks' && <FireworksEffect />}
        </div>
    );
};

const RainbowEffect = () => (
    <div className="rainbow-container">
        <div className="rainbow-text">Good Job!</div>
        <div className="rainbow-bg"></div>
    </div>
);

// Usage in game component
const GameArea = () => {
    const [showCelebration, setShowCelebration] = useState(false);
    
    const handlePlayerSuccess = () => {
        setShowCelebration(true);
    };
    
    return (
        <div className="game-area">
            {/* Game content */}
            <GlitchOverlay 
                type="rainbow" 
                trigger={showCelebration}
                onComplete={() => setShowCelebration(false)}
            />
        </div>
    );
};

export default GameArea;
```

## 🔄 Batch Conversion Scripts

### Node.js SWF to GIF Converter
```javascript
const fs = require('fs');
const path = require('path');
const { exec } = require('child_process');

class OverlayConverter {
    constructor(inputDir, outputDir) {
        this.inputDir = inputDir;
        this.outputDir = outputDir;
    }
    
    async convertAll() {
        const swfFiles = fs.readdirSync(this.inputDir)
            .filter(file => file.endsWith('.swf'));
        
        console.log(`Found ${swfFiles.length} SWF files to convert`);
        
        for (const file of swfFiles) {
            await this.convertSWFToGIF(file);
        }
    }
    
    convertSWFToGIF(filename) {
        return new Promise((resolve, reject) => {
            const inputPath = path.join(this.inputDir, filename);
            const outputPath = path.join(this.outputDir, 
                filename.replace('.swf', '.gif'));
            
            // Using ffmpeg to convert (requires ffmpeg with swf support)
            const command = `ffmpeg -i "${inputPath}" -pix_fmt rgb24 "${outputPath}"`;
            
            exec(command, (error, stdout, stderr) => {
                if (error) {
                    console.error(`Error converting ${filename}:`, error);
                    reject(error);
                } else {
                    console.log(`Converted: ${filename} → ${path.basename(outputPath)}`);
                    resolve();
                }
            });
        });
    }
}

// Usage
const converter = new OverlayConverter('./overlays', './converted');
converter.convertAll();
```

### Python Flash Asset Extractor
```python
import os
import zipfile
from xml.etree import ElementTree as ET

class FLAAnalyzer:
    def __init__(self, directory):
        self.directory = directory
        self.analysis = {}
    
    def analyze_all_files(self):
        """Analyze all .fla files in the directory"""
        for filename in os.listdir(self.directory):
            if filename.endswith('.fla'):
                self.analyze_fla(filename)
        return self.analysis
    
    def analyze_fla(self, filename):
        """Extract metadata from a .fla file"""
        filepath = os.path.join(self.directory, filename)
        
        try:
            # .fla files are ZIP archives
            with zipfile.ZipFile(filepath, 'r') as archive:
                # Look for the main document XML
                if 'DOMDocument.xml' in archive.namelist():
                    xml_content = archive.read('DOMDocument.xml')
                    root = ET.fromstring(xml_content)
                    
                    self.analysis[filename] = {
                        'width': root.get('width', 'unknown'),
                        'height': root.get('height', 'unknown'),
                        'frameRate': root.get('frameRate', 'unknown'),
                        'backgroundColor': root.get('backgroundColor', 'unknown'),
                        'symbols': self.count_symbols(archive),
                        'has_actionscript': self.has_actionscript(archive)
                    }
                    
        except Exception as e:
            print(f"Error analyzing {filename}: {e}")
            self.analysis[filename] = {'error': str(e)}
    
    def count_symbols(self, archive):
        """Count symbols in the library"""
        library_path = 'LIBRARY/'
        symbols = [name for name in archive.namelist() 
                  if name.startswith(library_path) and name.endswith('.xml')]
        return len(symbols)
    
    def has_actionscript(self, archive):
        """Check if file contains ActionScript"""
        as_files = [name for name in archive.namelist() 
                   if name.endswith('.as')]
        return len(as_files) > 0
    
    def generate_report(self):
        """Generate a markdown report of all files"""
        report = "# Flash File Analysis Report\n\n"
        
        for filename, data in self.analysis.items():
            if 'error' in data:
                report += f"## {filename}\n**Error**: {data['error']}\n\n"
            else:
                report += f"## {filename}\n"
                report += f"- **Dimensions**: {data['width']} x {data['height']}\n"
                report += f"- **Frame Rate**: {data['frameRate']} fps\n"
                report += f"- **Background**: {data['backgroundColor']}\n"
                report += f"- **Symbols**: {data['symbols']}\n"
                report += f"- **ActionScript**: {'Yes' if data['has_actionscript'] else 'No'}\n\n"
        
        return report

# Usage
analyzer = FLAAnalyzer('./overlays')
analysis = analyzer.analyze_all_files()
report = analyzer.generate_report()

with open('flash_analysis_report.md', 'w') as f:
    f.write(report)
```

## 🎓 Educational Applications

### Biology Teaching with Cell Overlays
```html
<!DOCTYPE html>
<html>
<head>
    <title>Cell Biology Interactive</title>
    <style>
        .cell-diagram { position: relative; width: 600px; height: 400px; }
        .organelle { position: absolute; cursor: pointer; }
        .info-panel { background: rgba(255,255,255,0.9); padding: 10px; }
    </style>
</head>
<body>
    <div class="cell-diagram">
        <img src="cell_background.jpg" alt="Cell diagram">
        
        <!-- Interactive organelle overlays -->
        <div class="organelle" data-overlay="endoplasmic_reticulum.swf" 
             style="left: 100px; top: 150px;">
            <button onclick="showOrganelle('endoplasmic_reticulum')">
                Endoplasmic Reticulum
            </button>
        </div>
        
        <div class="organelle" data-overlay="golgi_apparatus.swf"
             style="left: 250px; top: 100px;">
            <button onclick="showOrganelle('golgi_apparatus')">
                Golgi Apparatus
            </button>
        </div>
        
        <div class="organelle" data-overlay="vacuoles.swf"
             style="left: 400px; top: 200px;">
            <button onclick="showOrganelle('vacuoles')">
                Vacuoles
            </button>
        </div>
    </div>
    
    <div id="overlay-player"></div>
    <div id="info-panel" class="info-panel"></div>
    
    <script>
        const organelleInfo = {
            'endoplasmic_reticulum': {
                name: 'Endoplasmic Reticulum',
                description: 'A network of membranes that transports materials throughout the cell.',
                animation: 'endoplasmic_reticulum.swf'
            },
            'golgi_apparatus': {
                name: 'Golgi Apparatus', 
                description: 'Processes and packages proteins from the ER.',
                animation: 'golgi_apparatus.swf'
            },
            'vacuoles': {
                name: 'Vacuoles',
                description: 'Storage compartments for water, waste, and nutrients.',
                animation: 'vacuoles.swf'
            }
        };
        
        function showOrganelle(type) {
            const info = organelleInfo[type];
            
            // Update info panel
            document.getElementById('info-panel').innerHTML = `
                <h3>${info.name}</h3>
                <p>${info.description}</p>
            `;
            
            // Play animation
            const player = document.createElement('embed');
            player.src = `./biological_overlays/${info.animation}`;
            player.width = 300;
            player.height = 200;
            
            const container = document.getElementById('overlay-player');
            container.innerHTML = '';
            container.appendChild(player);
        }
    </script>
</body>
</html>
```

### Spelling Game with Letter Overlays
```javascript
class SpellingGame {
    constructor(words) {
        this.words = words;
        this.currentWord = '';
        this.currentIndex = 0;
        this.score = 0;
    }
    
    startGame() {
        this.currentWord = this.words[Math.floor(Math.random() * this.words.length)];
        this.currentIndex = 0;
        this.displayWord();
    }
    
    displayWord() {
        const container = document.getElementById('game-area');
        container.innerHTML = '';
        
        // Create letter placeholders
        for (let i = 0; i < this.currentWord.length; i++) {
            const letterSlot = document.createElement('div');
            letterSlot.className = 'letter-slot';
            letterSlot.id = `slot-${i}`;
            container.appendChild(letterSlot);
        }
    }
    
    onKeyPress(letter) {
        if (this.currentIndex >= this.currentWord.length) return;
        
        const expectedLetter = this.currentWord[this.currentIndex].toLowerCase();
        
        if (letter.toLowerCase() === expectedLetter) {
            // Show correct letter overlay
            this.showLetterOverlay(letter.toUpperCase(), `slot-${this.currentIndex}`);
            this.currentIndex++;
            
            if (this.currentIndex === this.currentWord.length) {
                // Word complete! Show celebration
                setTimeout(() => this.showCelebration(), 500);
            }
        } else {
            // Show error feedback
            this.showErrorFeedback();
        }
    }
    
    showLetterOverlay(letter, slotId) {
        // Use the original Glitch letter overlay system
        const slot = document.getElementById(slotId);
        const overlay = document.createElement('div');
        overlay.className = 'letter-overlay-animation';
        overlay.textContent = letter;
        
        slot.appendChild(overlay);
        
        // Trigger animation (CSS or JS)
        overlay.style.animation = 'letter-appear 0.8s ease-out';
    }
    
    showCelebration() {
        // Show rainbow celebration like in original Glitch
        const celebration = document.createElement('embed');
        celebration.src = 'rainbow_goodjob.swf';
        celebration.className = 'celebration-overlay';
        document.body.appendChild(celebration);
        
        setTimeout(() => celebration.remove(), 3000);
        this.score++;
        this.startGame(); // Next word
    }
}

// Initialize game
const game = new SpellingGame(['GLITCH', 'OVERLAY', 'RAINBOW', 'MAGIC']);
document.addEventListener('keypress', (e) => {
    game.onKeyPress(e.key);
});
```

## 🔍 Performance Optimization

### Efficient Overlay Management
```javascript
class OverlayManager {
    constructor() {
        this.activeOverlays = new Map();
        this.overlayPool = new Map();
        this.maxPoolSize = 10;
    }
    
    // Object pooling for better performance
    getOverlay(type) {
        if (this.overlayPool.has(type) && this.overlayPool.get(type).length > 0) {
            return this.overlayPool.get(type).pop();
        }
        return this.createOverlay(type);
    }
    
    returnOverlay(type, overlay) {
        overlay.reset(); // Reset to initial state
        
        if (!this.overlayPool.has(type)) {
            this.overlayPool.set(type, []);
        }
        
        const pool = this.overlayPool.get(type);
        if (pool.length < this.maxPoolSize) {
            pool.push(overlay);
        }
    }
    
    // Batch operations for multiple overlays
    showCelebrationSequence(achievements) {
        const delays = [0, 500, 1000, 1500]; // Staggered timing
        
        achievements.forEach((achievement, index) => {
            setTimeout(() => {
                const overlay = this.getOverlay('rainbow');
                overlay.show(achievement);
                
                overlay.onComplete(() => {
                    this.returnOverlay('rainbow', overlay);
                });
            }, delays[index] || index * 500);
        });
    }
}
```

## 🛠️ Debugging and Testing

### Overlay Testing Framework
```javascript
class OverlayTester {
    constructor() {
        this.testResults = [];
    }
    
    async testAllOverlays() {
        const overlayFiles = await this.getOverlayList();
        
        for (const file of overlayFiles) {
            const result = await this.testOverlay(file);
            this.testResults.push(result);
        }
        
        return this.generateReport();
    }
    
    async testOverlay(filename) {
        const startTime = performance.now();
        
        try {
            // Test loading
            const loadSuccess = await this.testLoad(filename);
            
            // Test playback
            const playbackSuccess = await this.testPlayback(filename);
            
            // Test performance
            const performanceMetrics = await this.testPerformance(filename);
            
            const endTime = performance.now();
            
            return {
                filename,
                success: loadSuccess && playbackSuccess,
                loadTime: endTime - startTime,
                metrics: performanceMetrics,
                errors: []
            };
            
        } catch (error) {
            return {
                filename,
                success: false,
                error: error.message,
                loadTime: performance.now() - startTime
            };
        }
    }
    
    generateReport() {
        const successful = this.testResults.filter(r => r.success).length;
        const total = this.testResults.length;
        
        return {
            summary: `${successful}/${total} overlays working correctly`,
            details: this.testResults,
            recommendations: this.generateRecommendations()
        };
    }
}
```

---

This usage guide provides practical starting points for working with Glitch overlays in modern development contexts. Each example can be adapted for specific needs, and the conversion techniques can be applied to preserve and modernize these historical game assets.