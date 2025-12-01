# Setting Up Vite for the AI Interface

---

## ⚠️ IMPORTANT UPDATE - Please Read!

**This section has been updated from the original instructions to ensure the AI interface works correctly.**

In the original setup, we used `lite-server` as our development server. However, to support the AI chat interface (which uses modern JavaScript modules), we need to upgrade to **Vite** - a more powerful development tool that supports the features we need.

**What's changing:**
- ✅ Installing Vite instead of (or in addition to) lite-server
- ✅ Creating a `vite.config.js` configuration file
- ✅ Updating the npm scripts in `package.json`
- ✅ Everything else stays the same!

**Why Vite?**
- Supports modern JavaScript modules (required for AI interface)
- Faster development server with instant updates
- Industry-standard tool used by professional developers
- Better error messages and debugging

---

## Exercise: Upgrade to Vite Development Server

### Objectives
* Install Vite as a development dependency
* Create a Vite configuration file
* Update package.json scripts
* Test that your site still works perfectly
* Prepare for AI interface integration

---

### Part 1: Install Vite

**Step 1: Open your terminal**
* Make sure you're in the `JagTrack` folder
* The terminal path should end with `JagTrack`

**Step 2: Install Vite**
In your terminal, type:
```bash
npm install vite --save-dev
```

**What this does:**
* Installs Vite as a development tool
* Adds it to your `package.json` under `devDependencies`
* Downloads all necessary files to run Vite

**You may see warnings:** These are normal. Only worry about messages marked "ERR" or "Error"

---

### Part 2: Create Vite Configuration File

**Step 1: Create vite.config.js**
* In VS Code, create a new file in the **root** of your `JagTrack` folder (same level as `index.html`)
* Name it: `vite.config.js`

**Step 2: Add the configuration code**
Copy and paste this code into `vite.config.js`:

```javascript
import { defineConfig } from 'vite';

export default defineConfig({
  root: './',
  server: {
    port: 3000,
    open: '/index.html'
  }
});
```

**What this configuration does:**
* `root: './'` - Sets the root folder for your project
* `port: 3000` - Runs the server on port 3000 (same as lite-server did)
* `open: '/index.html'` - Automatically opens index.html when you start the server

**Step 3: Save the file**
* Make sure Auto Save is enabled (checkmark should appear next to File → Auto Save)

---

### Part 3: Update package.json Scripts

Now you need to update your npm scripts to use Vite instead of lite-server.

**Step 1: Open package.json**
* Click on the `package.json` file in VS Code
* Find the `"scripts"` section (should be around lines 6-11)

**Step 2: Replace the scripts section**
Replace the current `"scripts"` section with:

```json
"scripts": {
  "dev": "vite",
  "start": "vite",
  "build": "vite build",
  "preview": "vite preview",
  "test": "echo \"Error: no test specified\" && exit 1"
},
```

