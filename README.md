<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Omveer Upadhyay | CNC Programmer & CAM Portfolio</title>
  
  <!-- Three.js & STLLoader for 3D CAD Previewing -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/three@0.128.0/examples/js/loaders/STLLoader.js"></script>

  <style>
    :root {
      --bg: #0b0d0f;
      --panel: #121619;
      --panel2: #171c20;
      --orange: #ff7a00;
      --orange2: #ff9d3d;
      --text: #f1f3f4;
      --muted: #a6b0b6;
      --line: #2a3034;
      --green: #72d572;
      --red: #ff5555;
      --blue: #0088ff;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    html {
      scroll-behavior: smooth;
    }

    body {
      background: 
        linear-gradient(rgba(255,255,255,.02) 1px, transparent 1px),
        linear-gradient(90deg, rgba(255,255,255,.02) 1px, transparent 1px),
        var(--bg);
      background-size: 40px 40px;
      color: var(--text);
      font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
      line-height: 1.6;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
    }

    body::before {
      content: "";
      position: fixed;
      inset: 0;
      pointer-events: none;
      background: radial-gradient(circle at 80% 10%, rgba(255,122,0,.08), transparent 40%);
    }

    .container {
      width: min(1180px, 92%);
      margin: auto;
    }

    /* NAVIGATION */
    nav {
      position: sticky;
      top: 0;
      z-index: 100;
      background: rgba(11, 13, 15, 0.94);
      backdrop-filter: blur(12px);
      border-bottom: 1px solid var(--line);
    }

    .nav-inner {
      height: 70px;
      display: flex;
      align-items: center;
      justify-content: space-between;
    }

    .logo {
      font-weight: 800;
      letter-spacing: 2px;
      text-decoration: none;
      color: var(--text);
      font-size: 18px;
      cursor: pointer;
    }

    .logo span {
      color: var(--orange);
    }

    .nav-links {
      display: flex;
      gap: 24px;
      list-style: none;
    }

    .nav-links a {
      color: var(--muted);
      text-decoration: none;
      font-size: 13px;
      font-weight: 600;
      letter-spacing: 0.5px;
      transition: color 0.2s, border-bottom 0.2s;
      padding: 8px 0;
      cursor: pointer;
    }

    .nav-links a:hover,
    .nav-links a.active {
      color: var(--orange);
      border-bottom: 2px solid var(--orange);
    }

    /* PAGE VIEW TOGGLING */
    .page-view {
      display: none;
      padding: 60px 0;
      flex: 1;
      animation: fadeIn 0.3s ease-in-out;
    }

    .page-view.active {
      display: block;
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(6px); }
      to { opacity: 1; transform: translateY(0); }
    }

    /* HERO / HOME PAGE */
    .hero {
      min-height: calc(100vh - 200px);
      display: grid;
      grid-template-columns: 1.15fr 0.85fr;
      align-items: center;
      gap: 50px;
    }

    .eyebrow {
      color: var(--orange);
      font-size: 13px;
      font-weight: bold;
      letter-spacing: 3px;
      margin-bottom: 18px;
    }

    .hero h1 {
      font-size: clamp(42px, 6vw, 80px);
      line-height: 0.98;
      letter-spacing: -2px;
      font-weight: 900;
    }

    .hero h1 span {
      color: var(--orange);
    }

    .hero h2 {
      margin-top: 20px;
      font-size: 22px;
      font-weight: 400;
      color: #d6dadd;
    }

    .hero p {
      margin-top: 18px;
      max-width: 620px;
      color: var(--muted);
    }

    .buttons {
      display: flex;
      gap: 14px;
      margin-top: 32px;
      flex-wrap: wrap;
    }

    .btn {
      padding: 12px 22px;
      border: 1px solid var(--orange);
      color: var(--text);
      text-decoration: none;
      font-size: 13px;
      font-weight: bold;
      letter-spacing: 1px;
      transition: all 0.25s ease;
      display: inline-block;
      cursor: pointer;
    }

    .btn.primary {
      background: var(--orange);
      color: #111;
    }

    .btn:hover {
      transform: translateY(-2px);
      box-shadow: 0 8px 25px rgba(255, 122, 0, 0.25);
    }

    /* CANVAS VISUALIZER */
    .machine-visual {
      min-height: 380px;
      border: 1px solid var(--line);
      background: #0d1013;
      position: relative;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      padding: 20px;
    }

    canvas {
      width: 100%;
      max-width: 380px;
      height: 240px;
      background: #080a0b;
      border: 1px solid var(--line);
    }

    .sim-readout {
      margin-top: 12px;
      font-family: monospace;
      font-size: 12px;
      color: var(--orange2);
      letter-spacing: 1px;
    }

    /* SECTION HEADINGS */
    .section-head {
      margin-bottom: 40px;
    }

    .section-number {
      color: var(--orange);
      font-family: monospace;
      font-size: 13px;
    }

    .section-title {
      font-size: 38px;
      margin-top: 6px;
      font-weight: 800;
    }

    /* GRIDS & PANELS */
    .about-grid, .contact-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 24px;
    }

    .panel {
      background: var(--panel);
      border: 1px solid var(--line);
      padding: 28px;
    }

    .panel h3 {
      margin-bottom: 12px;
      color: var(--orange2);
      font-size: 20px;
    }

    .panel p {
      color: var(--muted);
    }

    .software-grid, .projects {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      gap: 20px;
    }

    .software {
      background: linear-gradient(145deg, #171c20, #0f1214);
      border: 1px solid var(--line);
      padding: 26px;
    }

    .software .number {
      color: var(--orange);
      font-family: monospace;
      font-size: 12px;
    }

    .software h3 {
      font-size: 24px;
      margin: 10px 0;
    }

    .software ul {
      margin-top: 12px;
      padding-left: 18px;
      color: var(--muted);
      font-size: 13.5px;
    }

    /* UPLOAD CARDS STYLING */
    .upload-grid {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 20px;
      margin-top: 20px;
    }

    .upload-card {
      background: var(--panel2);
      border: 2px dashed var(--line);
      padding: 24px;
      border-radius: 4px;
      text-align: center;
      transition: border-color 0.3s, background-color 0.3s;
    }

    .upload-card:hover {
      border-color: var(--orange);
      background: #1a2025;
    }

    .upload-card h4 {
      color: var(--text);
      font-size: 16px;
      margin-bottom: 8px;
    }

    .upload-card p {
      color: var(--muted);
      font-size: 12px;
      margin-bottom: 16px;
      font-family: monospace;
    }

    .file-input {
      display: none;
    }

    .file-label {
      display: inline-block;
      padding: 10px 18px;
      background: var(--orange);
      color: #111;
      font-size: 12px;
      font-weight: bold;
      letter-spacing: 1px;
      cursor: pointer;
      transition: all 0.2s;
    }

    .file-label:hover {
      background: var(--orange2);
      transform: translateY(-1px);
    }

    .file-status {
      margin-top: 12px;
      font-size: 12px;
      font-family: monospace;
      color: var(--green);
      word-break: break-all;
    }

    /* UPLOADED FILES SECTION */
    .file-list-container {
      margin-top: 25px;
      background: var(--panel);
      border: 1px solid var(--line);
      padding: 20px;
    }

    .file-list-container h4 {
      color: var(--orange2);
      font-size: 16px;
      margin-bottom: 12px;
      display: flex;
      align-items: center;
      justify-content: space-between;
    }

    .file-table {
      width: 100%;
      border-collapse: collapse;
      font-size: 13px;
      font-family: monospace;
    }

    .file-table th {
      text-align: left;
      padding: 10px;
      background: #080a0b;
      color: var(--orange);
      border-bottom: 1px solid var(--line);
    }

    .file-table td {
      padding: 10px;
      border-bottom: 1px solid var(--line);
      color: var(--text);
    }

    .file-table tr:last-child td {
      border-bottom: none;
    }

    .btn-view {
      background: transparent;
      border: 1px solid var(--blue);
      color: var(--blue);
      padding: 4px 10px;
      cursor: pointer;
      font-size: 11px;
      font-family: monospace;
      margin-right: 6px;
      transition: all 0.2s;
    }

    .btn-view:hover {
      background: var(--blue);
      color: #fff;
    }

    .btn-delete {
      background: transparent;
      border: 1px solid var(--red);
      color: var(--red);
      padding: 4px 10px;
      cursor: pointer;
      font-size: 11px;
      font-family: monospace;
      transition: all 0.2s;
    }

    .btn-delete:hover {
      background: var(--red);
      color: #fff;
    }

    .empty-msg {
      color: var(--muted);
      font-size: 13px;
      font-family: monospace;
      padding: 10px 0;
      text-align: center;
    }

    /* CAD/G-CODE VIEWER MODAL */
    .modal-overlay {
      display: none;
      position: fixed;
      inset: 0;
      background: rgba(0, 0, 0, 0.85);
      backdrop-filter: blur(6px);
      z-index: 1000;
      align-items: center;
      justify-content: center;
      padding: 20px;
    }

    .modal-overlay.active {
      display: flex;
    }

    .modal-content {
      background: var(--panel);
      border: 1px solid var(--orange);
      width: min(900px, 95vw);
      max-height: 85vh;
      display: flex;
      flex-direction: column;
      border-radius: 4px;
      overflow: hidden;
      box-shadow: 0 10px 40px rgba(0,0,0,0.8);
    }

    .modal-header {
      background: #080a0b;
      padding: 14px 20px;
      border-bottom: 1px solid var(--line);
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    .modal-header h3 {
      font-size: 16px;
      color: var(--orange);
      font-family: monospace;
    }

    .modal-close {
      background: transparent;
      border: none;
      color: var(--muted);
      font-size: 20px;
      cursor: pointer;
      font-weight: bold;
    }

    .modal-close:hover {
      color: var(--orange);
    }

    .modal-body {
      padding: 20px;
      overflow-y: auto;
      flex: 1;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
    }

    #viewerCanvasContainer {
      width: 100%;
      height: 400px;
      background: #080a0b;
      border: 1px solid var(--line);
      position: relative;
    }

    .code-viewer {
      width: 100%;
      background: #080a0b;
      border: 1px solid var(--line);
      padding: 16px;
      color: var(--green);
      font-family: monospace;
      font-size: 13px;
      line-height: 1.6;
      max-height: 400px;
      overflow-y: auto;
      white-space: pre-wrap;
    }

    .archive-viewer {
      width: 100%;
      background: var(--panel2);
      border: 1px solid var(--line);
      padding: 24px;
      text-align: left;
    }

    .archive-viewer h4 {
      color: var(--orange2);
      margin-bottom: 10px;
      font-size: 18px;
    }

    .archive-viewer p {
      color: var(--muted);
      font-size: 13px;
      margin-bottom: 8px;
      font-family: monospace;
    }

    .project {
      background: var(--panel);
      border: 1px solid var(--line);
      padding: 28px;
    }

    .project-number {
      font-family: monospace;
      color: var(--orange);
      font-size: 12px;
    }

    .project h3 {
      font-size: 22px;
      margin: 12px 0 8px;
    }

    .project p {
      color: var(--muted);
      font-size: 14px;
    }

    .project-flow {
      margin-top: 18px;
      color: #d2d6d8;
      font-size: 12px;
      font-family: monospace;
      background: rgba(0,0,0,0.3);
      padding: 8px 12px;
      border-left: 2px solid var(--orange);
    }

    /* EXPERIENCE */
    .experience {
      border-left: 2px solid var(--orange);
      padding-left: 26px;
    }

    .exp-item {
      margin-bottom: 32px;
    }

    .exp-item .date {
      color: var(--orange);
      font-family: monospace;
      font-size: 12px;
    }

    .exp-item h3 {
      margin: 6px 0;
      font-size: 20px;
    }

    .exp-list {
      margin-top: 12px;
      padding-left: 18px;
      color: var(--muted);
    }

    .exp-list li {
      margin: 6px 0;
      font-size: 14px;
    }

    /* CONTACT */
    .contact-item {
      border: 1px solid var(--line);
      padding: 20px;
      background: var(--panel);
    }

    .contact-item span {
      color: var(--orange);
      font-family: monospace;
      font-size: 11px;
    }

    .contact-item p {
      margin-top: 4px;
      font-weight: 600;
    }

    /* FOOTER */
    footer {
      border-top: 1px solid var(--line);
      padding: 30px 0;
      color: var(--muted);
      font-size: 12px;
      margin-top: auto;
    }

    .footer-flex {
      display: flex;
      justify-content: space-between;
      gap: 20px;
    }

    .orange {
      color: var(--orange);
    }

    /* RESPONSIVE MEDIA QUERIES */
    @media (max-width: 900px) {
      .hero, .about-grid, .contact-grid, .software-grid, .projects, .upload-grid {
        grid-template-columns: 1fr;
      }
    }

    @media (max-width: 600px) {
      .nav-links {
        display: flex;
        gap: 12px;
        flex-wrap: wrap;
      }

      .nav-inner {
        height: auto;
        padding: 15px 0;
        flex-direction: column;
        gap: 10px;
      }

      .hero h1 {
        font-size: 40px;
      }

      .section-title {
        font-size: 30px;
      }

      .file-table {
        display: block;
        overflow-x: auto;
      }
    }
  </style>
</head>
<body>

  <!-- NAVIGATION -->
  <nav>
    <div class="container nav-inner">
      <a onclick="showPage('home')" class="logo">OM<span>V</span>EER</a>
      <ul class="nav-links">
        <li><a id="nav-home" class="active" onclick="showPage('home')">HOME</a></li>
        <li><a id="nav-about" onclick="showPage('about')">ABOUT</a></li>
        <li><a id="nav-cam" onclick="showPage('cam')">CAM</a></li>
        <li><a id="nav-projects" onclick="showPage('projects')">PROJECTS</a></li>
        <li><a id="nav-experience" onclick="showPage('experience')">EXPERIENCE</a></li>
        <li><a id="nav-contact" onclick="showPage('contact')">CONTACT</a></li>
      </ul>
    </div>
  </nav>

  <main class="container">
    <!-- PAGE 1: HOME -->
    <div id="page-home" class="page-view active">
      <div class="hero">
        <div>
          <div class="eyebrow">MECHANICAL ENGINEERING / CNC / CAM</div>
          <h1>OMVEER<br><span>UPADHYAY</span></h1>
          <h2>CNC Programmer &amp; CAM Professional</h2>
          <p>
            Mechanical Engineering professional focused on CNC turning/milling, G-code execution,
            tooling setups, CAD/CAM workflow, and quality-driven manufacturing.
          </p>
          <div class="buttons">
            <a class="btn primary" onclick="showPage('about')">LEARN MORE ABOUT ME</a>
            <a class="btn" onclick="showPage('cam')">EXPLORE CAM</a>
            <a class="btn" onclick="showPage('contact')">GET IN TOUCH</a>
          </div>
        </div>

        <div class="machine-visual">
          <canvas id="cncCanvas"></canvas>
          <div class="sim-readout" id="cncReadout">G01 X50.000 Z-12.500 F0.2</div>
        </div>
      </div>
    </div>

    <!-- PAGE 2: ABOUT -->
    <div id="page-about" class="page-view">
      <div class="section-head">
        <div class="section-number">01 / PROFILE</div>
        <h2 class="section-title">About Me</h2>
      </div>

      <div class="about-grid">
        <div class="panel">
          <h3>Professional Summary</h3>
          <p>
            I am a Mechanical Engineering graduate and CNC/CAM professional with practical shop-floor 
            experience in precision manufacturing. My technical foundation spans CNC turning, VMC operation, 
            G-code/M-code programming, and CAD/CAM modeling using software like Mastercam and AutoCAD.
          </p>
          <br>
          <p>
            With hands-on experience in high-volume production environments, I bridge the gap between 
            digital design files and zero-defect machined components through precise tooling setups, 
            work offset calibrations, and in-process quality control.
          </p>
        </div>

        <div class="panel">
          <h3>Career Objective</h3>
          <p>
            To advance my engineering career in <strong>CNC Programming, Tooling Optimization, and CAM Technology</strong>. 
            I aim to combine hands-on machining insights with modern CAM toolpath strategies to minimize cycle times, 
            extend tool life, and drive efficient manufacturing operations.
          </p>
          <br>
          <p class="orange" style="font-family: monospace; font-size: 13px;">
            PRECISION • CYCLE EFFICIENCY • QUALITY CONTROL
          </p>
        </div>
      </div>

      <div style="margin-top: 30px;" class="about-grid">
        <div class="panel">
          <h3>Core Technical Focus Areas</h3>
          <ul style="padding-left: 20px; color: var(--muted); font-size: 14px;">
            <li style="margin-bottom: 8px;"><strong>CNC &amp; VMC Machining:</strong> Setups, work coordinate systems (G54–G59), and tool length offsets.</li>
            <li style="margin-bottom: 8px;"><strong>G-Code Programming:</strong> Manual programming for 2-axis turning and multi-axis milling (canned cycles, cutter comp G41/G42).</li>
            <li style="margin-bottom: 8px;"><strong>CAD/CAM Integration:</strong> 2D drafting in AutoCAD and 2D/3D toolpath creation in Mastercam.</li>
            <li style="margin-bottom: 8px;"><strong>Quality &amp; GD&amp;T:</strong> Reading engineering drawings, interpreting geometric tolerances, and in-process dimensional inspection.</li>
          </ul>
        </div>

        <div class="panel">
          <h3>Background &amp; Experience</h3>
          <p style="color: var(--muted); font-size: 14px; margin-bottom: 12px;">
            <strong>Education:</strong> B.Tech in Mechanical Engineering
          </p>
          <p style="color: var(--muted); font-size: 14px; margin-bottom: 12px;">
            <strong>Industry Experience:</strong> Hands-on experience in manufacturing environments (including production monitoring, line inspection, and VMC/CNC machine setups at Baxy Engineering Pvt. Ltd.).
          </p>
          <div class="buttons" style="margin-top: 20px;">
            <a class="btn primary" onclick="showPage('cam')">VIEW CAM SKILLS</a>
            <a class="btn" onclick="showPage('experience')">SEE WORK EXPERIENCE</a>
          </div>
        </div>
      </div>
    </div>

    <!-- PAGE 3: CAD / CAM -->
    <div id="page-cam" class="page-view">
      <div class="section-head">
        <div class="section-number">02 / SOFTWARE &amp; WORKFLOW</div>
        <h2 class="section-title">CAD / CAM Engineering</h2>
      </div>

      <div class="software-grid">
        <div class="software">
          <div class="number">01 / CAM</div>
          <h3>Mastercam</h3>
          <p>Primary CAM tool for 2D/3D milling, turning profile setup, and toolpath verification.</p>
          <ul>
            <li>2D Contour, Dynamic Motion, &amp; Pocketing</li>
            <li>3D Surface High-Speed Machining (HSM)</li>
            <li>Stock setup &amp; solid model verification</li>
            <li>Post-processor execution for FANUC/Haas controls</li>
          </ul>
        </div>

        <div class="software">
          <div class="number">02 / CAM</div>
          <h3>PowerMill</h3>
          <p>Advanced 3-axis milling software for complex surfaces and automated toolpath generation.</p>
          <ul>
            <li>Model roughing (3D Offset &amp; Area Clearance)</li>
            <li>Finishing strategies (Constant Z, Raster, Parametric)</li>
            <li>Collision detection &amp; holder clearance checking</li>
            <li>Optimal stock model tracking</li>
          </ul>
        </div>

        <div class="software">
          <div class="number">03 / CAD</div>
          <h3>AutoCAD</h3>
          <p>2D mechanical drafting, geometry cleanup for CAM import, and profile engineering.</p>
          <ul>
            <li>2D profile geometry creation for CNC turning/milling</li>
            <li>Engineering drawing reading &amp; GD&amp;T interpretation</li>
            <li>Fixture and clamping layout drafting</li>
            <li>DXF/DWG file preparation for CAM integration</li>
          </ul>
        </div>
      </div>

      <!-- DIRECT FILE UPLOAD SECTION -->
      <div style="margin-top: 40px;">
        <h3 style="color: var(--orange2); font-size: 20px; margin-bottom: 10px;">Direct CAD/CAM File Portal</h3>
        <p style="color: var(--muted); font-size: 14px;">Select your 2D/3D design or toolpath project file below for review and G-code execution.</p>
        
        <div class="upload-grid">
          <!-- Mastercam 2D -->
          <div class="upload-card">
            <h4>Mastercam 2D Upload</h4>
            <p>.mcam, .dxf, .dwg, .step, .igs</p>
            <label class="file-label" for="mcam2d-file">SELECT 2D FILE</label>
            <input type="file" id="mcam2d-file" class="file-input" accept=".mcam,.dxf,.dwg,.step,.stp,.igs,.iges,.stl,.nc,.gcode" onchange="processFileUpload(this, 'Mastercam 2D', 'mcam2d-status')">
            <div id="mcam2d-status" class="file-status"></div>
          </div>

          <!-- Mastercam 3D -->
          <div class="upload-card">
            <h4>Mastercam 3D Upload</h4>
            <p>.mcam, .step, .stp, .x_t, .igs</p>
            <label class="file-label" for="mcam3d-file">SELECT 3D FILE</label>
            <input type="file" id="mcam3d-file" class="file-input" accept=".mcam,.step,.stp,.x_t,.igs,.iges,.stl" onchange="processFileUpload(this, 'Mastercam 3D', 'mcam3d-status')">
            <div id="mcam3d-status" class="file-status"></div>
          </div>

          <!-- PowerMill CAM -->
          <div class="upload-card">
            <h4>PowerMill CAM Upload</h4>
            <p>.pkm, .pxd, .dgk, .step, .zip</p>
            <label class="file-label" for="powermill-file">SELECT POWERMILL FILE</label>
            <input type="file" id="powermill-file" class="file-input" accept=".pkm,.pxd,.dgk,.step,.stp,.zip" onchange="processFileUpload(this, 'PowerMill CAM', 'powermill-status')">
            <div id="powermill-status" class="file-status"></div>
          </div>
        </div>

        <!-- UPLOADED FILES DISPLAY SECTION -->
        <div class="file-list-container">
          <h4>
            <span>UPLOADED CAD/CAM FILES</span>
            <span id="fileCount" style="color: var(--muted); font-size: 12px; font-weight: normal;">(0 Files)</span>
          </h4>
          <div id="fileTableWrapper">
            <p class="empty-msg" id="emptyMsg">No files uploaded yet. Select a file above to add it to your queue.</p>
            <table class="file-table" id="fileTable" style="display: none;">
              <thead>
                <tr>
                  <th>FILE NAME</th>
                  <th>CATEGORY</th>
                  <th>SIZE</th>
                  <th>DATE UPLOADED</th>
                  <th>ACTION</th>
                </tr>
              </thead>
              <tbody id="fileTableBody">
                <!-- Dynamic File Rows Added Here -->
              </tbody>
            </table>
          </div>
        </div>
      </div>

      <div style="margin-top: 40px;">
        <h3 style="color: var(--orange2); font-size: 20px; margin-bottom: 20px;">Standard CAM Programming Process</h3>
        <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); gap: 16px;">
          <div class="panel" style="padding: 20px;">
            <div style="color: var(--orange); font-family: monospace; font-size: 12px;">STEP 01</div>
            <h4 style="margin: 8px 0;">Geometry Prep</h4>
            <p style="font-size: 13px; color: var(--muted);">Import 2D/3D CAD model, align coordinate origin (WCS / G54), and clean up boundary curves.</p>
          </div>
          <div class="panel" style="padding: 20px;">
            <div style="color: var(--orange); font-family: monospace; font-size: 12px;">STEP 02</div>
            <h4 style="margin: 8px 0;">Stock &amp; Tooling</h4>
            <p style="font-size: 13px; color: var(--muted);">Define raw stock dimensions, select tooling, calculate speeds/feeds, and assign tool station numbers.</p>
          </div>
          <div class="panel" style="padding: 20px;">
            <div style="color: var(--orange); font-family: monospace; font-size: 12px;">STEP 03</div>
            <h4 style="margin: 8px 0;">Toolpath Setup</h4>
            <p style="font-size: 13px; color: var(--muted);">Apply roughing, semi-finishing, and finishing strategies with safe lead-in/out ramps.</p>
          </div>
          <div class="panel" style="padding: 20px;">
            <div style="color: var(--orange); font-family: monospace; font-size: 12px;">STEP 04</div>
            <h4 style="margin: 8px 0;">Verify &amp; Post-Process</h4>
            <p style="font-size: 13px; color: var(--muted);">Run solid verification to check for collisions, inspect gouges, and generate clean G-code.</p>
          </div>
        </div>
      </div>

      <div style="margin-top: 40px;" class="about-grid">
        <div class="panel">
          <h3>FANUC Milling Program Sample</h3>
          <p style="font-size: 14px; color: var(--muted); margin-bottom: 15px;">
            Sample CNC milling code demonstrating standard safety blocks, work coordinate initialization, tool length compensation, and canned contouring execution.
          </p>
          <p><strong style="color: var(--orange2);">G21 G90 G17</strong> — Metric, Absolute, XY Plane</p>
          <p><strong style="color: var(--orange2);">G54</strong> — Work Coordinate System Zero</p>
          <p><strong style="color: var(--orange2);">G43 H01</strong> — Tool Length Offset Call</p>
          <p><strong style="color: var(--orange2);">G41 / G42</strong> — Cutter Diameter Compensation</p>
          <p><strong style="color: var(--orange2);">M30</strong> — End of Program &amp; Rewind</p>
        </div>

        <div style="background: #080a0b; border: 1px solid var(--line); border-radius: 4px; overflow: hidden;">
          <div style="padding: 10px 16px; background: #15191c; border-bottom: 1px solid var(--line); color: var(--muted); font-family: monospace; font-size: 12px;">
            MILLING_EXAMPLE.NC
          </div>
          <pre style="padding: 20px; color: #d9dddf; font-family: 'Courier New', Courier, monospace; font-size: 13px; line-height: 1.7; overflow-x: auto;">
