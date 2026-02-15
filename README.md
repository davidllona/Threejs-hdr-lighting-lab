# threejs-hdr-lighting-lab

Physically based rendering (PBR) lighting lab built with Three.js to understand HDR environment maps, reflections and tone mapping.

## Live Demo
- Vercel: [https://threejs-hdr-lighting-lab.vercel.app/]
## What is this?
This is a small interactive Three.js scene focused on **lighting through HDR environment maps**.
Instead of using many lights, the scene uses an HDR image to simulate realistic ambient lighting and reflections on PBR materials.

The goal is to clearly understand how **metalness**, **roughness**, and **exposure** change the final look.

## Features
- Real-time controls using **lil-gui**
- HDR environment lighting + separate background
- PBR material experiments (metalness / roughness)
- Tone mapping exposure control
- Environment rotation (to see reflections move)

## Key concepts explained (simple but correct)

### 1) Environment vs Background (important)
In Three.js there are two different things:

- `scene.environment`  
  ✅ This is what actually affects **lighting + reflections** on PBR materials (MeshStandardMaterial / MeshPhysicalMaterial).

- `scene.background`  
  ✅ This is only the **image you see behind** the scene.  
  ❌ It does not automatically light the objects (unless you also use it as `scene.environment`).

That’s why you can have a background image but still need an HDR environment map to get realistic reflections.

### 2) Why metalness and roughness change everything
With PBR materials:

- **metalness = 1**  
  The surface behaves like metal and reflects the environment strongly.

- **roughness = 0**  
  The surface becomes mirror-like (sharp reflections).

- Increasing roughness makes reflections blurrier and the object looks more matte.

That’s why a “mirror look” is usually:
`metalness: 1` + `roughness: 0`

### 3) PMREM (why reflections look realistic)
HDR images are too sharp/noisy if used directly.
Three.js uses **PMREMGenerator** to prefilter the environment, producing better and more realistic reflections for PBR materials.

### 4) Tone mapping & exposure (brightness control)
Even with the same HDR, the scene can look too dark/bright.
The main control is:

- `renderer.toneMappingExposure`

Higher exposure = brighter scene.  
Lower exposure = darker scene.

## Tech Stack
- Three.js
- Vite
- JavaScript (ES Modules)
- lil-gui

## Getting Started (local)

### 1) Install
```bash
npm install
