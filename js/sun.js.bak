/**
 * Created by clovisneto on 12/26/16.
 */
class Particle {
	constructor(x,y,hue,hasFirework, userMouseX, userMouseY){
		this.position = createVector(x,y);
		this.acceleration = createVector(0,0);
		this.firework = hasFirework;
		this.lifespan = 255;
		this.hue = hue;

		if(userMouseY){
			this.velocity = createVector(0, random(-17, -20));
		}else if(this.firework){
			this.velocity = createVector(0,random(-15, -10));

		}else {
			this.velocity = p5.Vector.random2D();
			this.velocity.mult(random(-21,15))
		}
	}

	get done(){
		if(this.lifespan <= 0){
			return true;
		}else {
			return false;
		}
	}

	bindForce(gravity){
		this.acceleration.add(gravity);
	}

	update(){
		if(!this.firework){
			this.velocity.mult(0.9);
			this.lifespan -= random(2,6);
		}

		this.velocity.add(this.acceleration);
		this.position.add(this.velocity);
		this.acceleration.mult(0);
	}

	show(){
		colorMode(HSB)

		if(this.firework) {
			strokeWeight(4);
			stroke(this.hue, 255, 255);
		}else {
			strokeWeight(2);
			stroke(this.hue, 255, 255, this.lifespan);
		}

		point(this.position.x, this.position.y);
	}
}
/**
 * Created by clovisneto on 12/26/16.
 */
class Firework {
	constructor(x,y){
		let positionX = x ? x : random(windowWidth);

		this.hue = random(255);
		this.firework = new Particle(positionX, windowHeight, this.hue, true, x, y);
		this.hasExploded = false;
		this.particles = [];
		this.mouseY = y;
	}

	explode(){
		for (var i=0; i<100; i++){
			let p = new Particle(this.firework.position.x, this.firework.position.y, this.hue);
			this.particles.push(p);
		}
	}

	get done(){
		if(this.hasExploded && this.particles.length === 0){
			return true;
		}else {
			return false;
		}
	}

	update(){
		if(!this.hasExploded){
			this.firework.bindForce(gravity);
			this.firework.update();

			if(this.firework.velocity.y >= 0 || (this.mouseY && this.mouseY >= this.firework.position.y)) {
				this.hasExploded = true;
				this.explode();
			}
		}

		for(var i=this.particles.length-1; i >= 0; i--){
			this.particles[i].bindForce(gravity);
			this.particles[i].update();

			if(this.particles[i].done){
				this.particles.splice(i,1);
			}
		}
	}

	show(){
		if(!this.hasExploded){
			this.firework.show();
		}

		for(var i=0; i < this.particles.length; i++){
			this.particles[i].show();
		}
	}
}

/**
 * Created by clovisneto on 12/26/16.
 */
let fireworks = [],
	appartments = [],
	qtd_apt = 10,
	columns = window.innerWidth/qtd_apt,
	gravity;

function setup(){
	createCanvas(windowWidth, windowHeight);
	colorMode(HSB);
	gravity = createVector(0, 0.2);
	strokeWeight(4)
	stroke(255);

	drawAppartments();
}

function drawAppartments(){
	columns = window.innerWidth/qtd_apt,
	appartments = [];

	for(var i=0; i<= columns;i++) {
		let h = random(60, 200);
		appartments.push({h: h, x: columns*i});
	}
}

function windowResized() {
	resizeCanvas(windowWidth, windowHeight);
}

function mouseDragged(){
	fireworks.push(new Firework(mouseX, mouseY));
}

function mousePressed(){
	fireworks.push(new Firework(mouseX, mouseY));
}

function draw(){
	colorMode(RGB)
	background('rgba(3, 10, 39, 0.2)');

	if(random(1) < 0.08){
		fireworks.push(new Firework());
	}

	for(var i = fireworks.length-1; i>=0; i--){
		fireworks[i].update();
		fireworks[i].show();

		if(fireworks[i].done){
			fireworks.splice(i,1)
		}
	}

	for(var i=0; i< appartments.length;i++){
		fill(0);
		noStroke();
		rect(appartments[i].x,height-appartments[i].h,columns,appartments[i].h);
	}
}