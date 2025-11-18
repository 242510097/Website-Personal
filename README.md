<!doctype html>
<html lang="id">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Trimulia Canteen</title>
<style>
:root{
--bg:#f6f5f2;
--card:#ffffff;
--accent:#0b4d6c;
--muted:#666;
--gap:14px;
font-family: system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial;
}
*{box-sizing:border-box}
body{margin:0; background:var(--bg); color:#222; padding:20px;}
header{display:flex; align-items:center; justify-content:space-between; gap:12px; margin-bottom:18px;}
h1{font-size:1.2rem; margin:0}
p.subtitle{margin:0; color:var(--muted); font-size:0.9rem}
.cats{display:flex; gap:8px; margin:12px 0 20px; flex-wrap:wrap;}
.cat{padding:8px 12px; background:var(--card); border-radius:999px; cursor:pointer; border:1px solid transparent; font-size:0.92rem;}
.cat.active{background:var(--accent); color:white;}
.grid{display:grid; grid-template-columns:repeat(auto-fill,minmax(220px,1fr)); gap:var(--gap);}
.card{background:var(--card); border-radius:10px; padding:12px; box-shadow:0 1px 4px rgba(0,0,0,0.06); display:flex; gap:10px; align-items:flex-start; cursor:pointer;}
.thumb{width:84px; height:84px; border-radius:8px; background:linear-gradient(135deg,#e6eef2,#dfeef0); display:flex; align-items:center; justify-content:center; font-weight:700; color:var(--muted);}
.info h3{margin:0; font-size:1rem}
.info p{margin:6px 0 0; color:var(--muted); font-size:0.85rem}
.overlay{position:fixed; inset:0; display:none; align-items:center; justify-content:center; background:rgba(0,0,0,0.35); z-index:50;}
.overlay.show{display:flex;}
.detail{width:min(760px,96%); background:var(--card); border-radius:12px; padding:18px; box-shadow:0 8px 30px rgba(0,0,0,0.2); display:grid; grid-template-columns:260px 1fr; gap:14px;}
.detail .big{width:100%; height:220px; border-radius:8px; background:linear-gradient(135deg,#f0f8fb,#e6eef2); display:flex; align-items:center; justify-content:center; font-weight:700; color:var(--muted);}
.detail h2{margin:0 0 8px}
.detail p{margin:0 0 10px; color:var(--muted)}
.actions{display:flex; gap:10px; align-items:center; flex-wrap:wrap;}
.btn{padding:8px 12px; border-radius:8px; border:1px solid #ddd; background:white; cursor:pointer;}
.btn.primary{background:var(--accent); color:white; border:0;}
.cart-panel{position:fixed; top:0; right:0; height:100%; width:320px; background:var(--card); box-shadow:-3px 0 12px rgba(0,0,0,0.15); transform:translateX(100%); transition:transform .3s ease; z-index:99; display:flex; flex-direction:column;}
.cart-panel.show{transform:translateX(0);}
.cart-header{padding:16px; border-bottom:1px solid #eee; display:flex; justify-content:space-between; align-items:center;}
.cart-items{flex:1; overflow:auto; padding:12px;}
.cart-item{display:flex; justify-content:space-between; align-items:center; margin-bottom:10px; font-size:0.9rem;}
.cart-footer{border-top:1px solid #eee; padding:12px;}
.cart-empty{text-align:center; color:var(--muted); margin-top:30px; font-size:0.9rem;}
.del-btn{background:none; border:none; color:red; cursor:pointer; margin-left:6px;}
.cart-btn{position:relative; padding:8px 12px; background:var(--accent); color:white; border-radius:8px; cursor:pointer; font-size:0.9rem;}
.cart-count{position:absolute; top:-6px; right:-6px; background:red; color:white; font-size:0.7rem; padding:2px 6px; border-radius:999px;}
.payment-modal{position:fixed; inset:0; background:rgba(0,0,0,0.35); display:none; align-items:center; justify-content:center; z-index:200;}
.payment-modal.show{display:flex;}
.payment-box{background:var(--card); padding:20px; border-radius:12px; width:min(420px,90%); box-shadow:0 6px 25px rgba(0,0,0,0.2);}
.payment-box h3{text-align:center; margin-top:0; margin-bottom:16px;}
.payment-options{display:grid; gap:12px;}
.pay-option{border:1px solid #ddd; border-radius:10px; padding:14px; display:flex; align-items:center; justify-content:space-between; cursor:pointer; transition:0.2s; background:white;}
.pay-option:hover{background:#f0f8fb; border-color:var(--accent);}
.pay-option span{font-weight:500;}
.pay-option small{color:var(--muted);}
.close-pay{margin-top:16px; width:100%;}
.history-panel{position:fixed; top:0; left:0; height:100%; width:320px; background:var(--card); box-shadow:3px 0 12px rgba(0,0,0,0.15); transform:translateX(-100%); transition:transform .3s ease; z-index:98; display:flex; flex-direction:column;}
.history-panel.show{transform:translateX(0);}
.history-header{padding:16px; border-bottom:1px solid #eee; display:flex; justify-content:space-between; align-items:flex-start; flex-direction:column; gap:8px;}
.history-filter{display:flex; gap:6px;}
.history-filter button{padding:4px 8px; border-radius:6px; border:1px solid #ddd; background:white; cursor:pointer; font-size:0.8rem;}
.history-filter button.active{background:var(--accent); color:white; border:0;}
.history-items{flex:1; overflow:auto; padding:12px;}
.history-item{padding:8px; border-bottom:1px solid #eee; border-radius:6px; margin-bottom:6px;}
.history-item small.lunas{color:green;}
.history-item small.belum{color:red;}
@media (max-width:600px){
.detail{grid-template-columns:1fr; padding:12px}
.detail .big{height:160px}
}

#loginPage{
  position:fixed;
  inset:0;
  background:var(--bg);
  display:flex;
  justify-content:center;
  align-items:center;
  z-index:999;
}
.login-box{
  background:var(--card);
  padding:30px;
  border-radius:12px;
  width:300px;
  box-shadow:0 6px 25px rgba(0,0,0,0.2);
  text-align:center;
}
.login-box h2{margin-bottom:20px;}
.login-box input{
  width:100%;
  padding:10px;
  margin-bottom:12px;
  border:1px solid #ddd;
  border-radius:8px;
}
.login-box button{
  width:100%;
  padding:10px;
  background:var(--accent);
  color:white;
  border:none;
  border-radius:8px;
  cursor:pointer;
}
</style>
</head>
<body>
<div id="loginPage">
  <div class="login-box">
    <h2>Welcome!</h2>
    <input type="email" id="loginEmail" placeholder="Email" />
    <input type="password" id="loginPassword" placeholder="Password" />
    <button id="loginBtn">Login</button>
  </div>
</div>

<header>
<div>
<h1>Trimulia Canteen</h1>
<p class="subtitle">Order your favorite foods and drinks on this online website, easy and fast!</p>
</div>
<div style="display:flex;align-items:center;gap:10px">
<div style="font-size:0.9rem;color:var(--muted)">Total menu: <strong id="total">0</strong></div>
<div class="cart-btn" id="historyToggle">📓</div>
<div class="cart-btn" id="cartToggle">🛒 <span class="cart-count" id="cartCount">0</span></div>
</div>
</header>
<div class="cats" id="categories"></div>
<div class="grid" id="grid"></div>

<!-- Detail Modal -->
<div class="overlay" id="overlay">
<div class="detail">
<div><div class="big" id="detailImg">IMG</div></div>
<div>
<h2 id="detailTitle">Judul Menu</h2>
<p id="detailMeta">1 bowl • Rp 0</p>
<p id="detailDesc">Deskripsi menu tampil di sini.</p>
<div class="actions">
<div style="display:flex;gap:8px;align-items:center">
<button class="btn" id="dec">-</button>
<div id="qty" style="min-width:28px;text-align:center">1</div>
<button class="btn" id="inc">+</button>
</div>
<button class="btn primary" id="addToCartBtn">Tambah ke Keranjang</button>
<button class="btn" id="close">Tutup</button>
</div>
</div>
</div>
</div>

<!-- Cart Sidebar -->
<div class="cart-panel" id="cartPanel">
<div class="cart-header">
<strong>Keranjang</strong>
<button class="btn" id="closeCart">Tutup</button>
</div>
<div class="cart-items" id="cartItems"></div>
<div class="cart-footer">
<div>Total: Rp <span id="cartTotal">0</span></div>
<button class="btn primary" id="checkoutBtn" style="width:100%;margin-top:10px">Checkout</button>
</div>
</div>

<!-- History Sidebar -->
<div class="history-panel" id="historyPanel">
<div class="history-header">
<div>
<strong>History Pesanan</strong>
<div class="history-filter">
<button data-filter="All" class="active">Semua</button>
<button data-filter="Lunas">Lunas</button>
<button data-filter="Belum">Belum Bayar</button>
</div>
</div>
<button class="btn" id="closeHistory">Tutup</button>
</div>
<div class="history-items" id="historyItems"></div>
</div>

<!-- Payment Modal -->
<div class="payment-modal" id="paymentModal">
<div class="payment-box">
<h3>Pilih Metode Pembayaran</h3>
<div class="payment-options">
<div class="pay-option" data-method="Cash">
<span>💵 Cash</span><small>Bayar langsung di kasir</small>
</div>
<div class="pay-option" data-method="QRIS">
<span>📱 QRIS</span><small>Scan QR untuk pembayaran digital</small>
</div>
<div class="pay-option" data-method="Ngutang">
<span>📓 Ngutang</span><small>Bayar nanti, tapi jangan lupa</small>
</div>
</div>
<button class="btn close-pay" id="cancelPay">Batal</button>
</div>
</div>

<script>
    // --- LOGIN ---
    const loginPage = document.getElementById('loginPage');
    const loginBtn = document.getElementById('loginBtn');
    const emailInput = document.getElementById('loginEmail');
    const passwordInput = document.getElementById('loginPassword');
    // Buat elemen error pesan
    const emailError = document.createElement('div');
    emailError.style.color = 'red';
    emailError.style.fontSize = '0.8rem';
    emailError.style.marginTop = '8px';
    emailError.style.display = 'none';
    // Sisipkan setelah input email
    emailInput.parentNode.insertBefore(emailError, emailInput.nextSibling);

    document.getElementById('loginBtn').onclick = () => {
      const email = emailInput.value.trim();
      const password = passwordInput.value;
      if(email && email.endsWith('@trimulia.sch.id')){
        emailError.style.display = 'none'; // hilangkan pesan error
        loginPage.style.display = 'none';
      } else {
        // Tampilkan pesan error
        emailError.style.display = 'block';
        emailError.textContent = 'Hanya email @trimulia.sch.id yang bisa login!';
      }
    };

const products = [   
{id:1,title:"Nasi Goreng",cat:"Rice",size:"1 bowl",price:15000,desc:"Nasi goreng dengan udang dan ikan.", img: "https://i.pinimg.com/736x/4d/89/4a/4d894ae7d925293f90b3aa7e5b3a316c.jpg"},
{id:2,title:"Indomie",cat:"Noodles",size:"1 bowl",price:10000,desc:"Indomie sayur cocok untuk vegetarian.", img: "https://i.pinimg.com/1200x/50/6f/8b/506f8bd602cb15ea0028f3f470c8352b.jpg"},
{id:3,title:"Kwetiau",cat:"Noodles",size:"1 bowl",price:15000,desc:"Kwetiau goreng dengan paprika dan basil.", img: "https://i.pinimg.com/736x/a0/8b/4e/a08b4ec0e8e532da743d8782fb3f3c0c.jpg"},
{id:4,title:"Nasi Hainan",cat:"Rice",size:"1 bowl",price:22000,desc:"Nasi hainam ayam khas oriental.", img: "https://i.pinimg.com/736x/40/fc/b6/40fcb612bca67e1c094cf5afd78509b7.jpg "},
{id:5,title:"Nasi Katsu",cat:"Rice",size:"1 bowl",kcal:390,price:15000,desc:"Katsu ikan renyah dengan saus asin-manis.", img: "https://i.pinimg.com/1200x/30/af/7e/30af7eacbd832c4be4172ef91821c905.jpg "},
{ id:6, title:"Nasi Ikan Tongkol", cat:"Rice", size:"1 bowl", price:12000, desc:"Tongkol pedas gurih, disajikan dengan sambal.", img: "https://i.pinimg.com/736x/3b/31/3f/3b313fce710af2b5537daf5bef3bcb9c.jpg"},
{ id:7, title:"Nasi Ayam Serundeng", cat:"Rice", size:"1 bowl", price:15000, desc:"Nasi ayam serundeng gurih dengan kelapa renyah menggugah selera.", img: "https://i.pinimg.com/1200x/55/68/ea/5568ea648bd2bf52b1d9d484a7acc44c.jpg"},
{ id:8, title:"Nasi Kuning", cat:"Rice", size:"1 bowl", price:12000, desc:"Nasi kuning harum dengan cita rasa gurih dan lezat.", img: "https://i.pinimg.com/736x/bd/8d/89/bd8d8972793480a3a5b3d622df559fdc.jpg "},
{ id:9, title:"Nasi Ayam Matah", cat:"Rice", size:"1 bowl", price:12000, desc:"Nasi ayam matah pedas segar khas Bali.", img: "https://i.pinimg.com/736x/e3/80/23/e3802352f8e61be24bcc76227bc34f30.jpg "},
{ id:10, title:"Nasi Babi Matah", cat:"Rice", size:"1 bowl", price:15000, desc:"Nasi babi matah pedas gurih dengan sambal segar Bali.", img: "https://i.pinimg.com/736x/07/43/14/074314387f536714ac8ebbf4a6a40fd5.jpg"},
{ id:11, title:"Nasi Ayam Teriyaki", cat:"Rice", size:"1 bowl", price:15000, desc:"Nasi ayam teriyaki manis gurih ala Jepang.", img: "https://i.pinimg.com/736x/3f/dd/7a/3fdd7aeed9cb3460075db966380ef4bb.jpg "},
{ id:12, title:"Nasi Babi Bawang", cat:"Rice", size:"1 bowl", price:15000, desc:"Nasi babi bawang gurih dengan aroma bawang yang menggoda.", img: "https://i.pinimg.com/1200x/44/e0/c2/44e0c27f531bc47423759b4d6c42e9f3.jpg"},
{ id:13, title:"Jus Alpukat", cat:"Drinks", size:"1 cup", price:10000, desc:"Nasi babi bawang gurih dengan aroma bawang yang menggoda.", img: "https://i.pinimg.com/736x/a5/df/58/a5df58cb2972c04ca6f4a74e08a27eb1.jpg"},
{ id:14, title:"Jus Mangga", cat:"Drinks", size:"1 cup", price:10000, desc:"Jus mangga manis segar penuh rasa tropis.", img: "https://i.pinimg.com/736x/26/17/12/261712d651d6efb63f6f238edb9cce63.jpg"},
{ id:15, title:"Jus Jeruk", cat:"Drinks", size:"1 cup", price:10000, desc:"Jus jeruk segar dengan rasa asam manis yang menyegarkan.", img: "https://i.pinimg.com/1200x/a2/c9/fa/a2c9fa151d585052646a92c338bff265.jpg"},
{ id:16, title:"Jus Strawberry", cat:"Drinks", size:"1 cup", price:10000, desc:"Jus strawberry manis segar dengan aroma buah alami.", img: "https://i.pinimg.com/736x/e5/cd/b8/e5cdb897f3d113d51a0a93dd3ea47c46.jpg"},
{ id:17, title:"Teh Botol", cat:"Drinks", size:"1 bottle", price:8000, desc:"Teh Botol Sosro manis segar, siap menemani harimu.", img: "https://i.pinimg.com/736x/7b/05/cd/7b05cd49df6a8a96dd46e02073e67616.jpg "},
{ id:18, title:"Pocari", cat:"Drinks", size:"1 bottle", price:8000, desc:"Pocari Sweat minuman isotonic segar untuk tetap bugar dan hidrasi.", img: "https://i.pinimg.com/736x/cd/34/5f/cd345f97811c0ac4d084933f66486e47.jpg "},
{ id:19, title:"Fibber Mini", cat:"Drinks", size:"1 bottle", price:8000, desc:"Fibber Mini minuman ringan praktis, segar, dan nikmat kapan saja.", img: "https://i.pinimg.com/1200x/07/ea/4c/07ea4cade4c8c17fc19fab3b5996a8b2.jpg"},
{ id:20, title:"C100", cat:"Drinks", size:"1 bottle", price:8000, desc:"C1000 minuman vitamin C segar untuk tubuh tetap bugar dan sehat.", img: "https://i.pinimg.com/1200x/56/4f/e8/564fe895815844b14f6df8e5b8e64131.jpg"},
{ id:21, title:"Fruit Tea", cat:"Drinks", size:"1 bottle", price:5000, desc:"Fruit Tea Instan praktis, segar dan penuh rasa buah alami.", img: "https://i.pinimg.com/1200x/0f/cd/47/0fcd47b802b070b3aa1a86767f34facf.jpg"},
{ id:22, title:"Milo", cat:"Drinks", size:"1 kotak", price:8000, desc:"Susu Milo creamy, manis, dan penuh energi.", img: "https://i.pinimg.com/736x/e2/e3/e6/e2e3e6cb7e480043d3bd883aa75e5647.jpg"},
{ id:23, title:"Susu KitKat", cat:"Drinks", size:"1 can", price:8000, desc:"Susu KitKat manis, creamy, dan nikmat dengan rasa cokelat khas KitKat.", img: "https://i.pinimg.com/736x/99/e8/07/99e807180b986affb46089dec29ccf57.jpg "},
{ id:24, title:"Nu Green Tea", cat:"Drinks", size:"1 bottle", price:4000, desc:"Nu Green Tea segar dengan aroma teh hijau alami.", img: "https://i.pinimg.com/736x/65/c1/3c/65c13c8c93d69e27aaa64b3f8a0334b8.jpg"},
{ id:25, title:"Nescafe", cat:"Drinks", size:"1 can", price:10000, desc:"Nescafé kopi instan hangat dan nikmat untuk semangat harimu.", img: "https://i.pinimg.com/736x/b1/c4/0a/b1c40a98359ba76cc120e4f9a99fe51c.jpg"},
{ id:26, title:"Nipis Madu", cat:"Drinks", size:"1 bottle", price:5000, desc:"Nipis Madu segar manis alami, menyegarkan setiap tegukan.", img: "https://i.pinimg.com/736x/2d/99/6b/2d996beddad5af902afa225a39a065e4.jpg"},
{ id:27, title:"Le Minerale", cat:"Drinks", size:"1 bottle", price:3000, desc:"Le Minerale air mineral segar, murni, dari pegunungan", img: "https://i.pinimg.com/736x/27/62/7c/27627c18d11e0258d25678b0c922b3c8.jpg"},
{ id:28, title:"Aqua", cat:"Drinks", size:"1 bottle", price:5000, desc:"Aqua air mineral murni, segar, dan menyehatkan tubuh.", img: "https://i.pinimg.com/736x/af/07/78/af07783b06cfd7c4c126ad6e769c0997.jpg"},
{ id:29, title:"Cimory Yogurt", cat:"Drinks", size:"1 bottle", price:8000, desc:"Yoghurt Cimory creamy, segar, dan kaya probiotik.", img: "https://i.pinimg.com/736x/2b/3c/2f/2b3c2fe795ecd5104bdc4098ffb13a2a.jpg" },
{ id:30, title:"Donut", cat:"Deserts", size:"1 pcs", price:5000, desc:"Donut manis lembut, cocok untuk camilan atau sarapan.", img: "https://i.pinimg.com/1200x/28/16/8c/28168c6f54f32f22d68578c172484d55.jpg"},
{ id:31, title:"Roti", cat:"Deserts", size:"1 pcs", price:7000, desc:"Roti lembut dan hangat, pas untuk sarapan atau camilan.", img: "https://i.pinimg.com/1200x/9b/4d/0f/9b4d0f9f743c15e4ec555eceb8d317cb.jpg" },
{ id:32, title:"Hot Dog", cat:"Snacks", size:"1 pcs", price:10000, desc:"Hot dog lezat dengan sosis gurih dan roti hangat.", img: "https://i.pinimg.com/1200x/3c/ec/1a/3cec1ae6e9432ab292e154b9bbcef45d.jpg"},
{ id:33, title:"Mie Yamien", cat:"Noodles", size:"1 bowl", price:10000, desc:"Mie Yamyien kenyal dengan kuah gurih yang menggugah selera.", img: "https://i.pinimg.com/736x/46/6d/d3/466dd3d62f2d7a1b626bb3fa63f97ac.jpg"},
{ id:34, title:"Silver Queen", cat:"Sweets", size:"1 pcs", price:12000, desc:"Silver Queen coklat lezat, manis, dan meleleh di mulut.", img: "https://i.pinimg.com/1200x/9d/b9/da/9db9dad80e29391007afaee4318a490c.jpg" },
{ id:35, title:"Pangsit Chilli", cat:"Snacks", size:"1 cup", price:12000, desc:"Pangsit Chilli pedas gurih, nikmat untuk cemilan atau lauk.", img: "https://i.pinimg.com/736x/f8/8e/eb/f88eeb4fe80bfd25fa7716094d756973.jpg"},
{ id:36, title:"Cookies", cat:"Deserts", size:"1 pcs", price:8000, desc:"Cookies renyah manis, cocok untuk cemilan kapan saja.", img: "https://i.pinimg.com/1200x/98/4c/d1/984cd1f8dafaf605a30cefafe16a1095.jpg" },
{ id:37, title:"Cilok", cat:"Snacks", size:"1 cup", price:6000, desc:"Cilok kenyal dengan saus gurih pedas, cemilan favorit semua usia.", img: "https://i.pinimg.com/1200x/eb/43/c7/eb43c7301c73be2f61e991b47f8f47a5.jpg"},
{ id:38, title:"Onigiri", cat:"Rice", size:"1 pcs", price:10000, desc:"Onigiri nasi kepal praktis, gurih, dan lezat untuk bekal atau cemilan.", img: "https://i.pinimg.com/1200x/e9/74/4b/e9744b267fc707ed326aa01c659cc8b6.jpg"},
{ id:39, title:"Nasi Japanese Sauce", cat:"Rice", size:"1 bowl", price:12000, desc:"Nasi dengan saus Jepang gurih, lezat, dan penuh cita rasa.", img: "https://i.pinimg.com/736x/29/c3/d3/29c3d3fdd6f7eba01640c66c712054c3.jpg"},
{ id:40, title:"Nasi Cumi Ijo", cat:"Rice", size:"1 bowl", price:12000, desc:"Nasi cumi ijo pedas gurih, nikmat dan menggugah selera.", img: "https://i.pinimg.com/736x/2b/71/9b/2b719bbcdd87695bd0f9e0e1d9762e56.jpg"},
{ id:41, title:"Nasi Cumi Merah", cat:"Rice", size:"1 bowl", price:12000, desc:"Nasi cumi merah pedas gurih, penuh cita rasa laut.", img: "https://i.pinimg.com/1200x/8b/5e/46/8b5e46247fff17720f39a9e7a3b69f79.jpg"},
{ id:42, title:"Nasi Katsu Curry", cat:"Rice", size:"1 bowl", price:12000, desc:"Nasi Katsu Curry gurih dengan saus kari hangat dan ayam renyah.", img: "https://i.pinimg.com/1200x/58/5b/e9/585be9b90c84803d96d39ab316ecc1c8.jpg" },
{ id:43, title:"Lays", cat:"Snacks", size:"1 pcs", price:3500, desc:"Lays renyah dan gurih, camilan praktis kapan saja.", img: "https://i.pinimg.com/736x/cb/c9/ba/cbc9ba7987e9685820933e5de39df05f.jpg" },
{ id:44, title:"Nasi Ayam Madu", cat:"Rice", size:"1 bowl", price:15000, desc:"Nasi ayam madu manis gurih, lezat dan menggugah selera.", img: "https://i.pinimg.com/1200x/32/cf/8b/32cf8bcb9e2fdbe2a863730ec50752b5.jpg" },
{ id:45, title:"Nasi sate", cat:"Rice", size:"1 bowl", price:15000, desc:"Nasi sate gurih dengan potongan daging dan saus kacang khas.", img: "https://i.pinimg.com/736x/c6/c9/32/c6c932395dc180bc9d5b1c7e62de5a2a.jpg"},
{ id:46, title:"Nasi Uduk", cat:"Rice", size:"1 bowl", price:12000, desc:"Nasi uduk gurih harum dengan pelengkap lezat.", img: "https://i.pinimg.com/1200x/23/ed/d0/23edd0b146ffc32ab856ea9c1d1fcf94.jpg" },
{ id:47, title:"Nasi Ayam Tartar", cat:"Rice", size:"1 bowl", price:12000, desc:"Nasi ayam dengan saus mayo", img: "https://assets.promediateknologi.id/crop/0x0:0x0/750x500/webp/photo/2023/04/03/ayam-goreng-jepang-1853944364.jpeg" },
{ id:48, title:"Nasi katsu tomat mayo", cat:"Rice", size:"1 bowl", price:12000, desc:"Nasi katsu dengan saus tomat dan mayo", img: "https://i.pinimg.com/1200x/5b/7a/18/5b7a1823fccaed770169356a1dda780f.jpg"},
{ id:49, title:"Sushi", cat:"Rice", size:"1 cup", price:15000, desc:"Sushi segar dengan nasi lembut dan isian lezat.", img: "https://i.pinimg.com/1200x/9b/6d/17/9b6d17cfa1772f49b2efa99a3df1683d.jpg"},
{ id:50, title:"Nasi Babi samcan", cat:"Rice", size:"1 bowl", price:15000, desc:"Nasi babi Samcan gurih dengan potongan babi lezat dan bumbu khas.", img: "https://i.pinimg.com/736x/dd/5c/b0/dd5cb0c87184b8ddd6a95f65ce668a7d.jpg"},
{ id:51, title:"Nasi Ayam teriyaki", cat:"Rice", size:"1 bowl", price:12000, desc:"Nasi ayam teriyaki gurih manis dengan saus khas Jepang.", img: "https://i.pinimg.com/1200x/38/5d/86/385d869595e0c99586b1d2c1096b0353.jpg"},
{ id:52, title:"Pringles", cat:"Snacks", size:"1 pcs", price:9000, desc:"cocok untuk dijadiakn cemilan.", img: "https://i.pinimg.com/1200x/93/1a/5f/931a5f4a2872cc58703b8c2987e96c64.jpg" },
{ id:53, title:"Chitato", cat:"Snacks", size:"1 pcs", price:3000, desc:"Nasi ayam dengan saus mayo", img: "https://i.pinimg.com/736x/a9/3e/4a/a93e4aa6870d972f895522cee3627c38.jpg" },
{ id:54, title:"Tictac", cat:"Snacks", size:"1 pcs", price:4000, desc:"Nasi katsu dengan saus tomat dan mayo", img: "https://i.pinimg.com/736x/c1/0f/8a/c10f8a38ad04cfb45446499b4a555de0.jpg"},
{ id:55, title:"Kusuka", cat:"Snacks", size:"1 pcs", price:8000, desc:"cocok untuk dijadiakn cemilan.", img: "https://i.pinimg.com/736x/ca/41/a0/ca41a0229e83509ca3396bc1942a92bd.jpg" },
{ id:56, title:"Siip", cat:"Snacks", size:"1 pcs", price:4000, desc:"Nasi ayam dengan saus mayo", img: "https://i.pinimg.com/736x/8e/1c/20/8e1c20c51763c168513f774cbbe5debf.jpg" },
{ id:57, title:"Chiki Balls", cat:"Snacks", size:"1 pcs", price:4000, desc:"Nasi katsu dengan saus tomat dan mayo", img: "https://i.pinimg.com/1200x/d8/54/52/d854529b613f1af6dc21a98c83b20e06.jpg"},
{ id:58, title:"Pota Bee", cat:"Snacks", size:"1 pcs", price:8000, desc:"cocok untuk dijadiakn cemilan.", img: "https://i.pinimg.com/1200x/88/7c/33/887c3334cc37618d273613fb988bcc67.jpg" },
{ id:59, title:"Guribee", cat:"Snacks", size:"1 pcs", price:7000, desc:"Ciki dengan bumbu yang sangat sedap", img: "https://i.pinimg.com/736x/96/f5/24/96f5240927dcad2ccfeb30d16a5893fe.jpg" },
{ id:60, title:"Qtela", cat:"Snacks", size:"1 pcs", price:4000, desc:"Ciki singkong yang enak untuk dijadikan cemilan", img: "https://i.pinimg.com/736x/0c/f4/74/0cf474535a597de10a179f8edc574420.jpg"},
{ id:61, title:"Taro net", cat:"Snacks", size:"1 pcs", price:9000, desc:"Ciki berbentuk seperti net yang unik dan lezat", img: "https://i.pinimg.com/736x/39/98/0f/39980f256e1c29433f5656db29332fda.jpg" },
{ id:62, title:"Gery", cat:"Snacks", size:"1 pcs", price:3000, desc:"Biskuit dengan benduk kotak dengan berbagai variasi", img: "https://i.pinimg.com/1200x/bb/d6/31/bbd6316a104e70b84364173ce5d3c26d.jpg" },
{ id:63, title:"Sari Gandum", cat:"Snacks", size:"1 pcs", price:4000, desc:"Biskuit dengan bahan alami dari gandum yang sehat", img: "https://i.pinimg.com/1200x/c1/f2/dd/c1f2dd8492d6c46289482bec93b0607d.jpg"},
{ id:64, title:"Good Time", cat:"Snacks", size:"1 pcs", price:8000, desc:"Biskuit cookies coklat", img: "https://i.pinimg.com/736x/58/87/aa/5887aafe811a19ca54a1d94d5e7e5c16.jpg" },
{ id:65, title:"Nabati", cat:"Snacks", size:"1 pcs", price:5000, desc:"Biskuit dengan krim pink di dalam", img: "https://i.pinimg.com/736x/cc/11/9e/cc119e2828fe254223ea6f29e8f80c1e.jpg" },
{ id:66, title:"Hello Panda", cat:"Snacks", size:"1 pcs", price:4000, desc:"Biskuit mini mini", img: "https://i.pinimg.com/736x/d6/1b/de/d61bde6c0d2d881c59430d94fc0457c0.jpg"},
{ id:67, title:"ChicChoc", cat:"Sweets", size:"1 pcs", price:9000, desc:"Cemilan manis berbentuk bola bola", img: "https://i.pinimg.com/1200x/f9/9d/94/f99d944a8e48917ed8e190b9ab469718.jpg" },
{ id:68, title:"Chacha", cat:"Sweets", size:"1 pcs", price:3000, desc:"Coklat dengan isian kacang", img: "https://i.pinimg.com/1200x/5a/58/95/5a5895dcec6e880e7f77ee28f9972bc7.jpg" },
{ id:69, title:"ChupaChups", cat:"Sweets", size:"1 pcs", price:4000, desc:"Permen layu yang enak dimakan", img: "https://i.pinimg.com/1200x/f0/f7/26/f0f726e5b6f7012eab15e588720b9ab1.jpg"},
{ id:70, title:"Yupi", cat:"Sweets", size:"1 pcs", price:7000, desc:"Sangat cocok untuk semua usia", img: "https://i.pinimg.com/736x/fd/f5/db/fdf5db3e95c411437f4ea78c471cc0c1.jpg" },
{ id:71, title:"Haribo", cat:"Sweets", size:"1 pcs", price:15000, desc:"Permen berbentuk cola dan rasa yg enak", img: "https://i.pinimg.com/1200x/4e/a3/62/4ea3621eef88935c2319a5ccdfe3e1b9.jpg" },
{ id:72, title:"KitKat", cat:"Sweets", size:"1 pcs", price:10000, desc:"Coklat batangan yang bisa untuk dibahi beberapa orang", img: "https://i.pinimg.com/736x/f0/ce/1c/f0ce1c7bd46f95470e4b642174ab9343.jpg"},
{ id:73, title:"Snickers", cat:"Sweets", size:"1 pcs", price:12000, desc:"Coklat dengan isian caramel", img: "https://i.pinimg.com/736x/67/f6/66/67f666423b07222f952292f0131133a4.jpg" }, 
{ id:74, title:"Nutella", cat:"Sweets", size:"1 pcs", price:17000, desc:"Biskuit diluar dan isian nutella yang banyak", img: "https://i.pinimg.com/736x/21/3a/15/213a152d0675556cc10ba2b4e5474adb.jpg" },
{ id:75, title:"Milo Nuggets", cat:"Sweets", size:"1 pcs", price:10000, desc:"Milo nuggets yang bikin nagih", img: "https://i.pinimg.com/736x/22/f1/76/22f176ad20919d816c6e3790709369eb.jpg"},
{ id:76, title:"Dairy Milk", cat:"Sweets", size:"1 pcs", price:9000, desc:"Lumer dimulut dan sangat enak.", img: "https://i.pinimg.com/736x/7d/02/fc/7d02fca439acc3f097863b02c194b56b.jpg" },
    { id:77, title:"Pudding Caramel", cat:"Deserts", size:"1 pcs", price:25000, desc:"Pudding dengan saos karamel", img: "https://i.pinimg.com/736x/cd/35/b9/cd35b9047da30d0a393e7bd4148582f4.jpg"},
    { id:78, title:"Ice Cream Sandwich", cat:"Deserts", size:"1 pcs", price:2000, desc:"Es krim sandwich dengan biskuit di kedu sisinya", img: "https://i.pinimg.com/1200x/e3/5f/4e/e35f4e086bbce6992f280107dd2b1cf7.jpg"},
     { id:79, title:"Mini Lemon Cheesecake", cat:"Deserts", size:"1 pcs", price:35000, desc:"Cheesecake mini rasa lemon", img: "https://i.pinimg.com/1200x/49/8a/74/498a749dfbab1dc58fa76c7f1eeb3af5.jpg"},
    { id:80, title:"Tiramisu", cat:"Deserts", size:"1 pcs", price:45000, desc:"Kue lembut, lumer dimulut rasa kopi", img: "https://i.pinimg.com/736x/f4/e2/75/f4e275c59e39bb16be059059eff92e74.jpg"},
    { id:81, title:"Churros", cat:"Deserts", size:"1 pcs", price:30000, desc:"Churros dengan saos coklat", img: "https://i.pinimg.com/1200x/23/cc/17/23cc176e7e967058152d2dcb51a5f7fc.jpg"},
    { id:82, title:"Strawberry Chocolate", cat:"Deserts", size:"1 pcs", price:20000, desc:"Stroberi yang dilapisi coklat", img: "https://i.pinimg.com/1200x/6e/9d/3e/6e9d3e045b9741acc005e5cc66b35335.jpg"},
     { id:83, title:"Japanese fruit sandwich", cat:"Deserts", size:"2 pcs", price:20000, desc:"Roti dengan isian krim dan ada buah stroberi", img: "https://i.pinimg.com/1200x/f6/d9/2f/f6d92f51752b9f9a8140c91cf3cf61c2.jpg"},
    { id:84, title:"Tanghulu", cat:"Deserts", size:"1 pcs", price:26000, desc:"Buah buahan yang dilapisi gula", img: "https://i.pinimg.com/736x/e0/36/24/e03624f41c81d73cce5e1227a30fedf6.jpg"},
    
  ];

const categories = ["All","Rice","Noodles","Snacks","Sweets","Deserts","Drinks"];
const catsEl = document.getElementById('categories');
let activeCat = "All";
categories.forEach(c => {
const btn = document.createElement('button');
btn.textContent = c;
btn.className = 'cat' + (c===activeCat?' active':'');
btn.onclick = () => {
document.querySelectorAll('.cat').forEach(x=>x.classList.remove('active'));
btn.classList.add('active');
activeCat = c;
renderGrid();
};
catsEl.appendChild(btn);
});
const grid = document.getElementById('grid');
const totalEl = document.getElementById('total');
let cart = [];
let history = [];
function formatRupiah(amount){ return ' '+amount.toLocaleString('id-ID'); }
function renderGrid() {
grid.innerHTML = '';
const list = products.filter(p => activeCat==='All' || p.cat===activeCat);
totalEl.textContent = list.length;
list.forEach(p=>{
const card = document.createElement('article');
card.className = 'card';
card.innerHTML = `
<div class="thumb">${p.img ? `<img src="${p.img}" width="84" height="84" style="object-fit:cover;border-radius:8px">` : p.title.charAt(0)}</div>
<div class="info">
<h3>${p.title}</h3>
<p>${p.size} • ${formatRupiah(p.price)}</p>
</div>
`;
card.onclick = () => showDetail(p);
grid.appendChild(card);
});
}
// Detail Modal
const overlay = document.getElementById('overlay');
const detailImg = document.getElementById('detailImg');
const detailTitle = document.getElementById('detailTitle');
const detailMeta = document.getElementById('detailMeta');
const detailDesc = document.getElementById('detailDesc');
const qtyEl = document.getElementById('qty');
let currentQty = 1;
let currentProduct = null;
function showDetail(p) {
currentProduct = p;
detailImg.innerHTML = currentProduct.img ? `<img src="${currentProduct.img}" width="220" height="220" style="object-fit:cover;border-radius:8px">` : currentProduct.title.charAt(0);
detailTitle.textContent = currentProduct.title;
detailMeta.textContent = `${currentProduct.size} • ${formatRupiah(currentProduct.price)}`;
detailDesc.textContent = currentProduct.desc;
currentQty = 1;
qtyEl.textContent = currentQty;
overlay.classList.add('show');
}
document.getElementById('close').onclick = ()=> overlay.classList.remove('show');
document.getElementById('dec').onclick = ()=>{ if(currentQty>1) currentQty--; qtyEl.textContent = currentQty; };
document.getElementById('inc').onclick = ()=>{ currentQty++; qtyEl.textContent = currentQty; };
document.getElementById('addToCartBtn').onclick = ()=>{
const item = cart.find(x=>x.id===currentProduct.id);
if(item) item.qty += currentQty;
else cart.push({...currentProduct, qty: currentQty});
overlay.classList.remove('show');
renderCart();
};
// Cart
const cartPanel = document.getElementById('cartPanel');
const cartItems = document.getElementById('cartItems');
const cartTotal = document.getElementById('cartTotal');
const cartCount = document.getElementById('cartCount');
function renderCart() {
cartItems.innerHTML = '';
if(cart.length===0){
cartItems.innerHTML = '<div class="cart-empty">Keranjang kosong</div>';
} else {
cart.forEach(item=>{
const div = document.createElement('div');
div.className = 'cart-item';
div.innerHTML = `${item.title} x${item.qty} - ${formatRupiah(item.price*item.qty)} <button class="del-btn">x</button>`;
div.querySelector('.del-btn').onclick = ()=>{ cart = cart.filter(x=>x.id!==item.id); renderCart(); };
cartItems.appendChild(div);
});
}
const total = cart.reduce((a,b)=>a+b.price*b.qty,0);
cartTotal.textContent = formatRupiah(total);
cartCount.textContent = cart.reduce((a,b)=>a+b.qty,0);
}
document.getElementById('cartToggle').onclick = ()=>cartPanel.classList.toggle('show');
document.getElementById('closeCart').onclick = ()=>cartPanel.classList.remove('show');
// History Panel
const historyPanel = document.getElementById('historyPanel');
const historyItems = document.getElementById('historyItems');
document.getElementById('historyToggle').onclick = ()=>historyPanel.classList.toggle('show');
document.getElementById('closeHistory').onclick = ()=>historyPanel.classList.remove('show');
let currentHistoryFilter = 'All';
function renderHistory() {
historyItems.innerHTML = '';
let list = [...history];
if(currentHistoryFilter==='Lunas') list = list.filter(h=>h.method!=='Ngutang');
else if(currentHistoryFilter==='Belum') list = list.filter(h=>h.method==='Ngutang');
if(list.length===0){
historyItems.innerHTML = '<div class="cart-empty">Belum ada pesanan</div>';
} else {
list.forEach((h, i)=>{
const div = document.createElement('div');
div.className = 'history-item';
div.innerHTML = `<strong>Pesanan ${i+1} (${h.method})</strong><br>${h.items.map(it=>`${it.title} x${it.qty} - ${formatRupiah(it.price*it.qty)}`).join('<br>')}<br>Total: ${formatRupiah(h.total)}<br><small class="${h.method==='Ngutang' ? 'belum' : 'lunas'}">${h.method==='Ngutang' ? 'Belum bayar' : 'Lunas'}</small>`;
historyItems.appendChild(div);
});
}
}
// Filter buttons
document.querySelectorAll('.history-filter button').forEach(btn=>{
btn.onclick = ()=>{
document.querySelectorAll('.history-filter button').forEach(b=>b.classList.remove('active'));
btn.classList.add('active');
currentHistoryFilter = btn.dataset.filter==='Belum Bayar' ? 'Belum' : btn.dataset.filter;
renderHistory();
};
});
// Payment Modal
const paymentModal = document.getElementById('paymentModal');
document.getElementById('checkoutBtn').onclick = ()=>{ if(cart.length===0) return alert('Keranjang kosong!'); paymentModal.classList.add('show'); };
document.getElementById('cancelPay').onclick = ()=>paymentModal.classList.remove('show');
document.querySelectorAll('.pay-option').forEach(o=>{
o.onclick = ()=>{
const total = cart.reduce((a,b)=>a+b.price*b.qty,0);
history.push({items:[...cart], total: total, method: o.dataset.method});
alert('Pembayaran dengan '+o.dataset.method+' berhasil!');
cart = [];
renderCart();
renderHistory();
paymentModal.classList.remove('show');
historyPanel.classList.add('show');
};
});
// Render awal
renderGrid();
renderCart();
renderHistory();
</script>
</body>
</html>

