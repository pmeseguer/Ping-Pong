# Ping-Pong
import ddf.minim.*;// sonido
Minim soundengine;
AudioSample sonido1;
AudioSample sonido2;
AudioSample sonido3;
int x;//              variables
int y;
int vx;
int vy;
int yb1;
int yb2;
int puntuacion1;
int puntuacion2;
boolean menu = false;
boolean w,s,a,b;
PImage imagenfondo;
PImage imagenmenu;
PImage player1;
PImage player2;
void setup(){
  soundengine = new Minim(this);
sonido1 = soundengine.loadSample("1.mp3", 1024);
sonido2 = soundengine.loadSample("2.mp3", 1024);
sonido3 = soundengine.loadSample("3.mp3", 1024);
  frameRate(90);
  size(800,450);
  x=100;
  y=200;
  vx=2;
  vy=3;
  yb1=100;
  yb2=100;
  puntuacion1 = 0;
  puntuacion2 = 0;
  player1 = loadImage("player1.jpg");
  player2 = loadImage("player2.jpg");
  imagenfondo = loadImage("fondo1.jpg");
  imagenmenu = loadImage("fondomenu.jpg");
  //image (imagenfondo, 0, 0);
}
void draw(){
  if(menu){
  image (imagenfondo, 0, 0);//  fondo
    //background(0);
    if(puntuacion1 > 2) {//    fin de juego
      image (player1, 0, 0);
    }
    if(puntuacion2 > 2) {
      image (player2, 0, 0);
    }
    textSize(100);
    fill(255);
    text(puntuacion1, 249, 100);// puntuaciones
    text("-", 350, 100);
    text(puntuacion2, 450, 100);
    fill(255);//                  figuras
    if (puntuacion1 < 3 && puntuacion2 < 3){
    ellipse(x,y,45,45);
    rect(10,yb1,30,135);
    rect(760,yb2,30,135);
  x= x+vx;
  y= y+vy;
    }
  //                                CHOQUE BARRAS
  /*if(x<62 && y>yb1 && y<yb1+180){//barra izquierda
    vx= vx*-1;
    }*/
   // vx= vx+1;//                  aceleracion bola
  if (x<62 && y>yb1 && y<yb1+45){//  deformacion 
    vx=vx*-1;
    vy = vy-2;
    sonido1.trigger();// sonido
  }else if (x<62 && y> yb1+46 && y< yb1+90){ 
    vx=vx*-1;
    sonido1.trigger();// sonido
  }else if ( x<62 && y> yb1+91 && y< yb1+135){
    vx= vx*-1;
    vy= vy+2;
    sonido1.trigger();// sonido
  }
  /*if(x>width-62 && y>yb2 && y<yb2+180){//barra derecha
    vx= vx*-1;
    vx= vx-1;//aceleracion bola
  }*/
  if (x>width-62 && y>yb2 && y<yb2+45){//  deformacion 
    vx=vx*-1;
    vy = vy-2;
    sonido1.trigger();// sonido
    vx= vx-1;//aceleracion bola
  }else if (x>width-62 && y> yb2+46 && y< yb2+90){ 
    vx=vx*-1;
    sonido1.trigger();// sonido
    vx= vx-1;//aceleracion bola
  }else if ( x>width-62 && y> yb2+91 && y< yb2+135){
    vx= vx*-1;
    vy= vy+2;
    sonido1.trigger();// sonido
    vx= vx-1;//aceleracion bola
  }
  //                                CHOQUE PARED
 /* if(x>width-22||x<22){
    vx=vx*-1;
  }*/
  if(y>height-22||y<22){
    vy=vy*-1;
    sonido2.trigger();// sonido
    };
    if(x>width-22){
       x=100;
       y=200;
       vx=2;
       vy=3;
       sonido3.trigger();// sonido
       puntuacion1 = puntuacion1 +1;
    }else if(x<22){
      x=100;
      x=700;
      y=200;
      vx=-2;
      vy=3;
      sonido3.trigger();//sonido
      puntuacion2 = puntuacion2 +1;
    }
  //                             VARIABLES DE MOVIMIENTO de las barras
  if (a) {
    yb2=yb2-5;
  }
  if (b) {
    yb2=yb2+5;
  }
  if (w) {
    yb1=yb1-5;
  }
  if (s) {
    yb1=yb1+5;
  }
  if(yb1<0){
  yb1=0;
  }else if(yb1>height-135) {
  yb1=height-135;
  }
  if(yb2<0){
  yb2=0;
  }else if(yb2>height-135) {
  yb2=height-135;
  }
  }else{//                       menu de inicio
    image (imagenmenu, 0, 0);
      x=100;
  y=200;
  vx=2;
  vy=3;
  yb1=100;
  yb2=100;
  puntuacion1 = 0;
  puntuacion2 = 0;
  }
};
//                               control botones
void keyPressed(){
  if (key == ' '){
   menu=!menu;
   sonido1.trigger();
  }
  if (key=='w'){
    w=true;
  }
  if (key=='s'){
    s=true;
  }
  if (keyCode==UP){
    a=true;
  }
  if (keyCode==DOWN){
    b=true;
  }
}
void keyReleased() {
  //if (key=='q'){
   // menu=false;
  //}
  if (key=='w'){
    w=false;
  }
  if (key=='s'){
    s=false;
  }
   if (keyCode==UP){
    a=false;
  }
  if (keyCode==DOWN){
    b=false;
  }
}
