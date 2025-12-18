# -<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <title>Product Management App</title>
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <style>
    :root{
      --bg:#0f1724;
      --card:#0b1220;
      --muted:#9aa4b2;
      --accent:#38bdf8;
      --accent-2:#60a5fa;
      --success:#16a34a;
      --danger:#ef4444;
      --glass: rgba(255,255,255,0.03);
    }
    *{box-sizing:border-box;font-family:Inter,Inter var,Segoe UI,Roboto,"Helvetica Neue",Arial;}
    body{
      margin:0;
      min-height:100vh;
      background:linear-gradient(180deg,#071127 0%, #071727 100%);
      color:#e6eef8;
      display:flex;
      align-items:flex-start;
      justify-content:center;
      padding:32px;
    }
    .container{
      width:100%;
      max-width:900px;
      background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));
      border-radius:12px;
      padding:22px;
      box-shadow: 0 10px 30px rgba(2,6,23,0.6);
      border:1px solid rgba(255,255,255,0.03);
    }
    h1{
      margin:0 0 14px 0;
      font-size:20px;
      letter-spacing:0.2px;
    }
    form{
      display:flex;
      gap:10px;
      align-items:center;
      margin-bottom:18px;
      flex-wrap:wrap;
    }
    input[type="text"]{
      flex:1 1 280px;
      padding:10px 12px;
      border-radius:8px;
      border:1px solid rgba(255,255,255,0.06);
      background:var(--glass);
      color:inherit;
      outline:none;
      min-width:0;
    }
    button{
      padding:10px 14px;
      border-radius:8px;
      border:0;
      cursor:pointer;
      font-weight:600;
      background:linear-gradient(90deg,var(--accent),var(--accent-2));
      color:#05202b;
      box-shadow: 0 6px 18px rgba(56,189,248,0.12);
    }
    button.secondary{
      background:transparent;
      border:1px solid rgba(255,255,255,0.04);
      color:var(--muted);
      box-shadow:none;
      font-weight:600;
    }
    .note{
      font-size:13px;
      color:var(--muted);
      margin-bottom:10px;
    }
    table{
      width:100%;
      border-collapse:collapse;
      background:transparent;
      margin-top:6px;
    }
    thead th{
      text-align:left;
      padding:10px 12px;
      font-size:13px;
      color:var(--muted);
      border-bottom:1px solid rgba(255,255,255,0.03);
    }
    tbody td{
      padding:10px 12px;
      border-bottom:1px dashed rgba(255,255,255,0.02);
      vertical-align:middle;
    }
    .actions button{
      margin-right:8px;
      padding:6px 9px;
      border-radius:8px;
      border:0;
      cursor:pointer;
      font-size:13px;
    }
    .actions .edit{
      background:rgba(96,165,250,0.12);
      color:var(--accent-2);
      border:1px solid rgba(96,165,250,0.08);
    }
    .actions .delete{
      background:rgba(239,68,68,0.08);
      color:var(--danger);
      border:1px solid rgba(239,68,68,0.06);
    }
    .empty{
      padding:14px;
      text-align:center;
      color:var(--muted);
    }
    .status{
      margin-top:12px;
      font-size:13px;
      color:var(--muted);
    }
    @media (max-width:560px){
      .actions button{ margin-bottom:6px; display:inline-block; }
      form{ gap:8px; }
    }
  </style>
</head>
<body>
  <div class="container" role="main">
    <h1>Product Management App</h1>

    <p class="note">Add, edit and delete products stored in your Supabase database. Replace the Supabase URL and Key below with your own project values.</p>

    <form id="product-form" onsubmit="return false;">
      <input id="product-name" type="text" placeholder="Enter product name" aria-label="Product name" required />
      <button id="add-btn" type="button">Add Product</button>
      <button id="refresh-btn" type="button" class="secondary">Refresh</button>
    </form>

    <div class="status" id="status">Loading products…</div>

    <table aria-label="Products table" id="products-table" style="display:none;">
      <thead>
        <tr>
          <th style="width:60%;">Product Name</th>
          <th style="width:40%;">Actions</th>
        </tr>
      </thead>
      <tbody id="products-tbody">
        <!-- rows injected here -->
      </tbody>
    </table>

    <div id="empty" class="empty" style="display:none;">No products yet.</div>

    <p class="note" style="margin-top:18px;font-size:12px;">
      <strong>Supabase connection snippet included below (replace placeholders):</strong>
    </p>

    <pre id="supabase-snippet" style="background:rgba(0,0,0,0.12);padding:10px;border-radius:6px;font-size:13px;white-space:pre-wrap;">
const { createClient } = supabase;

