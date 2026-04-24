# Assets Guide - Adding Your Images & Reports

## 📁 Folder Structure

```
public/
├── projects/          # Your project screenshots/images
│   ├── cfd-hull.png
│   ├── fem-structure.png
│   ├── ml-predictor.png
│   └── wave-structure.png
├── reports/           # Your PDF reports and documents
│   ├── cfd-analysis.pdf
│   ├── cfd-validation.pdf
│   ├── fem-analysis.pdf
│   └── ...
└── resume.pdf         # Your CV
```

## 🖼️ Adding Project Images

### Step 1: Prepare Your Images

**Best Practices:**
- **Format:** PNG or JPG
- **Size:** 1200×900px or 800×600px (4:3 ratio works best)
- **Quality:** High resolution but compressed (<500KB per image)
- **Content:** 
  - CFD visualizations (velocity fields, pressure contours, streamlines)
  - FEM stress/strain plots
  - ML training curves and results
  - Diagrams and schematics
  - Screenshots of your analysis software

**Recommended Tools for Screenshots:**
- ANSYS: Use built-in screenshot feature (File → Export → Save Image)
- ParaView/Tecplot: Export views as PNG
- MATLAB/Python plots: `savefig('filename.png', dpi=300, bbox_inches='tight')`
- Design software: Export rendered views

### Step 2: Add Images to `/public/projects/`

1. Place your images in `/public/projects/` folder
2. Name them clearly (e.g., `cfd-hull-analysis.png`)
3. Update `/src/app/components/Projects.tsx`:

```typescript
{
  title: "Your-Project-Name",
  // ... other fields
  image: "/projects/your-image.png",  // ← Update this path
}
```

## 📄 Adding Reports & PDFs

### Step 1: Prepare Your Documents

**What to Include:**
- Research reports
- Technical papers
- Analysis results
- Validation studies
- Presentation slides (exported as PDF)
- Project documentation

**Tips:**
- Keep file sizes reasonable (<10MB per PDF)
- Use descriptive filenames
- Compress PDFs if needed (using Adobe Acrobat or online tools)

### Step 2: Add PDFs to `/public/reports/`

1. Place PDFs in `/public/reports/` folder
2. Update `/src/app/components/Projects.tsx`:

```typescript
{
  title: "Your-Project-Name",
  // ... other fields
  reports: [
    { name: "Display Name.pdf", path: "/reports/actual-filename.pdf" },
    { name: "Another Report.pdf", path: "/reports/another-file.pdf" }
  ]
}
```

## 🎨 Creating Placeholder Images

If you don't have images yet, you can create placeholders:

### Option 1: Use Unsplash (Free Stock Photos)
```typescript
image: "https://images.unsplash.com/photo-1581092918056-0c4c3acd3789?w=800"
```

### Option 2: Take Screenshots
- Screenshot your ANSYS/Abaqus workspace
- Export plots from MATLAB/Python
- Capture your CAD models

### Option 3: Create Simple Diagrams
- Use PowerPoint/Google Slides to create diagrams
- Export as PNG
- Tools: Draw.io, Excalidraw, Figma

## 🔧 Example: Complete Project Entry

```typescript
{
  title: "CFD-Ship-Hull-Analysis",
  description: "Computational fluid dynamics study...",
  tags: ["CFD", "ANSYS-Fluent", "Hydrodynamics"],
  status: "active",
  stars: 12,
  language: "Python",
  
  // Your project image (screenshot, visualization, diagram)
  image: "/projects/cfd-hull-visualization.png",
  
  // Your downloadable reports
  reports: [
    { 
      name: "CFD Analysis Report.pdf", 
      path: "/reports/ship-hull-cfd-report.pdf" 
    },
    { 
      name: "Validation Results.pdf", 
      path: "/reports/hull-validation.pdf" 
    },
    { 
      name: "Presentation Slides.pdf", 
      path: "/reports/hull-presentation.pdf" 
    }
  ]
}
```

## 📊 Quick Examples by Project Type

### CFD Projects
**Images:**
- Velocity field contours
- Pressure distribution plots
- Streamline visualizations
- Wave patterns
- Mesh views

**Reports:**
- CFD analysis methodology
- Grid independence study
- Validation against experiments
- Results and conclusions

### FEM Projects
**Images:**
- Stress/strain contour plots
- Deformation visualizations
- Von Mises stress distribution
- Mesh models
- Load cases

**Reports:**
- Structural analysis report
- Material properties
- Boundary conditions
- Safety factor calculations

### Machine Learning Projects
**Images:**
- Training/validation curves
- Confusion matrices
- Feature importance plots
- Network architecture diagrams
- Performance comparisons

**Reports:**
- Model documentation
- Dataset description
- Training methodology
- Results and metrics

## 🚀 Testing Your Assets

1. **Place files in correct folders**
2. **Update Projects.tsx with paths**
3. **Run locally:** `pnpm run dev`
4. **Check:**
   - Images load properly
   - Reports download when clicked
   - No broken links

## ⚠️ Common Issues

**Image not showing?**
- Check file path (must start with `/projects/`)
- Verify file exists in `/public/projects/`
- Check file extension matches (`.png` vs `.PNG`)

**Report not downloading?**
- Verify file is in `/public/reports/`
- Check path starts with `/reports/`
- Ensure filename matches exactly (case-sensitive)

**Large files?**
- Compress images: Use TinyPNG or ImageOptim
- Compress PDFs: Use Adobe Acrobat or online tools
- Consider hosting large files on Google Drive/Dropbox

## 📱 Mobile Optimization

Images will automatically:
- Scale to container width
- Maintain aspect ratio
- Load with fallback on error

## 🎯 Next Steps

1. ✅ Create `/public/projects/` folder
2. ✅ Add your project images
3. ✅ Create `/public/reports/` folder
4. ✅ Add your PDF reports
5. ✅ Update `Projects.tsx` with correct paths
6. ✅ Test locally
7. ✅ Deploy to GitHub Pages!