**What changed:**
* **OLD:** `"lite": "lite-server"` → **NEW:** `"dev": "vite"` (runs Vite dev server)
* **OLD:** `"start": "npm run lite"` → **NEW:** `"start": "vite"` (direct Vite command)
* **NEW:** `"build": "vite build"` (creates production-ready files - you'll use this later)
* **NEW:** `"preview": "vite preview"` (previews the built site)

**Important details:**
* Make sure each line inside `scripts` ends with a comma, **except the last line**
* If you see red lines in your code, it means there's a syntax issue - check your commas!

**Your full package.json should now look similar to this:**
```json
{
  "name": "jagtrack-bootstrap",
  "version": "1.0.0",
  "description": "This is a website made to help Jefferson Academy students organize their classes",
  "main": "index.html",
  "scripts": {
    "dev": "vite",
    "start": "vite",
    "build": "vite build",
    "preview": "vite preview",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "devDependencies": {
    "lite-server": "^2.6.1",
    "vite": "^7.2.4"
  },
  "dependencies": {
    "bootstrap": "^4.5.2",
    "jquery": "^3.5.1",
    "popper.js": "^1.16.1"
  }
}
```

---

### Part 4: Test Your Vite Setup

**Step 1: Stop any running servers**
* If you have a terminal running with `npm start` or lite-server, press `Ctrl+C` to stop it
* This frees up port 3000 for Vite

**Step 2: Start Vite**
In your terminal, type:
```bash
npm start
```

**What should happen:**
* Vite starts up (you'll see green text saying "VITE" and "ready in X ms")
* Your browser automatically opens to `http://localhost:3000`
* You should see your JagTrack homepage with all your styling intact
* The terminal shows: `➜  Local:   http://localhost:3000/`

**Step 3: Test hot module replacement**
* With the server running, make a small change to your `index.html` (like changing "JagTrack" to "JagTrack!")
* Save the file
* Watch your browser - it should update **instantly** without a full page reload
* This is one of Vite's best features - instant feedback!

**Step 4: Test navigation**
* Click around your site to make sure all pages work
* Test `index.html`
* Test `myclassesnextquarter.html` (if you've created it)
* All Bootstrap styling should still work perfectly

**To stop the Vite server:**
* In your terminal, press `Ctrl+C`

---

### Part 5: Update Your .gitignore

Since we're using Vite now, we should add Vite's build folder to `.gitignore`.

**Step 1: Open .gitignore**
* Find and open the `.gitignore` file in your JagTrack folder

**Step 2: Add Vite folders**
Your `.gitignore` should now include:
```
node_modules/
.DS_Store
dist/
```

**What this does:**
* `dist/` - Vite's build output folder (created when you run `npm run build`)
* We don't need to track this in Git since it's automatically generated

---

### Troubleshooting Common Issues

**Issue: "Port 3000 is already in use"**
* **Solution:** You have lite-server or another Vite instance still running
* Press `Ctrl+C` in all terminal tabs to stop servers
* Try `npm start` again

**Issue: "Cannot find module 'vite'"**
* **Solution:** Vite didn't install correctly
* Run: `npm install vite --save-dev` again
* Check that `"vite"` appears in your `package.json` under `devDependencies`

**Issue: Browser opens but shows error**
* **Solution:** Check that `vite.config.js` is in the root folder (same level as `index.html`)
* Make sure there are no typos in the config file

**Issue: Changes don't show up in browser**
* **Solution:** Hard refresh the browser with `Ctrl+Shift+R` (Windows) or `Cmd+Shift+R` (Mac)
* Stop and restart the Vite server

---

### Checkpoint: Vite Setup Complete

Verify you've completed these items:

- [ ] Vite installed (`npm install vite --save-dev`)
- [ ] `vite.config.js` created in root folder
- [ ] Configuration code added to `vite.config.js`
- [ ] `package.json` scripts updated to use Vite
- [ ] `.gitignore` updated with `dist/` folder
- [ ] `npm start` runs without errors
- [ ] Browser opens automatically to `http://localhost:3000`
- [ ] JagTrack site displays correctly with all styling
- [ ] Hot module replacement works (instant updates when you save files)

**Commit your Vite setup to Git:**

```bash
git add .
git commit -m "Updated to Vite dev server for AI interface support"
git push
```

---

### Summary

In this section, you:
* Upgraded from lite-server to Vite for better module support
* Created a Vite configuration file
* Updated npm scripts to use Vite commands
* Tested that everything still works perfectly
* Prepared your project for the AI chat interface

**Important Notes:**
* You can still use `npm start` just like before - it now runs Vite instead of lite-server
* Vite is **faster** and provides **instant updates** when you save files
* This setup is required for the AI interface to work correctly
* You're now using industry-standard development tools!

---

## What's Next?

Now that Vite is set up and working, you're ready to integrate the AI chat interface in the next section! The AI interface will use modern JavaScript modules that Vite supports, giving your JagTrack site an intelligent assistant to help with your studies.

---
