<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Service Manager – Personal</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />

  <style>
    :root {
      --primary-dark: #5B4636;
      --primary: #8C705E;
      --primary-light: #DCC6A3;

      --bg: #F4EDE3;
      --card-bg: #FAF7F3;

      --border: #CBBBA4;

      --text-main: #3C2F2F;
      --text-muted: #7C6A59;

      --danger: #9E4F3A;
      --accent-soft: #EFE1CF;
      --signature-bg: #FFF9C6;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", system-ui, sans-serif;
    }

    body {
      background: var(--bg);
      color: var(--text-main);
      min-height: 100vh;
      display: flex;
      flex-direction: column;
    }

    header {
      background: linear-gradient(90deg, var(--primary-dark), var(--primary));
      color: #FAF7F3;
      padding: 10px 14px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      box-shadow: 0 2px 6px rgba(60, 47, 47, 0.25);
    }

    header .title {
      font-size: 17px;
      font-weight: 600;
      letter-spacing: 0.04em;
      text-transform: uppercase;
    }

    header .subtitle {
      font-size: 13px;
      opacity: 0.95;
    }

    main {
      flex: 1;
      padding: 10px;
      max-width: 980px;
      width: 100%;
      margin: 0 auto;
    }

    .card {
      background: var(--card-bg);
      border-radius: 6px;
      border: 1px solid var(--border);
      box-shadow: 0 1px 3px rgba(91, 70, 54, 0.16);
      margin-bottom: 10px;
    }

    .card-header {
      padding: 10px 12px;
      border-bottom: 1px solid var(--border);
      background: #F0E5D6;
      display: flex;
      align-items: center;
      justify-content: space-between;
    }

    .card-title {
      font-size: 15px;
      font-weight: 600;
    }

    .card-body {
      padding: 10px 12px 12px;
    }

    .btn {
      display: inline-flex;
      align-items: center;
      justify-content: center;
      border-radius: 4px;
      border: 1px solid transparent;
      padding: 6px 14px;
      font-size: 14px;
      cursor: pointer;
      text-decoration: none;
      background: #E4D8C9;
      color: var(--text-main);
      transition: background 0.12s, box-shadow 0.12s, transform 0.08s;
    }

    .btn-primary {
      background: var(--primary);
      border-color: var(--primary-dark);
      color: #FAF7F3;
    }

    .btn-primary:hover {
      background: var(--primary-dark);
      transform: translateY(-1px);
      box-shadow: 0 2px 6px rgba(60, 47, 47, 0.32);
    }

    .btn-secondary {
      background: #FAF7F3;
      border-color: var(--border);
      color: var(--text-main);
    }

    .btn-danger {
      background: #FAF7F3;
      border-color: var(--danger);
      color: var(--danger);
    }

    .btn-sm {
      padding: 4px 8px;
      font-size: 12px;
    }

    .btn + .btn {
      margin-left: 6px;
    }

    .menu-list button {
      width: 100%;
      justify-content: flex-start;
      margin-bottom: 8px;
    }

    .menu-list button span {
      margin-left: 6px;
    }

    .field-group {
      display: flex;
      flex-direction: column;
      margin-bottom: 8px;
    }

    .field-group label {
      font-size: 12px;
      color: var(--text-muted);
      margin-bottom: 2px;
    }

    .field-group input,
    .field-group textarea,
    .field-group select {
      border-radius: 4px;
      border: 1px solid var(--border);
      padding: 6px 8px;
      font-size: 14px;
      background: #FFFDF9;
      color: var(--text-main);
    }

    .field-group textarea {
      min-height: 60px;
      resize: vertical;
    }

    .field-group input:focus,
    .field-group textarea:focus,
    .field-group select:focus {
      outline: none;
      border-color: var(--primary);
      box-shadow: 0 0 0 1px rgba(140, 112, 94, 0.35);
    }

    .grid-2 {
      display: grid;
      grid-template-columns: repeat(2, minmax(0, 1fr));
      gap: 8px;
    }

    .section-title {
      font-size: 13px;
      font-weight: 600;
      margin: 6px 0 4px;
      color: var(--text-main);
    }

    .hint {
      font-size: 11px;
      color: var(--text-muted);
      margin-top: 4px;
    }

    table {
      width: 100%;
      border-collapse: collapse;
      font-size: 13px;
    }

    th, td {
      padding: 6px 6px;
      border-bottom: 1px solid var(--border);
      text-align: left;
      vertical-align: top;
    }

    th {
      background: var(--accent-soft);
      font-weight: 600;
      color: var(--text-main);
    }

    tr:last-child td {
      border-bottom: none;
    }

    .status-tag {
      display: inline-block;
      padding: 2px 6px;
      border-radius: 20px;
      background: #EDDFCD;
      color: var(--primary-dark);
      font-size: 11px;
    }

    .badge-id {
      font-family: "SF Mono", ui-monospace, Menlo, Monaco, monospace;
      font-size: 11px;
      color: var(--text-muted);
    }

    .search-row {
      display: flex;
      gap: 6px;
      margin-bottom: 8px;
    }

    .search-row input {
      flex: 1;
    }

    /* Parts modal */
    .modal {
      position: fixed;
      inset: 0;
      background: rgba(0,0,0,0.35);
      display: none;
      align-items: center;
      justify-content: center;
      z-index: 20;
    }

    .modal.show {
      display: flex;
    }

    .modal-content {
      background: #FFFFFF;
      border-radius: 6px;
      border: 1px solid var(--border);
      width: 95%;
      max-width: 480px;
      box-shadow: 0 6px 18px rgba(0,0,0,0.3);
    }

    .modal-header {
      background: #F0E5D6;
      padding: 8px 12px;
      border-bottom: 1px solid var(--border);
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    .modal-header h3 {
      font-size: 14px;
      font-weight: 600;
    }

    .modal-body {
      padding: 10px 12px 12px;
    }

    .modal-footer {
      padding: 8px 12px 12px;
      text-align: right;
    }

    .close-x {
      cursor: pointer;
      font-size: 18px;
      color: var(--text-muted);
    }

    /* Signature */
    #signatureCanvas {
      width: 100%;
      max-width: 100%;
      border-radius: 4px;
      border: 1px solid var(--border);
      background: var(--signature-bg);
      touch-action: none;
    }

    .signature-toolbar {
      display: flex;
      justify-content: flex-end;
      margin-bottom: 4px;
      gap: 6px;
    }

    /* Photos */
    .photos-grid {
      display: flex;
      flex-wrap: wrap;
      gap: 6px;
      margin-top: 6px;
    }

    .photo-thumb {
      position: relative;
      width: 90px;
      height: 90px;
      border-radius: 4px;
      overflow: hidden;
      border: 1px solid var(--border);
      background: #E0D4C4;
    }

    .photo-thumb img {
      width: 100%;
      height: 100%;
      object-fit: cover;
    }

    .photo-remove {
      position: absolute;
      top: 2px;
      right: 2px;
      background: rgba(0,0,0,0.55);
      color: #fff;
      border: none;
      border-radius: 50%;
      width: 18px;
      height: 18px;
      font-size: 12px;
      cursor: pointer;
      line-height: 18px;
      text-align: center;
    }

    @media (max-width: 640px) {
      main {
        padding: 8px 6px 10px;
      }
      .grid-2 {
        grid-template-columns: 1fr;
      }
      header .subtitle {
        display: none;
      }
    }
  </style>
