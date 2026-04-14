<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<title>CatGame GODMODE JV 🐱🔥</title>

<style>
body {
    margin:0;
    font-family:'Segoe UI',sans-serif;
    background:#0f172a;
    color:white;
}

header {
    background:#111827;
    padding:15px;
    display:flex;
    justify-content:space-between;
    border-bottom:2px solid #ff4f91;
}

button {
    padding:8px;
    border:none;
    border-radius:8px;
    background:#ff4f91;
    color:white;
    cursor:pointer;
    margin:4px;
}

.container {
    display:grid;
    grid-template-columns:repeat(auto-fit,minmax(220px,1fr));
    gap:20px;
    padding:20px;
}

.card {
    background:#1e293b;
    border-radius:12px;
    overflow:hidden;
    transition:0.3s;
}
.card:hover { transform:scale(1.05); }

.card img {
    width:100%;
    height:160px;
    object-fit:cover;
}

.modal {
    position:fixed;
    top:50%;
    left:50%;
    transform:translate(-50%,-50%);
    background:#1e293b;
    padding:20px;
    border-radius:12px;
    display:none;
    max-height:500px;
    overflow:auto;
}

.hpbar {
    height:12px;
    background:red;
}

.battle {
    display:flex;
    justify-content:space-between;
    align-items:center;
}

.battle img {
    width:120px;
    transition:0.2s;
}
</style>
</head>

<body>

<header>
<div>🐱 CatGame GODMODE JV</div>
<div>
💰 <span id="saldo"></span> |
⭐ <span id="xp"></span> |
🏆 Lv <span id="level"></span>
</div>
</header>

<div style="text-align:center;">
<button onclick="Game.generateCats()">Gerar</button>
<button onclick="UI.openInventory()">Coleção</button>
<button onclick="Game.work()">Trabalhar</button>
<button onclick="UI.chooseBattle()">Batalhar</button>
</div>

<div class="container" id="galeria"></div>
<div class="modal" id="modal"></div>

<script>

/* =========================
   ===== NOMES =====
========================= */
const nomesBase = ["João","Pedro","Lucas","Mateus","Gabriel","Rafael","Arthur","Enzo","Leonardo","Davi",
"Bruno","Carlos","Diego","Eduardo","Felipe","Gustavo","Henrique","Igor","Kaique",
"Leandro","Marcelo","Nicolas","Otávio","Paulo","Renato","Samuel","Thiago","Victor","Yuri",
"Alan","André","Antônio","Augusto","Bernardo","Caio","Cauã","César","Cristiano","Danilo",
"Douglas","Erick","Fábio","Fernando","Francisco","Gilberto","Hugo","Ian","Ivan","Jorge",
"José","Julio","Kevin","Luan","Luiz","Marcos","Matheus","Murilo","Nathan","Pablo",
"Patrick","Ramon","Rodrigo","Sérgio","Vitor","Wesley","William","Zeca","Adriano","Alberto",

"Maria","Ana","Julia","Beatriz","Sofia","Isabela","Helena","Alice","Luna","Clara",
"Larissa","Camila","Fernanda","Gabriela","Juliana","Letícia","Mariana","Natália",
"Patrícia","Vanessa","Bianca","Carolina","Daniela","Elisa","Flávia","Giovana","Heloísa",
"Isadora","Jéssica","Karen","Lívia","Lorena","Luana","Mirela","Nayara","Priscila",
"Raquel","Sabrina","Tatiane","Valéria","Yasmin","Aline","Bruna","Cecília","Débora",
"Evelyn","Fabiana","Geovana","Iara","Janaina","Kátia","Laís","Mônica","Nádia","Rita",

"John","Michael","William","James","Alexander","Daniel","Christopher","Nathan",
"Logan","Ethan","Noah","Liam","Oliver","Henry","Jack","Leo","Benjamin","Elijah",
"Lucas","Mason","Sebastian","Aiden","Jackson","Carter","Wyatt","Jayden","Luke",
"David","Isaac","Grayson","Samuel","Owen","Julian","Levi","Mateo","Anthony","Dylan",
"Andrew","Joshua","Ezra","Hudson","Charles","Caleb","Ryan","Nathaniel","Aaron","Eli",

"Emily","Olivia","Sophia","Amelia","Isabella","Mia","Charlotte","Lily","Chloe",
"Grace","Hannah","Zoe","Ella","Scarlett","Aria","Layla","Avery","Nora","Riley",
"Victoria","Lucy","Paisley","Everly","Anna","Caroline","Nova","Genesis","Emilia",
"Kennedy","Samantha","Maya","Willow","Kinsley","Naomi","Aaliyah","Elena","Sarah",
"Ariana","Allison","Gabriella","Madison","Hailey","Autumn","Nevaeh","Natalie",

"Anubis","Osiris","Horus","Ramses","Set","Ra","Thoth","Cleopatra","Nefertiti",
"Bastet","Hathor","Sekhmet","Khonsu","Ptah","Sobek","Amun","Isis",

"Zeus","Ares","Hades","Poseidon","Apollo","Hermes","Athena","Artemis","Hera",
"Dionysus","Perseus","Achilles","Odysseus","Orion","Atlas",

"Simba","Nala","Milo","Otis","Felix","Garfield","Tom","Jerry","Max","Rocky",
"Charlie","Buddy","Toby","Oscar","Coco","Simone","Loki","Thor","Odin","Freya",
"Shadow","Lucky","Smokey","Tiger","Leo","Misty","Angel","Bella","Kitty","Ziggy"];

