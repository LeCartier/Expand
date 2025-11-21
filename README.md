# Could You Elaborate

**Version 1.0.0**

An augmented reality (AR) platform for visualizing 3D models through QR codes. Point your phone camera at a QR code to instantly view architectural models, building details, equipment, and more in AR - right where you're standing.

---

## 🎯 What It Does

**Could You Elaborate** bridges the physical and digital worlds by linking QR codes to 3D models that appear in augmented reality. Users scan a QR code with their phone and can:

- **View 3D models in real space** using AR (iPhone Quick Look, Android Scene Viewer, or WebXR)
- **Place models freely** in their environment or **pin them to marker patterns**
- **Interact with models** - rotate, scale, and examine from any angle
- **Share models instantly** via QR codes that work on any modern smartphone

---

## 🏗️ Use Cases

### Architecture & Construction
- **Full building models** - View complete architectural designs at scale in AR
- **Building sections** - Display cut-away views showing internal structure and systems
- **Detail callouts** - Examine specific building components (HVAC systems, structural connections, etc.)
- **Site planning** - Visualize proposed buildings on actual construction sites
- **Client presentations** - Show stakeholders realistic 3D representations without physical models

### Engineering & Manufacturing
- **Equipment visualization** - See machinery and equipment at full scale before purchase
- **Assembly instructions** - Interactive 3D guides showing how parts fit together
- **Maintenance documentation** - AR overlays showing service points and procedures
- **Product prototypes** - Review designs in 3D before manufacturing

### Drawing Augmentation
- **2D to 3D** - Place a QR code on 2D architectural drawings; scan to see the 3D model
- **Plan overlays** - Augment floor plans with 3D furniture, fixtures, or equipment
- **Elevation details** - Show depth and dimensionality on flat elevation drawings
- **Construction documents** - Link detail drawings to 3D callouts of specific components

### Education & Training
- **Anatomy models** - Study human body systems in 3D
- **Historical artifacts** - Examine replicas of museum pieces
- **Scientific visualization** - Molecular structures, geological formations, etc.
- **Skills training** - Interactive 3D guides for equipment operation

### Marketing & Sales
- **Product catalogs** - QR codes in brochures that show products in AR
- **Trade show displays** - Augment booth signage with 3D product models
- **Real estate** - Preview furniture in spaces or show building renovations
- **Wayfinding** - AR navigation and information in physical spaces

---

## 🚀 How It Works

### System Architecture

```
┌─────────────────┐
│  Upload GLB/    │
│  USDZ Model     │ → Supabase Storage
└────────┬────────┘
         ↓
┌─────────────────┐
│  QR Code        │
│  Generated      │ → Links to viewer URL
└────────┬────────┘
         ↓
┌─────────────────┐
│  User Scans QR  │
│  with Phone     │
└────────┬────────┘
         ↓
┌─────────────────┐
│  AR Viewer      │ → Model loads in AR
│  Opens          │    (Quick Look/Scene Viewer/WebXR)
└─────────────────┘
```

### Components

1. **Model Manager (`app.html`)**
   - Upload 3D models (GLB or USDZ format)
   - Authenticate with Supabase
   - Generate QR codes for each model
   - Manage your model library

2. **AR Viewer (`view.html`)**
   - Displays 3D models using Google's Model Viewer
   - Supports AR modes: WebXR, ARCore (Scene Viewer), ARKit (Quick Look)
   - Free placement mode - place models anywhere in your space
   - Camera controls for desktop viewing

3. **Marker-Based Viewer (`mark-view.html`)**
   - Uses AR.js for marker tracking
   - Pin models to physical QR markers
   - Models stay locked to marker position
   - Touch gestures for rotation and scaling

4. **Database (Supabase)**
   - Stores model metadata and file URLs
   - Handles user authentication
   - Manages file storage (GLB/USDZ files)

---

## 📱 Supported Devices & Browsers

### iOS (iPhone/iPad)
- **Safari** - Full AR support via ARKit Quick Look
- Tap "View in AR" to place models in real space
- Models appear at real-world scale

### Android
- **Chrome** - AR support via ARCore Scene Viewer
- Works on ARCore-compatible devices
- Tap "View in your space" for AR placement

### Desktop/Laptop
- **Any modern browser** - 3D preview with camera controls
- No AR, but full model interaction (rotate, zoom, pan)

### AR Headsets
- **WebXR-compatible devices** - Full AR/VR support
- Meta Quest, HoloLens, Magic Leap (via browser)

---

## 🎨 Model Requirements

### File Formats
- **GLB** (recommended) - GLTF 2.0 binary format
- **USDZ** (iOS only) - Apple's AR format for Quick Look
- Upload both formats for maximum compatibility

### Model Guidelines
- **File size**: Keep under 10 MB for best mobile performance
- **Texture size**: 2048x2048 pixels maximum recommended
- **Polygon count**: < 100k triangles for mobile devices
- **Materials**: Use PBR materials (Metallic-Roughness workflow)
- **Units**: Model in real-world scale (meters preferred)
- **Orientation**: Y-up coordinate system

### Optimization Tips
- Remove unnecessary geometry and hidden faces
- Combine meshes where possible
- Use texture atlases to reduce draw calls
- Compress textures (JPG for color, PNG for alpha)
- Test on actual mobile devices

---

## ⚙️ Setup & Installation

### Prerequisites
- A Supabase account (free tier works)
- GitHub account (for GitHub Pages hosting)
- 3D modeling software (Blender, SketchUp, Revit, etc.)

