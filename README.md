# PingPong
🎮 Jogo que criei no curso lógica de programação da Alura

Esse é o codigo que eu executei pelo p5.js 

//variáveis da bolinha
let xBolinha = 300;
let yBolinha = 200;
let diametro = 25;
let raio = diametro / 2;

//velocidade da bolinha

let velocidadeXBolinha = 6;
let velocidadeYBolinha = 6;

//variáveis da raquete

let xRaquete = 5;
let yRaquete = 150;
let raqueteComprimento = 10;
let raqueteAltura = 90;

let colidiu = false;

//placar do jogo
let meusPontos = 0;
let pontosOponente = 0;


//variáveis do oponente
let xRaqueteOponente = 585;
let yRaqueteOponente = 150;
let chanceDeErrar = 2;

//sons do jogo 
let raquetada;
let ponto;
let trilha;


function preload(){
  trilha = loadSound("trilha.mp3");
  ponto = loadSound("ponto.mp3");
  raquetada = loadSound("raquetada.mp3");
}
function setup() {
  createCanvas(600, 400);
  trilha.loop();
}

function draw() {
  background(0);
  mostraBolinha();
  movimentaBolinha();
  verificaColisaoBorda();
  mostraRaquete(xRaquete, yRaquete);
  movimentaMinhaRaquete();
  movimentaRaqueteOponente();
  mostraRaquete(xRaqueteOponente, yRaqueteOponente);
  colisaoMinhaRaqueteBiblioteca();
  colisaoRaqueteOponenteBiblioteca();
  incluiPlacar();
  marcaPonto();
  calculaChanceDeErrar();
  bolinhaNaoFicaPresa();
  
  
}
function mostraBolinha(){
  circle(xBolinha, yBolinha, diametro)  
}

function movimentaBolinha(){
  xBolinha += velocidadeXBolinha
  yBolinha += velocidadeYBolinha
}

function verificaColisaoBorda(){
   if (xBolinha + raio > width ||
     xBolinha - raio < 0){
    velocidadeXBolinha *= -1;
  }
  if (yBolinha + raio > height ||
     yBolinha - raio < 0){
    velocidadeYBolinha *= -1;
  
  }
}

function mostraRaquete(x,y){
  rect(x, y, raqueteComprimento, raqueteAltura);
}

function movimentaMinhaRaquete(){
  if (keyIsDown(UP_ARROW)){
  yRaquete -= 10;
  }
  if (keyIsDown(DOWN_ARROW)){
    yRaquete += 10;

}
  }
function movimentaRaqueteOponente(){
  velocidadeYOponente = yBolinha - yRaqueteOponente - 
    raqueteComprimento / 2 - 30;
  yRaqueteOponente += velocidadeYOponente
}

function colisaoMinhaRaqueteBiblioteca(x,y){
 colidiu=
   collideRectCircle(xRaquete,yRaquete,raqueteComprimento,raqueteAltura,xBolinha,yBolinha,raio);
	if (colidiu){
	  velocidadeXBolinha *= -1;
  raquetada.play();
    }
}
function colisaoRaqueteOponenteBiblioteca(){
  colidiu=
   collideRectCircle(xRaqueteOponente,yRaqueteOponente,raqueteComprimento,raqueteAltura,xBolinha,yBolinha,raio);
	if (colidiu){
	  velocidadeXBolinha *= -1;
      raquetada.play();
}
}

function incluiPlacar(){
  stroke(255)
  textAlign(CENTER)
  textSize(16)
  fill(color(255, 140, 0))
  rect(150, 10, 40, 20)
  fill(255)
  text(meusPontos, 170,26)
  fill(color(255, 140, 90))
  rect(450, 10, 40, 20)
  fill(255)
  text(pontosOponente, 470, 26)
}


function marcaPonto(){
  if (xBolinha > 585){
    meusPontos += 1;
    ponto.play();
  }
  if (xBolinha < 15){
    pontosOponente += 1;
    ponto.play();
  }
}

function movimentaRaqueteOponente(){
  velocidadeYOponente = yBolinha -yRaqueteOponente - raqueteComprimento / 2 - 30;
  yRaqueteOponente += velocidadeYOponente + chanceDeErrar
  calculaChanceDeErrar()
}


function calculaChanceDeErrar() {
  if (pontosOponente >= meusPontos) {
    chanceDeErrar += 1
    if (chanceDeErrar >= 50){
    chanceDeErrar = 40
    }
  } else {
    chanceDeErrar -= 1
    if (chanceDeErrar <= 45){
    chanceDeErrar = 35
    }
  }
}

function bolinhaNaoFicaPresa(){
    if (xBolinha - raio < 0){
    XBolinha = 25
    }
}
