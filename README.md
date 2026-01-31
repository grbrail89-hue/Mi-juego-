# Mi-juego-
...
<!DOCTYPE html><html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Tienda de Juegos</title>
<style>
body{margin:0;font-family:Arial;background:#f1f3f4}
header{background:#1a73e8;color:#fff;padding:15px;text-align:center;font-size:22px;font-weight:bold}
.container{max-width:900px;margin:auto;padding:20px}
.game,.comments,.admin{background:#fff;border-radius:16px;padding:16px;margin-bottom:16px;box-shadow:0 4px 12px rgba(0,0,0,.1)}
.game{display:flex;align-items:center}
.icon{width:64px;height:64px;border-radius:14px;background:#bbdefb;display:flex;align-items:center;justify-content:center;font-size:28px;margin-right:16px}
.download{background:#1a73e8;color:#fff;text-decoration:none;padding:10px 18px;border-radius:20px;font-weight:bold}
textarea,input{width:100%;padding:10px;border-radius:12px;border:1px solid #ccc;margin-top:8px}
button{margin-top:10px;padding:10px;border:none;border-radius:20px;background:#1a73e8;color:#fff;cursor:pointer}
.comment{background:#e3f2fd;padding:10px;border-radius:12px;margin-top:8px;display:flex;justify-content:space-between;align-items:center}
.small{font-size:13px;color:#555}
</style>
</head>
<body>
<header>🎮 Tienda de Juegos</header>
<div class="container"><div class="game"><div class="icon">🎯</div><div><b>Frag Hack</b><div class="small">Shooter</div></div><a class="download" href="https://safefileku.com/download/tIHLINPxMIqdSXQz" target="_blank">Instalar</a></div>
<div class="game"><div class="icon">🌱</div><div><b>PVZL Fusión</b><div class="small">Estrategia</div></div><a class="download" href="https://www.mediafire.com/file/c55b13u28jxfif1/PLVZ_FUSI%25C3%2593N_%2528EN_ESPA%25C3%2591OL%2529.apk/file" target="_blank">Instalar</a></div>
<div class="game"><div class="icon">🧟</div><div><b>PVZL GRW</b><div class="small">Mods</div></div><a class="download" href="https://www.mediafire.com/file/gaurawdn8ogwl69/PLVZ_GRW_v0.8.apk/file" target="_blank">Instalar</a></div><div class="comments">
<h3>💬 Sugerir un juego</h3>
<textarea id="game" placeholder="Nombre del juego"></textarea>
<input type="number" id="stars" min="1" max="5" placeholder="Estrellas (1-5)">
<button onclick="send()">Enviar</button>
<div id="list"></div>
</div><div class="admin">
<h3>🔐 Admin Online</h3>
<input type="password" id="pass" placeholder="Contraseña admin">
<button onclick="login()">Entrar</button>
</div></div><script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-app-compat.js"></script><script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-database-compat.js"></script><script>
const firebaseConfig={
 apiKey:"TU_API_KEY",
 authDomain:"TU_PROYECTO.firebaseapp.com",
 databaseURL:"https://TU_PROYECTO-default-rtdb.firebaseio.com",
 projectId:"TU_PROYECTO"
};
firebase.initializeApp(firebaseConfig);
const db=firebase.database();
let admin=false;

function send(){
 const g=document.getElementById('game').value.trim();
 const s=document.getElementById('stars').value||0;
 if(!g)return alert('Escribe un juego');
 db.ref('sugerencias').push({juego:g,estrellas:s});
 document.getElementById('game').value='';
}

function show(){
 db.ref('sugerencias').on('value',snap=>{
  const list=document.getElementById('list');list.innerHTML='<h4>📌 Sugerencias</h4>';
  snap.forEach(c=>{
   const d=c.val();
   list.innerHTML+=`<div class="comment">${d.juego} (${d.estrellas}⭐) ${admin?`<button onclick="del('${c.key}')">🗑️</button>`:''}</div>`;
  });
 });
}

function del(id){db.ref('sugerencias/'+id).remove();}
function login(){if(document.getElementById('pass').value==='admin123'){admin=true;alert('Admin activado');show();}}
show();
</script></body>
</html>