const sobrenomes = ["Silva","Souza","Costa","Smith","Brown","Khan"];
const titulos = ["Lord","Rei","Mestre","Supremo","Imperador","Guardião"];
const extras = ["I","II","III","IV","Prime","Alpha","Omega"];

/* =========================
   ===== GAME =====
========================= */
const Game = {

saldo:500,
xp:0,
level:1,
inventory:[],
equipped:null,

random(a){ return a[Math.floor(Math.random()*a.length)]; },

gerarNome(){
return `${Math.random()>0.5?this.random(titulos):""} ${this.random(nomesBase)} ${this.random(sobrenomes)} ${Math.random()>0.6?this.random(extras):""}`.replace(/\s+/g,' ').trim();
},

raridade(){
let r=Math.random();
if(r<0.5) return {nome:"Comum",cor:"gray",mult:1};
if(r<0.75) return {nome:"Raro",cor:"blue",mult:1.5};
if(r<0.9) return {nome:"Épico",cor:"purple",mult:2};
if(r<0.98) return {nome:"Lendário",cor:"gold",mult:3};
return {nome:"Mitico",cor:"red",mult:5};
},

createCat(){
let rar=this.raridade();
let atk=Math.floor((Math.random()*10+5)*rar.mult);
let def=Math.floor((Math.random()*10+5)*rar.mult);
let hp=Math.floor(60*rar.mult);

return {
nome:this.gerarNome(),
raridade:rar,
atk,def,hp,
crit:Math.random()*0.2,
dodge:Math.random()*0.15,
preco:Math.floor((atk+def)*12*rar.mult),
img:`https://cataas.com/cat?${Math.random()}`
};
},

generateCats(){
let g=document.getElementById("galeria");

for(let i=0;i<6;i++){
let c=this.createCat();

let card=document.createElement("div");
card.className="card";

card.innerHTML=`
<img src="${c.img}">
<div style="padding:10px">
<div>${c.nome}</div>
<div style="color:${c.raridade.cor}">${c.raridade.nome}</div>
<div>⚔️${c.atk} 🛡️${c.def}</div>
<div>💰${c.preco}</div>
<button onclick='Game.buy(this, ${JSON.stringify(c)})'>Comprar</button>
</div>`;

g.appendChild(card);
}
},

buy(btn, c){
    if(this.saldo < c.preco) return alert("Sem dinheiro");

this.saldo -= c.preco;
this.inventory.push(c);
this.xp += 10;
this.levelUp();
this.update();
btn.innerText = "Comprado ✅";
btn.disabled = true;
btn.style.background = "gray";
},

work(){
let ganho=Math.floor(Math.random()*150)+50;
this.saldo+=ganho;
this.xp+=5;
this.levelUp();
alert("Ganhou "+ganho);
this.update();
},

levelUp(){
if(this.xp>=100){
this.xp=0;
this.level++;
alert("LEVEL UP!");
}
},

update(){
saldo.innerText=this.saldo;
xp.innerText=this.xp;
level.innerText=this.level;
}

};

/* =========================
   ===== UI =====
========================= */
const UI = {

modal:document.getElementById("modal"),

openInventory(){
this.modal.style.display="block";
this.modal.innerHTML="<h3>🐱 Coleção</h3>";

Game.inventory.forEach((c,i)=>{
this.modal.innerHTML+=`
<div>
${c.nome} (${c.raridade.nome})
<button onclick="Game.equippedIndex=${i};UI.close()">Equipar</button>
<button onclick="Battle.start(${i})">Lutar</button>
</div>`;
});

this.modal.innerHTML+=`<button onclick="UI.close()">Fechar</button>`;
},

chooseBattle(){
if(Game.inventory.length==0) return alert("Sem gatos");
this.openInventory();
},

close(){ this.modal.style.display="none"; }

};

/* =========================
   ===== BATALHA =====
========================= */
const Battle = {

p:null,
e:null,

start(i){
this.p=JSON.parse(JSON.stringify(Game.inventory[i]));
this.e=Game.createCat();
this.render();
},

attack(){

if(Math.random()<this.e.dodge){
alert("Inimigo desviou!");
}else{
let dmg=this.p.atk;
if(Math.random()<this.p.crit){ dmg*=2; alert("CRÍTICO!"); }
this.e.hp-=dmg;
}

if(Math.random()<this.p.dodge){
alert("Você desviou!");
}else{
this.p.hp-=this.e.atk;
}

if(this.e.hp<=0){
Game.saldo+=this.e.preco;
Game.xp+=30;
alert("Vitória!");
UI.close();
Game.update();
return;
}

if(this.p.hp<=0){
alert("Derrota!");
UI.close();
return;
}

this.render();
},

render(){

UI.modal.style.display="block";

UI.modal.innerHTML=`
<h3>⚔️ Batalha</h3>

<div class="battle">
<div>
<img id="p" src="${this.p.img}">
<div>${this.p.nome}</div>
<div class="hpbar" style="width:${this.p.hp}px"></div>
</div>

<div>
<img id="e" src="${this.e.img}">
<div>${this.e.nome}</div>
<div class="hpbar" style="width:${this.e.hp}px"></div>
</div>
</div>

<button onclick="Battle.animate()">Atacar</button>
<button onclick="UI.close()">Fugir</button>
`;
},

animate(){
let p=document.getElementById("p");
let e=document.getElementById("e");

p.style.transform="translateX(50px)";
e.style.transform="translateX(-50px)";

setTimeout(()=>{
p.style.transform="translateX(0)";
e.style.transform="translateX(0)";
Battle.attack();
},200);
}

};

// INIT
Game.update();
Game.generateCats();

</script>

</body>
</html>
