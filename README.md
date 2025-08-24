<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Sky Store — Luxury Black & Gold</title>
<style>
  :root{
    --gold:#FFD700;
    --gold-dark:#d9b600;
    --black:#0d0d0d;
    --ink:#000;
    --card:#141414;
    --muted:#cfcfcf;
  }
  *{box-sizing:border-box}
  body{margin:0;font-family:system-ui,-apple-system,Segoe UI,Roboto,Arial,sans-serif;background:var(--gold);color:var(--ink);}
  /* Header */
  .header{
    position:sticky;top:0;z-index:30;
    background:var(--black);color:var(--gold);
    padding:12px 16px;border-bottom:1px solid rgba(255,215,0,.2);
    display:grid;grid-template-columns:auto 1fr auto;gap:12px;align-items:center;
  }
  .back-btn{color:var(--gold);text-decoration:none;font-weight:700;cursor:pointer}
  .brand{text-align:center;font-weight:700;letter-spacing:.3px}
  .actions{display:flex;gap:10px;align-items:center;justify-content:flex-end}
  .search{
    grid-column:1/-1;margin-top:8px;display:flex;gap:8px;
  }
  .search input{
    flex:1;padding:10px 12px;border-radius:12px;border:1px solid rgba(255,215,0,.35);
    background:#111;color:#fff;outline:none;
  }
  .search input::placeholder{color:#aaa}
  .pill-btn{
    padding:10px 14px;border-radius:999px;border:1px solid var(--gold);
    color:var(--gold);background:transparent;cursor:pointer;font-weight:600;
  }
  /* Slider placeholder */
  .slider{
    margin:14px auto;max-width:1100px;border-radius:16px;overflow:hidden;
    border:2px solid var(--black);box-shadow:0 8px 24px rgba(0,0,0,.15);
  }
  .slider img{width:100%;display:block}
  /* Grid produk */
  .wrap{max-width:1200px;margin:0 auto;padding:12px}
  .grid{
    display:grid;gap:14px;
    grid-template-columns:repeat(2,minmax(0,1fr));
  }
  @media (min-width:640px){.grid{grid-template-columns:repeat(3,1fr)}}
  @media (min-width:992px){.grid{grid-template-columns:repeat(4,1fr)}}
  .card{
    background:var(--card);border:2px solid var(--black);border-radius:14px;
    overflow:hidden;color:#fff;box-shadow:0 8px 16px rgba(0,0,0,.2);
    transition:transform .15s ease, box-shadow .2s ease, border-color .2s ease;
    cursor:pointer;
  }
  .card:hover{transform:translateY(-3px);box-shadow:0 14px 28px rgba(0,0,0,.28);border-color:var(--gold-dark)}
  .card img{width:100%;aspect-ratio:1/1;object-fit:cover;background:#000}
  .card .info{padding:10px 12px}
  .name{font-size:13px;color:#eaeaea;line-height:1.3;margin:0 0 6px}
  .row{display:flex;gap:8px;align-items:center;justify-content:space-between}
  .price{
    display:inline-flex;align-items:center;gap:6px;
    background:var(--gold);color:var(--ink);
    font-weight:800;padding:6px 10px;border-radius:999px;font-size:13px;
    border:1px solid var(--gold-dark);
  }
  .cta-mini{
    background:var(--gold);color:var(--ink);border:1px solid var(--gold-dark);
    padding:6px 10px;border-radius:999px;font-size:12px;font-weight:700;
  }
  /* Modal */
  .modal-backdrop{
    position:fixed;inset:0;background:rgba(0,0,0,.6);display:none;align-items:center;justify-content:center;z-index:50;
  }
  .modal{
    width:min(92vw,520px);background:var(--card);border:2px solid var(--gold-dark);border-radius:16px;overflow:hidden;color:#fff;
    box-shadow:0 18px 40px rgba(0,0,0,.45);
  }
  .modal header{display:flex;justify-content:space-between;align-items:center;padding:10px 12px;border-bottom:1px solid rgba(255,215,0,.2)}
  .modal header h3{margin:0;font-size:16px;color:#fff}
  .modal .close{background:#0000;border:1px solid var(--gold);color:var(--gold);border-radius:999px;padding:6px 10px;cursor:pointer}
  .modal .body{padding:12px}
  .modal .body img{width:100%;border-radius:12px;margin-bottom:12px;object-fit:cover;max-height:360px}
  .modal .price{font-size:16px}
  .modal .actions{display:flex;gap:10px;margin-top:12px}
  .btn{
    flex:1;background:#000;border:1px solid var(--gold);color:var(--gold);
    padding:10px 12px;border-radius:12px;font-weight:800;cursor:pointer;
  }
  .btn.gold{background:var(--gold);color:var(--ink);border:1px solid var(--gold-dark)}
  .btn:hover{filter:brightness(1.02)}
  /* Bottom nav */
  .bottom-nav{
    position:sticky;bottom:0;z-index:40;background:var(--black);color:var(--gold);
    border-top:1px solid rgba(255,215,0,.25);display:grid;grid-template-columns:1fr 1fr 1fr 1fr;gap:6px;padding:8px 6px;
  }
  .nav-item{display:flex;flex-direction:column;align-items:center;gap:4px;color:var(--gold);font-size:12px;text-decoration:none}
  .fab{
    position:relative;top:-18px;justify-self:center;width:54px;height:54px;border-radius:999px;
    background:var(--gold);display:grid;place-items:center;border:2px solid var(--gold-dark);box-shadow:0 10px 20px rgba(0,0,0,.35);
    font-size:26px;font-weight:900;color:#e60023; /* plus merah */
  }
  .hidden{display:none!important}
</style>
</head>
<body>
<!-- HEADER -->
  <header class="header">
    <a class="back-btn" onclick="history.length>1?history.back():window.scrollTo({top:0,behavior:'smooth'})">&larr;</a>
    <div class="brand">✨ Selamat Datang di <strong>Sky Store</strong> ✨</div>
    <div class="actions"></div>
    <div class="search">
      <input id="searchInput" type="text" placeholder="Cari produk… (cth: kaos, jaket)" />
      <button class="pill-btn" onclick="applySearch()">Cari</button>
    </div>
  </header>

  <!-- SLIDER (placeholder; ganti gambar sesuai kebutuhan) -->
  <div class="slider">
    <img src="https://raw.githubusercontent.com/NdikzDatabase/Database/main/Database/1755612711971-5jl9vx.jpg" alt="Promo">
  </div>

  <!-- GRID PRODUK -->
  <main class="wrap">
    <section class="grid" id="productGrid">
      <!-- Card contoh; ganti src/nama/harga -->
      <article class="card" data-name="Baju Keren" data-price="150000">
        <img src="https://raw.githubusercontent.com/NdikzDatabase/Database/main/Database/1755612697709-w04mvm.jpg" alt="Baju Keren">
        <div class="info">
          <h4 class="name">Baju Keren</h4>
          <div class="row">
            <div class="price">Rp 150.000</div>
            <div class="cta-mini">Klik di sini untuk beli</div>
          </div>
        </div>
      </article>

      <article class="card" data-name="Kaos Stylish" data-price="100000">
        <img src="https://raw.githubusercontent.com/NdikzDatabase/Database/main/Database/1755612729218-tdft7y.jpg" alt="Kaos Stylish">
        <div class="info">
          <h4 class="name">Kaos Stylish</h4>
          <div class="row">
            <div class="price">Rp 100.000</div>
            <div class="cta-mini">Klik di sini untuk beli</div>
          </div>
        </div>
      </article>

      <article class="card" data-name="Jaket Trendy" data-price="250000">
        <img src="https://raw.githubusercontent.com/NdikzDatabase/Database/main/Database/1755612592190-tg0hux.jpg" alt="Jaket Trendy">
        <div class="info">
          <h4 class="name">Jaket Trendy</h4>
          <div class="row">
            <div class="price">Rp 250.000</div>
            <div class="cta-mini">Klik di sini untuk beli</div>
          </div>
        </div>
      </article>

      <article class="card" data-name="Hoodie Stylish" data-price="200000">
        <img src="https://files.catbox.moe/glf9th.jpg" alt="Hoodie Stylish">
        <div class="info">
          <h4 class="name">Hoodie Stylish</h4>
          <div class="row">
            <div class="price">Rp 200.000</div>
            <div class="cta-mini">Klik di sini untuk beli</div>
          </div>
        </div>
      </article>
    </section>
  </main>

  <!-- MODAL DETAIL -->
  <div class="modal-backdrop" id="modalBackdrop" role="dialog" aria-modal="true">
    <div class="modal">
      <header>
        <h3 id="modalTitle">Nama Produk</h3>
        <button class="close" onclick="closeModal()">Tutup</button>
      </header>
      <div class="body">
        <img id="modalImg" src="" alt="Detail">
        <div class="price" id="modalPrice">Rp 0</div>
        <div class="actions">
          <button class="btn" onclick="addToCart()">+ Keranjang</button>
          <button class="btn gold" onclick="buyNow()">Beli Sekarang</button>
        </div>
      </div>
    </div>
  </div>

  <!-- BOTTOM NAV -->
  <nav class="bottom-nav">
    <a class="nav-item" href="#" onclick="window.scrollTo({top:0,behavior:'smooth'})">🏠<span>Beranda</span></a>
    <button id="fabAdd" class="fab hidden" title="Tambah Produk">+</button>
    <a class="nav-item" href="#" onclick="openCart()">🛒<span>Keranjang</span></a>
    <a class="nav-item" href="#" onclick="openAccount()">👤<span>Akun</span></a>
  </nav>
<script>
  // ====== CONFIG SEDERHANA ======
  const isAdmin = false; // ubah ke true agar tombol Tambah (+) muncul untuk admin
  const phoneWA = "6285211069474";

  // ====== STATE MINIMAL ======
  let currentProduct = { name:"", price:0, img:"" };
  const cart = [];

  // tampilkan tombol tambah jika admin
  if(isAdmin){ document.getElementById('fabAdd').classList.remove('hidden'); }

  // ====== SEARCH / FILTER ======
  function applySearch(){                                                                                                                                                            const q = document.getElementById('searchInput').value.toLowerCase().trim();
    document.querySelectorAll('#productGrid .card').forEach(card=>{
      const name = card.dataset.name.toLowerCase();
      card.style.display = name.includes(q) ? '' : 'none';                                                                                                                           });
  }
  document.getElementById('searchInput').addEventListener('input', applySearch);

  // ====== OPEN MODAL DARI CARD ======
  document.querySelectorAll('#productGrid .card').forEach(card=>{
    card.addEventListener('click', ()=>{
      const name = card.dataset.name;
      const price = Number(card.dataset.price||0);
      const img = card.querySelector('img')?.src || '';
      currentProduct = { name, price, img };
      // isi modal
      document.getElementById('modalTitle').textContent = name;
      document.getElementById('modalPrice').textContent = toRupiah(price);
      document.getElementById('modalImg').src = img;
      openModal();
    });
  });

  function openModal(){ document.getElementById('modalBackdrop').style.display='flex'; }
  function closeModal(){ document.getElementById('modalBackdrop').style.display='none'; }

  // ====== KERANJANG & BELI ======
  function addToCart(){
    const idx = cart.findIndex(i=>i.name===currentProduct.name);
    if(idx>-1) cart[idx].qty+=1;
    else cart.push({ ...currentProduct, qty:1 });
    alert(`Ditambahkan: ${currentProduct.name}`);
  }
  function buyNow(){
    const msg = `Halo, saya ingin membeli ${currentProduct.name} seharga ${toRupiah(currentProduct.price)}`;
    window.open(`https://wa.me/${phoneWA}?text=${encodeURIComponent(msg)}`, "_blank");
  }
  function openCart(){
    if(cart.length===0){ alert("Keranjang masih kosong."); return; }
    const list = cart.map((i,idx)=>`${idx+1}. ${i.name} x${i.qty} — ${toRupiah(i.price*i.qty)}`).join('\n');
    const total = cart.reduce((s,i)=>s+i.price*i.qty,0);
    alert(`Isi Keranjang:\n${list}\n\nTotal: ${toRupiah(total)}`);
  }
  function openAccount(){ alert("Halaman akun coming soon ✨"); }

  // ====== UTIL ======
  function toRupiah(n){
    return "Rp " + (n||0).toLocaleString("id-ID");
  }

  // fallback gambar
  document.querySelectorAll('img').forEach(img=>{
    img.onerror=()=>{ img.src='https://via.placeholder.com/600x600/000/fff?text=No+Image'; };
  });

  // klik backdrop menutup modal
  document.getElementById('modalBackdrop').addEventListener('click', (e)=>{
    if(e.target.id==='modalBackdrop') closeModal();
  });

  // admin: tombol tambah
  document.getElementById('fabAdd').addEventListener('click', ()=>{
    alert("Form tambah produk (admin) — nanti kita bikin modal upload/URL + nama + harga + kategori.");
  });
</script>
</body>
</html>