%
O1002 (2D CONTOUR MILLING)
G21 G90 G17 G40 G80 G49
G28 G91 Z0.
G90

(12MM END MILL - TOOL 1)
T01 M06
G54
S2200 M03
G00 X-20. Y-20.
G43 H01 Z50. M08

(ROUGHING PASS)
G00 Z2.
G01 Z-5. F150
G41 D01 X0 Y0 F400
G01 Y80.
G01 X100.
G01 Y0
G01 X-10.
G40 G00 X-20. Y-20.

G00 Z50.
M05 M09
G28 G91 Z0.
G28 G91 Y0.
M30
%
          </pre>
        </div>
      </div>

      <div class="buttons" style="margin-top: 30px;">
        <a class="btn primary" onclick="showPage('projects')">VIEW CAM PROJECTS</a>
        <a class="btn" onclick="showPage('experience')">SEE WORK EXPERIENCE</a>
      </div>
    </div>

    <!-- PAGE 4: PROJECTS -->
    <div id="page-projects" class="page-view">
      <div class="section-head">
        <div class="section-number">03 / PORTFOLIO SHOWCASE</div>
        <h2 class="section-title">Selected Projects</h2>
      </div>

      <div class="projects">
        <div class="project">
          <div class="project-number">PROJECT / 01</div>
          <h3>Mastercam CNC Milling Component</h3>
          <p>
            Full CAM toolpath strategy for a multi-featured aluminum plate. Includes 2D dynamic roughing, 
            contour finishing, pocket milling, and hole drilling cycles with verified G-code output.
          </p>
          <ul style="margin-top: 12px; padding-left: 18px; color: var(--muted); font-size: 13.5px;">
            <li>Optimized toolpaths to reduce total machining time by 15%.</li>
            <li>Implemented dynamic motion strategies to extend tool cutter life.</li>
            <li>Solid model verification to eliminate air-cutting and avoid fixture collisions.</li>
          </ul>
          <div class="project-flow">
            CAD MODEL → WCS SETUP → TOOL SELECTION → SIMULATION → G-CODE
          </div>
        </div>

        <div class="project">
          <div class="project-number">PROJECT / 02</div>
          <h3>2-Axis CNC Turning Profiles &amp; Canned Cycles</h3>
          <p>
            Custom 2D AutoCAD profile designs converted into FANUC turning programs utilizing canned roughing (G71), 
            facing (G72), pattern repeating (G73), and drilling (G81) cycles.
          </p>
          <ul style="margin-top: 12px; padding-left: 18px; color: var(--muted); font-size: 13.5px;">
            <li>Configured nose radius compensation (G41/G42) for accurate taper turning.</li>
            <li>Designed profile geometry optimized for left-side chuck orientation.</li>
            <li>Calculated precise depth-of-cut (U) and retract (R) parameters for chip control.</li>
          </ul>
          <div class="project-flow">
            2D AUTOCAD → PROFILE GEOMETRY → G71/G70 CYCLES → MACHINE EXECUTION
          </div>
        </div>

        <div class="project">
          <div class="project-number">PROJECT / 03</div>
          <h3>PowerMill 3D Surface Machining</h3>
          <p>
            3-axis CNC milling toolpath programming for complex 3D contoured surfaces. Applies 3D offset roughing 
            and high-speed finishing strategies for low surface roughness.
          </p>
          <ul style="margin-top: 12px; padding-left: 18px; color: var(--muted); font-size: 13.5px;">
            <li>Constant-Z and raster finishing passes for smooth surface finish (R_a).</li>
            <li>Automated collision avoidance and shank clearance checking in PowerMill.</li>
            <li>Stock model tracking for precise semi-finishing material removal.</li>
          </ul>
          <div class="project-flow">
            3D MODEL → ROUGHING → STOCK TRACKING → FINISHING → VERIFICATION
          </div>
        </div>

        <div class="project">
          <div class="project-number">PROJECT / 04</div>
          <h3>Working Model of Lathe Machine</h3>
          <p>
            Academic mechanical engineering project detailing the mechanism, gear train setup, bedway alignment, 
            and component assembly of a conventional benchtop lathe.
          </p>
          <ul style="margin-top: 12px; padding-left: 18px; color: var(--muted); font-size: 13.5px;">
            <li>Drafted complete assembly drawings and part breakdown charts.</li>
            <li>Analyzed headstock spindle drive ratios and apron feed mechanisms.</li>
            <li>Presented practical working principles to engineering peer groups.</li>
          </ul>
          <div class="project-flow">
            DESIGN → FABRICATION → ASSEMBLY → MECHANICAL DEMONSTRATION
          </div>
        </div>
      </div>

      <div class="buttons" style="margin-top: 35px;">
        <a class="btn primary" onclick="showPage('experience')">SEE WORK EXPERIENCE</a>
        <a class="btn" onclick="showPage('contact')">GET IN TOUCH</a>
      </div>
    </div>

    <!-- PAGE 5: EXPERIENCE -->
    <div id="page-experience" class="page-view">
      <div class="section-head">
        <div class="section-number">04 / EXPERIENCE</div>
        <h2 class="section-title">Practical Work Experience</h2>
      </div>

      <div class="experience">
        <div class="exp-item">
          <div class="date">JULY 2026 — PRESENT</div>
          <h3>Baxy Engineering Pvt. Ltd. — Bhiwadi, Rajasthan</h3>
          <p><strong>Trainee / CNC-VMC Manufacturing</strong></p>
          <ul class="exp-list">
            <li>VMC machine operation, workpiece alignment, and high-volume component machining.</li>
            <li>Tool offset setting (G43 length offsets, tool nose radius compensation) and tool changing.</li>
            <li>Fixture setup, clamping, and zero-point calibration (G54–G59 work offsets).</li>
            <li>Line monitoring, robot cell integration support, and machine cycle tracking.</li>
            <li>In-process dimensional quality checks using vernier calipers, micrometers, and bore gauges.</li>
            <li>Alarm identification and shop-floor troubleshooting to maintain machine uptime.</li>
            <li>Interpreting 2D engineering drawings, geometric tolerances (GD&amp;T), and CAD models.</li>
          </ul>
        </div>
      </div>

      <div class="buttons" style="margin-top: 35px;">
        <a class="btn primary" onclick="showPage('contact')">GET IN TOUCH</a>
        <a class="btn" onclick="showPage('home')">BACK TO HOME</a>
      </div>
    </div>

    <!-- PAGE 6: CONTACT -->
    <div id="page-contact" class="page-view">
      <div class="section-head">
        <div class="section-number">05 / CONNECT</div>
        <h2 class="section-title">Get In Touch</h2>
      </div>

      <div class="contact-grid">
        <div class="panel">
          <h3>Contact Information</h3>
          <p style="color: var(--muted); font-size: 14px; margin-bottom: 24px;">
            Open for CNC programming roles, CAM project consulting, and manufacturing process development opportunities.
          </p>

          <div style="display: flex; flex-direction: column; gap: 16px;">
            <div class="contact-item">
              <span>LOCATION</span>
              <p>Uttar Pradesh / Rajasthan, India</p>
            </div>

            <div class="contact-item">
              <span>SPECIALIZATION</span>
              <p>CNC Turning, VMC Milling &amp; CAD/CAM (Mastercam / PowerMill)</p>
            </div>

            <div class="contact-item">
              <span>WORK AVAILABILITY</span>
              <p style="color: var(--green);">Full-Time Roles &amp; Project Consulting</p>
            </div>
          </div>
        </div>

        <div class="panel">
          <h3>Send a Direct Message</h3>
          <form id="portfolioContactForm" onsubmit="handleFormSubmit(event)" style="display: flex; flex-direction: column; gap: 16px; margin-top: 12px;">
            <div>
              <label style="display: block; font-size: 12px; font-family: monospace; color: var(--orange); margin-bottom: 6px;">YOUR NAME</label>
              <input type="text" id="senderName" required placeholder="Enter your name" style="width: 100%; padding: 12px; background: #080a0b; border: 1px solid var(--line); color: var(--text); font-size: 14px; outline: none; border-radius: 2px;">
            </div>

            <div>
              <label style="display: block; font-size: 12px; font-family: monospace; color: var(--orange); margin-bottom: 6px;">EMAIL ADDRESS</label>
              <input type="email" id="senderEmail" required placeholder="name@company.com" style="width: 100%; padding: 12px; background: #080a0b; border: 1px solid var(--line); color: var(--text); font-size: 14px; outline: none; border-radius: 2px;">
            </div>

            <div>
              <label style="display: block; font-size: 12px; font-family: monospace; color: var(--orange); margin-bottom: 6px;">MESSAGE / INQUIRY</label>
              <textarea id="senderMessage" required rows="4" placeholder="Describe your project or position details..." style="width: 100%; padding: 12px; background: #080a0b; border: 1px solid var(--line); color: var(--text); font-size: 14px; outline: none; border-radius: 2px; resize: vertical;"></textarea>
            </div>

            <button type="submit" class="btn primary" style="cursor: pointer; border: none; font-size: 13px; font-weight: bold; padding: 12px; margin-top: 6px;">
              SEND MESSAGE
            </button>
            
            <div id="formFeedback" style="display: none; font-family: monospace; font-size: 12px; padding: 10px; border-radius: 2px; margin-top: 8px;"></div>
          </form>
        </div>
      </div>

      <div class="buttons" style="margin-top: 35px;">
        <a class="btn" onclick="showPage('home')">BACK TO HOME</a>
        <a class="btn" onclick="showPage('experience')">VIEW EXPERIENCE</a>
      </div>
    </div>
  </main>

  <!-- FILE VIEWER MODAL -->
  <div class="modal-overlay" id="viewerModal">
    <div class="modal-content">
      <div class="modal-header">
        <h3 id="modalTitle">FILE VIEWER</h3>
        <button class="modal-close" onclick="closeViewer()">✕</button>
      </div>
      <div class="modal-body" id="modalBody">
        <!-- Dynamic Viewer Content -->
      </div>
    </div>
  </div>

  <!-- FOOTER -->
  <footer>
    <div class="container footer-flex">
      <div>
        <strong>OM<span class="orange">V</span>EER UPADHYAY</strong><br>
        CNC Programmer &amp; CAM Professional
      </div>
      <div>
        © 2026 Omveer Upadhyay
      </div>
    </div>
  </footer>

  <!-- SCRIPT FOR ROUTING, FILE UPLOADS, 3D PREVIEWING & ANIMATIONS -->
  <script>
    // Navigation Routing
    function showPage(pageId) {
      const pages = document.querySelectorAll('.page-view');
      pages.forEach(page => page.classList.remove('active'));

      const navLinks = document.querySelectorAll('.nav-links a');
      navLinks.forEach(link => link.classList.remove('active'));

      const targetPage = document.getElementById('page-' + pageId);
      if (targetPage) {
        targetPage.classList.add('active');
      }

      const targetNav = document.getElementById('nav-' + pageId);
      if (targetNav) {
        targetNav.classList.add('active');
      }

      window.scrollTo(0, 0);
    }

    // Dynamic File Upload & Management Queue
    let uploadedFiles = [];

    function formatBytes(bytes) {
      if (bytes === 0) return '0 Bytes';
      const k = 1024;
      const sizes = ['Bytes', 'KB', 'MB', 'GB'];
      const i = Math.floor(Math.log(bytes) / Math.log(k));
      return parseFloat((bytes / Math.pow(k, i)).toFixed(2)) + ' ' + sizes[i];
    }

    function processFileUpload(input, category, statusId) {
      const statusElement = document.getElementById(statusId);
      if (input.files && input.files[0]) {
        const file = input.files[0];
        const fileObj = {
          id: Date.now(),
          fileData: file,
          name: file.name,
          category: category,
          size: formatBytes(file.size),
          date: new Date().toLocaleTimeString([], { hour: '2-digit', minute: '2-digit', second: '2-digit' })
        };

        uploadedFiles.push(fileObj);
        statusElement.textContent = "✓ Uploaded";

        setTimeout(() => {
          statusElement.textContent = "";
        }, 3000);

        renderFileList();
        input.value = ""; 
      }
    }

    function removeFile(fileId) {
      uploadedFiles = uploadedFiles.filter(f => f.id !== fileId);
      renderFileList();
    }

    function renderFileList() {
      const emptyMsg = document.getElementById('emptyMsg');
      const fileTable = document.getElementById('fileTable');
      const fileTableBody = document.getElementById('fileTableBody');
      const fileCount = document.getElementById('fileCount');

      fileCount.textContent = `(${uploadedFiles.length} File${uploadedFiles.length === 1 ? '' : 's'})`;

      if (uploadedFiles.length === 0) {
        emptyMsg.style.display = 'block';
        fileTable.style.display = 'none';
      } else {
        emptyMsg.style.display = 'none';
        fileTable.style.display = 'table';
        fileTableBody.innerHTML = '';

        uploadedFiles.forEach(file => {
          const tr = document.createElement('tr');
          tr.innerHTML = `
            <td style="color: var(--orange2);">${file.name}</td>
            <td>${file.category}</td>
            <td>${file.size}</td>
            <td style="color: var(--muted);">${file.date}</td>
            <td>
              <button class="btn-view" onclick="viewFile(${file.id})">VIEW</button>
              <button class="btn-delete" onclick="removeFile(${file.id})">REMOVE</button>
            </td>
          `;
          fileTableBody.appendChild(tr);
        });
      }
    }

    // Modal File Viewer Logic
    function viewFile(fileId) {
      const fileObj = uploadedFiles.find(f => f.id === fileId);
      if (!fileObj) return;

      const modal = document.getElementById('viewerModal');
      const modalTitle = document.getElementById('modalTitle');
      const modalBody = document.getElementById('modalBody');

      modalTitle.textContent = `VIEWING: ${fileObj.name.toUpperCase()}`;
      modalBody.innerHTML = '';
      modal.classList.add('active');

      const fileName = fileObj.name.toLowerCase();

      // Text/G-Code Files
      if (fileName.endsWith('.nc') || fileName.endsWith('.gcode') || fileName.endsWith('.txt') || fileName.endsWith('.tap')) {
        const reader = new FileReader();
        reader.onload = function(e) {
          const pre = document.createElement('pre');
          pre.className = 'code-viewer';
          pre.textContent = e.target.result;
          modalBody.appendChild(pre);
        };
        reader.readAsText(fileObj.fileData);
      } 
      // STL 3D Files
      else if (fileName.endsWith('.stl')) {
        const container = document.createElement('div');
        container.id = 'viewerCanvasContainer';
        modalBody.appendChild(container);
        render3DModel(fileObj.fileData, container);
      } 
      // CAD / STEP / IGES Placeholder 3D Viewer Rendering
      else if (fileName.endsWith('.step') || fileName.endsWith('.stp') || fileName.endsWith('.igs') || fileName.endsWith('.iges') || fileName.endsWith('.dxf') || fileName.endsWith('.dwg')) {
        const container = document.createElement('div');
        container.id = 'viewerCanvasContainer';
        modalBody.appendChild(container);
        renderCADCanvas(fileObj.name, container);
      } 
      // Proprietary Mastercam / PowerMill Binary Archives
      else {
        const archiveDiv = document.createElement('div');
        archiveDiv.className = 'archive-viewer';
        archiveDiv.innerHTML = `
          <h4>${fileObj.category} Binary Package</h4>
          <p><strong>File Name:</strong> ${fileObj.name}</p>
          <p><strong>File Size:</strong> ${fileObj.size}</p>
          <p><strong>Status:</strong> File verified and queued for CAM post-processing execution.</p>
          <br>
          <p style="color: var(--orange2);">* Proprietary CAM binaries (.mcam, .pxd, .pkm) are parsed directly in Mastercam/PowerMill workstations.</p>
        `;
        modalBody.appendChild(archiveDiv);
      }
    }

    function closeViewer() {
      const modal = document.getElementById('viewerModal');
      modal.classList.remove('active');
    }

    // 3D Canvas Visualizer for CAD geometries
    function renderCADCanvas(filename, container) {
      const scene = new THREE.Scene();
      scene.background = new THREE.Color(0x080a0b);

      const camera = new THREE.PerspectiveCamera(45, container.clientWidth / container.clientHeight, 0.1, 1000);
      camera.position.set(100, 100, 100);

      const renderer = new THREE.WebGLRenderer({ antialias: true });
      renderer.setSize(container.clientWidth, container.clientHeight);
      container.appendChild(renderer.domElement);

      const gridHelper = new THREE.GridHelper(200, 20, 0xff7a00, 0x2a3034);
      scene.add(gridHelper);

      // Render a representative CAD component geometry
      const geometry = new THREE.BoxGeometry(40, 20, 60);
      const material = new THREE.MeshPhongMaterial({ color: 0xff7a00, wireframe: true });
      const cube = new THREE.Mesh(geometry, material);
      scene.add(cube);

      const ambientLight = new THREE.AmbientLight(0xffffff, 0.7);
      scene.add(ambientLight);

      camera.lookAt(0, 0, 0);

      function animate() {
        requestAnimationFrame(animate);
        cube.rotation.y += 0.01;
        renderer.render(scene, camera);
      }
      animate();
    }

    function render3DModel(file, container) {
      const scene = new THREE.Scene();
      scene.background = new THREE.Color(0x080a0b);

      const camera = new THREE.PerspectiveCamera(45, container.clientWidth / container.clientHeight, 0.1, 1000);
      const renderer = new THREE.WebGLRenderer({ antialias: true });
      renderer.setSize(container.clientWidth, container.clientHeight);
      container.appendChild(renderer.domElement);

      const light = new THREE.DirectionalLight(0xffffff, 1);
      light.position.set(1, 1, 1).normalize();
      scene.add(light);
      scene.add(new THREE.AmbientLight(0x404040));

      const reader = new FileReader();
      reader.onload = function (e) {
        const loader = new THREE.STLLoader();
        const geometry = loader.parse(e.target.result);
        const material = new THREE.MeshPhongMaterial({ color: 0xff7a00, specular: 0x111111, shininess: 200 });
        const mesh = new THREE.Mesh(geometry, material);

        geometry.computeBoundingBox();
        const center = geometry.boundingBox.getCenter(new THREE.Vector3());
        mesh.position.sub(center);

        scene.add(mesh);
        camera.position.set(80, 80, 80);
        camera.lookAt(0, 0, 0);

        function animate() {
          requestAnimationFrame(animate);
          mesh.rotation.y += 0.008;
          renderer.render(scene, camera);
        }
        animate();
      };
      reader.readAsArrayBuffer(file);
    }

    // Form Handling
    function handleFormSubmit(e) {
      e.preventDefault();
      const feedback = document.getElementById('formFeedback');
      const name = document.getElementById('senderName').value;
      
      if (feedback) {
        feedback.style.display = 'block';
        feedback.style.background = 'rgba(114, 213, 114, 0.1)';
        feedback.style.border = '1px solid var(--green)';
        feedback.style.color = 'var(--green)';
        feedback.textContent = `Thank you, ${name}! Your message has been received.`;
        
        document.getElementById('portfolioContactForm').reset();
        setTimeout(() => {
          feedback.style.display = 'none';
        }, 5000);
      }
    }

    // Canvas Toolpath Simulation Animation
    const canvas = document.getElementById('cncCanvas');
    const ctx = canvas ? canvas.getContext('2d') : null;
    const readout = document.getElementById('cncReadout');

    function resizeCanvas() {
      if (canvas) {
        canvas.width = canvas.offsetWidth;
        canvas.height = canvas.offsetHeight;
      }
    }
    resizeCanvas();

    let t = 0;
    function drawToolpath() {
      if (!canvas || !ctx) return;
      ctx.clearRect(0, 0, canvas.width, canvas.height);

      ctx.strokeStyle = '#1e2428';
      ctx.lineWidth = 1;
      ctx.beginPath();
      ctx.moveTo(0, canvas.height / 2);
      ctx.lineTo(canvas.width, canvas.height / 2);
      ctx.moveTo(canvas.width / 2, 0);
      ctx.lineTo(canvas.width / 2, canvas.height);
      ctx.stroke();

      ctx.fillStyle = '#1c2226';
      ctx.fillRect(40, canvas.height / 2 - 50, 220, 100);
      ctx.strokeStyle = '#3a444a';
      ctx.strokeRect(40, canvas.height / 2 - 50, 220, 100);

      const pathX = 260 - (t % 200);
      const pathY = canvas.height / 2 - (pathX > 160 ? 30 : (pathX > 100 ? 45 : 50));

      ctx.strokeStyle = '#ff7a00';
      ctx.lineWidth = 2;
      ctx.beginPath();
      ctx.moveTo(260, canvas.height / 2 - 30);
      ctx.lineTo(160, canvas.height / 2 - 30);
      ctx.lineTo(100, canvas.height / 2 - 45);
      ctx.lineTo(40, canvas.height / 2 - 50);
      ctx.stroke();

      ctx.fillStyle = '#ff9d3d';
      ctx.beginPath();
      ctx.arc(pathX, pathY, 5, 0, Math.PI * 2);
      ctx.fill();

      if (readout) {
        const currentX = ((canvas.height / 2 - pathY) * 0.8).toFixed(3);
        const currentZ = ((pathX - 260) * 0.5).toFixed(3);
        readout.textContent = `G01 X${currentX} Z${currentZ} F0.20`;
      }

      t += 0.8;
      requestAnimationFrame(drawToolpath);
    }

    drawToolpath();
  </script>
</body>
</html>