### Quick Start

1. **Create a Supabase Project**
   ```
   - Go to https://supabase.com
   - Create a new project
   - Note your project URL and anon key
   ```

2. **Set Up Database**
   - Create a table named `qr_models` with columns:
     - `id` (text, primary key)
     - `owner_user_id` (uuid, references auth.users)
     - `name` (text)
     - `glb_url` (text)
     - `usdz_url` (text)
     - `source_type` (text)
     - `created_at` (timestamp)

3. **Configure Storage**
   - Create a storage bucket named `models`
   - Set bucket to public
   - Configure CORS to allow your domain

4. **Update Configuration**
   - Edit `config.js` with your Supabase credentials:
   ```javascript
   window.APP_CONFIG = {
     SUPABASE_URL: "your-project-url",
     SUPABASE_ANON_KEY: "your-anon-key",
     VIEWER_BASE_URL: "https://yourusername.github.io/Expand/view.html"
   };
   ```

5. **Deploy to GitHub Pages**
   - Push code to a GitHub repository
   - Enable GitHub Pages in repository settings
   - Set source to main branch

6. **Start Using**
   - Open `app.html` in your browser
   - Sign up for an account
   - Upload your first model
   - Scan the generated QR code with your phone!

---

## 📖 User Guide

### Uploading Models

1. Open the Model Manager (`app.html`)
2. Sign in or create an account
3. Enter a descriptive name for your model
4. Choose your GLB or USDZ file (or both)
5. Click "Upload & create QR"
6. QR code appears in your model library

### Viewing in AR

**On Mobile:**
1. Scan the QR code with your phone camera
2. Browser opens the AR viewer
3. Tap "View on floor in AR" or "View in your space"
4. Point camera at floor/surface
5. Tap to place model
6. Pinch to scale, drag to rotate

**On Desktop:**
1. Open the viewer URL in browser
2. Use mouse to orbit, pan, and zoom
3. Preview model before generating QR

### Marker-Based AR

1. Click "Pin to QR (marker)" in the viewer
2. Print the marker pattern (`FFE.patt`)
3. Point phone camera at printed marker
4. Model appears locked to marker position
5. Touch to rotate and scale

### Managing Models

- **Copy URL** - Share direct link to AR viewer
- **Download QR** - Save high-res QR code image (with logo)
- **Delete** - Remove model and free up storage
- All models are private to your account

---

## 🔧 Customization

### Change QR Marker Pattern
Replace `FFE.patt` with your own marker file from [AR.js Marker Training](https://ar-js-org.github.io/AR.js/three.js/examples/marker-training/examples/generator.html)

### Adjust Model Scale
Edit `mark-view.html`, change the target size:
```javascript
const targetSize = 0.6096; // 2 feet in meters
```

### Modify Branding
- Replace `Logo.png` with your logo (will appear in QR codes)
- Edit CSS colors and styling in each HTML file
- Update footer links and attribution

### Add Custom Features
The codebase is modular - extend with:
- Animation support
- Multi-model scenes
- Measurement tools
- Annotation overlays

---

## 🐛 Troubleshooting

### Model doesn't appear in AR
- Check file size (< 10 MB recommended)
- Verify GLB is valid GLTF 2.0 format
- Ensure model has materials and textures
- Test on different devices

### QR code doesn't scan
- Increase QR code size when printing
- Ensure good lighting and contrast
- Use a QR scanner app if camera doesn't auto-detect
- Check that viewer URL is accessible

### Marker tracking issues
- Print marker at least 3" x 3" in size
- Use matte paper (avoid glare)
- Ensure good lighting conditions
- Keep marker flat and visible to camera

### Model appears too large/small
- Models auto-scale to 2 feet max dimension
- Original model scale affects final size
- Edit scale factor in `mark-view.html` if needed

---

## 🤝 Contributing

Contributions are welcome! This is an open-source project under the MIT License.

**Areas for improvement:**
- Multi-language support
- Advanced AR features (plane detection, lighting estimation)
- Model analytics (view counts, engagement)
- Batch QR generation
- Custom QR styling

---

## 📄 License

This project is licensed under the **MIT License** - see [LICENSE](LICENSE) file for details.

Built with open-source technologies - see [ATTRIBUTIONS.md](ATTRIBUTIONS.md) for complete credits.

---

## 🔗 Resources

### Documentation
- [A-Frame Docs](https://aframe.io/docs/)
- [AR.js Guide](https://ar-js-org.github.io/AR.js-Docs/)
- [Model Viewer Docs](https://modelviewer.dev/docs/)
- [Supabase Docs](https://supabase.com/docs)

### 3D Model Resources
- [Sketchfab](https://sketchfab.com) - 3D model marketplace
- [Poly Haven](https://polyhaven.com) - Free PBR textures and models
- [glTF Sample Models](https://github.com/KhronosGroup/glTF-Sample-Models) - Test models

### Tools
- [Blender](https://www.blender.org) - Free 3D modeling software
- [glTF Validator](https://github.khronos.org/glTF-Validator/) - Check GLB files
- [AR.js Marker Generator](https://ar-js-org.github.io/AR.js/three.js/examples/marker-training/examples/generator.html)

---

## 📧 Support

For questions, issues, or feature requests, please open an issue on GitHub.

**Version**: 1.0.0  
**Last Updated**: November 21, 2025

---

*Could You Elaborate - Bringing 3D models to life in AR*