const supabaseUrl = 'https://your-supabase-url.supabase.co';  // Replace with your Supabase URL
const supabaseKey = 'your-anon-key';  // Replace with your Supabase Key 
const supabaseClient = createClient(supabaseUrl, supabaseKey);
    </pre>
  </div>

  <!-- Supabase JS (UMD bundle) -->
  <script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js/dist/umd/supabase.min.js"></script>

  <script>
    // -------------------------------
    // Supabase connection (edit these)
    // -------------------------------
    // The following lines follow the structure you requested:
    const { createClient } = supabase;

    // TODO: Replace these placeholders with your actual Supabase project details:
    const supabaseUrl = 'https://rrqppzwgqzqniplrefxw.supabase.co';  // Replace with your Supabase URL
    const supabaseKey = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6InJycXBwendncXpxbmlwbHJlZnh3Iiwicm9sZSI6ImFub24iLCJpYXQiOjE3NjYwNjQ4NzYsImV4cCI6MjA4MTY0MDg3Nn0._8s6Qo-_CQ29cc2GSmHm-Vk7E0IiGuhGfiK8-dE8ues';  // Replace with your Supabase Key

    // Create the Supabase client
    const supabaseClient = createClient(supabaseUrl, supabaseKey);

    // -------------------------------
    // App behavior
    // -------------------------------
    const form = document.getElementById('product-form');
    const input = document.getElementById('product-name');
    const addBtn = document.getElementById('add-btn');
    const refreshBtn = document.getElementById('refresh-btn');
    const statusEl = document.getElementById('status');
    const table = document.getElementById('products-table');
    const tbody = document.getElementById('products-tbody');
    const emptyEl = document.getElementById('empty');

    // Table name in your Supabase DB
    const TABLE = 'products';

    // Initialize
    document.addEventListener('DOMContentLoaded', () => {
      fetchProducts();
    });

    addBtn.addEventListener('click', addProduct);
    refreshBtn.addEventListener('click', fetchProducts);

    async function setStatus(msg, isError = false) {
      statusEl.textContent = msg;
      statusEl.style.color = isError ? '#ffb4b4' : '';
    }

    async function fetchProducts() {
      setStatus('Loading products…');
      // Hide table while loading
      table.style.display = 'none';
      emptyEl.style.display = 'none';
      tbody.innerHTML = '';

      try {
        const { data, error } = await supabaseClient
          .from(TABLE)
          .select('id, name')
          .order('id', { ascending: true });

        if (error) throw error;

        if (!data || data.length === 0) {
          emptyEl.style.display = 'block';
          setStatus('No products found.');
          return;
        }

        renderTable(data);
        setStatus('Products loaded.');
      } catch (err) {
        console.error('Fetch error:', err);
        setStatus('Failed to load products. See console for details.', true);
      }
    }

    function renderTable(items) {
      tbody.innerHTML = '';
      for (const row of items) {
        const tr = document.createElement('tr');

        const nameTd = document.createElement('td');
        nameTd.textContent = row.name;
        tr.appendChild(nameTd);

        const actionsTd = document.createElement('td');
        actionsTd.className = 'actions';

        const editBtn = document.createElement('button');
        editBtn.className = 'edit';
        editBtn.textContent = 'Edit';
        editBtn.addEventListener('click', () => handleEdit(row.id, row.name));
        actionsTd.appendChild(editBtn);

        const delBtn = document.createElement('button');
        delBtn.className = 'delete';
        delBtn.textContent = 'Delete';
        delBtn.addEventListener('click', () => handleDelete(row.id, row.name));
        actionsTd.appendChild(delBtn);

        tr.appendChild(actionsTd);
        tbody.appendChild(tr);
      }
      table.style.display = '';
      emptyEl.style.display = 'none';
    }

    async function addProduct() {
      const name = input.value.trim();
      if (!name) {
        alert('Please enter a product name.');
        return;
      }

      addBtn.disabled = true;
      addBtn.textContent = 'Adding…';

      try {
        const { data, error } = await supabaseClient
          .from(TABLE)
          .insert([{ name }]);

        if (error) throw error;

        input.value = '';
        setStatus('Product added.');
        // Optionally, re-fetch to get latest list
        await fetchProducts();
      } catch (err) {
        console.error('Insert error:', err);
        setStatus('Failed to add product. See console for details.', true);
        alert('Error adding product: ' + (err.message || err.toString()));
      } finally {
        addBtn.disabled = false;
        addBtn.textContent = 'Add Product';
      }
    }

    async function handleEdit(id, currentName) {
      // Use a simple prompt for editing. You can replace with a modal or inline edit if desired.
      const newName = prompt('Edit product name:', currentName);
      if (newName === null) return; // cancelled
      const trimmed = newName.trim();
      if (!trimmed) {
        alert('Product name cannot be empty.');
        return;
      }

      try {
        setStatus('Updating product…');

        const { data, error } = await supabaseClient
          .from(TABLE)
          .update({ name: trimmed })
          .eq('id', id);

        if (error) throw error;

        setStatus('Product updated.');
        await fetchProducts();
      } catch (err) {
        console.error('Update error:', err);
        setStatus('Failed to update product. See console for details.', true);
        alert('Error updating product: ' + (err.message || err.toString()));
      }
    }

    async function handleDelete(id, name) {
      const ok = confirm(`Delete product "${name}"? This action cannot be undone.`);
      if (!ok) return;

      try {
        setStatus('Deleting product…');

        const { data, error } = await supabaseClient
          .from(TABLE)
          .delete()
          .eq('id', id);

        if (error) throw error;

        setStatus('Product deleted.');
        await fetchProducts();
      } catch (err) {
        console.error('Delete error:', err);
        setStatus('Failed to delete product. See console for details.', true);
        alert('Error deleting product: ' + (err.message || err.toString()));
      }
    }

    // Helpful: expose functions for debugging in console
    window._pm = {
      fetchProducts, addProduct, handleEdit, handleDelete, supabaseClient
    };
  </script>
</body>
</html>
