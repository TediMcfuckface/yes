var circles = []
var total = 100
var img;
function setup() {
	createCanvas(600, 600);;
	
	loadImage('XXX;)') , function(img2) {
	  background(30)
    img = img2

		for(var i = 0; i < total; i++){
			circles[i] = {};
			circles[i].prevPos = {x: width/2, y: height/2}
			circles[i].pos = {x: width/2, y: height/2}
			circles[i].dir = random() > 0.5 ? 1 : -1
			circles[i].radius = random(3, 10)
			circles[i].angle = 0
			
		}
  };
}

function draw() {
	//image loading
  if(!img){
	 background(30);
   if(frameCount%2) text("loading", width/2, height/2);
   return;
  }
	
	for(var i = 0; i < total; i++){
		var circle = circles[i]
		circle.angle += 1/circle.radius*circle.dir

		circle.pos.x += cos(circle.angle) * circle.radius
		circle.pos.y += sin(circle.angle) * circle.radius
		if(brightness(img.get(round(circle.pos.x), round(circle.pos.y))) > 70 || circle.pos.x < 0 || circle.pos.x > width || circle.pos.y < 0 || circle.pos.y > height){
			circle.dir *= -1
			circle.radius = random(3, 10)
			circle.angle += PI
		}
		stroke(img.get(circle.pos.x, circle.pos.y))
		line(circle.prevPos.x, circle.prevPos.y, circle.pos.x, circle.pos.y)

		circle.prevPos.x = circle.pos.x
		circle.prevPos.y = circle.pos.y
	}
}