</head>

<body>
  <header>
    <div>
      <div class="title">SERVICE MANAGER</div>
      <div class="subtitle">Personal use • Offline tool</div>
    </div>
    <div style="font-size:13px;">Welcome: MAX</div>
  </header>

  <main>
    <!-- MAIN MENU -->
    <section id="view-menu" class="card">
      <div class="card-header">
        <div class="card-title">Main Menu</div>
      </div>
      <div class="card-body">
        <div class="menu-list">
          <button class="btn btn-primary" onclick="openNewCall()">
            ➕ <span>New Service Call</span>
          </button>
          <button class="btn btn-secondary" onclick="showView('list')">
            📋 <span>Service List</span>
          </button>
          <button class="btn btn-secondary" onclick="showView('search')">
            🔍 <span>Search</span>
          </button>
        </div>
        <div class="hint">
          Данные хранятся в браузере (localStorage). Никакого сервера, только для личного пользования.
        </div>
      </div>
    </section>

    <!-- NEW / EDIT SERVICE CALL -->
    <section id="view-form" class="card" style="display:none;">
      <div class="card-header">
        <div class="card-title" id="form-title">New Service Call</div>
        <div>
          <button class="btn btn-secondary btn-sm" onclick="backToMenu()">Back</button>
        </div>
      </div>
      <div class="card-body">
        <form id="serviceForm" onsubmit="saveCall(event)">
          <input type="hidden" id="callId" />

          <div class="section-title">Customer Info</div>
          <div class="grid-2">
            <div class="field-group">
              <label for="customerName">Name</label>
              <input id="customerName" type="text" autocomplete="off" />
            </div>
            <div class="field-group">
              <label for="customerPhone">Phone</label>
              <input id="customerPhone" type="tel" autocomplete="off" />
            </div>
          </div>
          <div class="field-group">
            <label for="customerAddress">Address</label>
            <input id="customerAddress" type="text" autocomplete="off" />
          </div>

          <div class="section-title" style="margin-top:10px;">Service Info</div>
          <div class="field-group">
            <label for="techNotes">Tech Notes</label>
            <textarea id="techNotes"></textarea>
          </div>
          <div class="field-group">
            <label for="complaint">Complaint</label>
            <textarea id="complaint"></textarea>
          </div>
          <div class="field-group">
            <label for="description">Description (for yourself)</label>
            <textarea id="description"></textarea>
          </div>
          <div class="grid-2">
            <div class="field-group">
              <label for="dealer">Dealer</label>
              <input id="dealer" type="text" />
            </div>
            <div class="field-group">
              <label for="source">Source</label>
              <input id="source" type="text" />
            </div>
          </div>

          <div class="section-title" style="margin-top:10px;">Appliance Info</div>
          <div class="field-group">
            <label for="applType">Appl Type</label>
            <input id="applType" type="text" placeholder="Washer / Dryer / Oven / etc." />
          </div>
          <div class="grid-2">
            <div class="field-group">
              <label for="make">Make</label>
              <input id="make" type="text" />
            </div>
            <div class="field-group">
              <label for="model">Model#</label>
              <input id="model" type="text" />
            </div>
          </div>
          <div class="grid-2">
            <div class="field-group">
              <label for="serial">Serial#</label>
              <input id="serial" type="text" />
            </div>
            <div class="field-group">
              <label for="mfg">Mfg#</label>
              <input id="mfg" type="text" />
            </div>
          </div>

          <div class="grid-2" style="margin-top:10px;">
            <div class="field-group">
              <label for="status">Status</label>
              <select id="status">
                <option value="open">Open</option>
                <option value="scheduled">Scheduled</option>
                <option value="completed">Completed</option>
                <option value="cancelled">Cancelled</option>
              </select>
            </div>
            <div class="field-group">
              <label for="callDate">Call Date</label>
              <input id="callDate" type="date" />
            </div>
          </div>

          <!-- PARTS -->
          <div class="section-title" style="margin-top:12px;">Parts</div>
          <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:4px;">
            <div class="hint">Список запчастей для этого вызова.</div>
            <button type="button" class="btn btn-secondary btn-sm" onclick="openPartsModal()">Add Part</button>
          </div>
          <div id="parts-table-wrapper" class="hint">No parts yet.</div>

          <!-- SIGNATURE -->
          <div class="section-title" style="margin-top:12px;">Signature</div>
          <div class="signature-toolbar">
            <button type="button" class="btn btn-secondary btn-sm" onclick="clearSignature()">Clear</button>
          </div>
          <canvas id="signatureCanvas" height="160"></canvas>
          <div class="hint">Подпись клиента или свои заметки. Рисуй пальцем / мышкой.</div>

          <!-- PHOTOS -->
          <div class="section-title" style="margin-top:12px;">Photos</div>
          <button type="button" class="btn btn-secondary btn-sm" onclick="triggerPhotoInput()">Add Photo</button>
          <input id="photoInput" type="file" accept="image/*" multiple style="display:none" />
          <div id="photos-wrapper" class="photos-grid"></div>
          <div class="hint">Фото повреждений, серийника, платы и т.п.</div>

          <div style="margin-top:14px; display:flex; justify-content:flex-end;">
            <button type="button" class="btn btn-secondary" onclick="backToMenu()">Cancel</button>
            <button type="submit" class="btn btn-primary">Save</button>
          </div>
        </form>
      </div>
    </section>

    <!-- SERVICE LIST -->
    <section id="view-list" class="card" style="display:none;">
      <div class="card-header">
       
