# P5js-Magnetron-Electrons
P5js animation to visualize the motion of electrons inside a microwave's magnetron.  
It uses OOP, each electron is an object with its own methods
## Preview
![Preview](https://github.com/frephs/P5js-Magnetron-Electrons/blob/main/preview.gif)  
[Preview the animations here](https://htmlpreview.github.io/?https://github.com/frephs/P5js-Magnetron-Electrons/blob/main/index.html)

 

## Sketch 
```
//autore: Francesco Genovese
let electrons = [];
class electron{
	//metodo costruttore
	constructor(x,y,a,r){
		this.x= x;        
		this.y = y;     
		this.a = a; //angolo
		this.r = r;  //distanza dal centro
		this.rSpeed= 10;
		this.tSpeed= 35.88;
	}
	//metodo che muove gli elettroni
	move(){
		//gli elettroni si muovono di moto rettilineo
		this.r = this.r + this.rSpeed;
		//composto ad un moto circolare uniforme
		this.a = this.a + this.tSpeed;
        this.x = cx+this.r*cos(+this.a); 
		this.y = cy+this.r*sin(-this.a);
	}
	//visualizza gli elettroni sul canvas
	show(){
		ellipse(this.x,this.y,5);
	} 
}


//SETUP
function setup() {
	frameRate(20);
	createCanvas(windowWidth, windowHeight);
	background(220);
	for(var i=0;i<10;i++){
		e= new electron(windowWidth/2,windowHeight/2,360/10*i,45);
		electrons.push(e);
		console.log(electrons)
	}
}

//loop per disegnare
function draw() {
	cx = windowWidth/2;
	cy = windowHeight/2;
	
  //disegno il solenoide
	ellipse(cx,cy,100); ellipse(cx,cy,50);

	for(let electron of electrons){
		if(dist(cx, cy, electron.x, electron.y)<200){
			electron.move();
			electron.show();
		}
		else{
			electron.r= 45;
			electron.move();
			electron.show();
			background(220);ellipse(cx,cy,100); ellipse(cx,cy,50);

		}
	}
}

```
