Student-vs-Zombies
==================

Alpha version of a math game shooting zombies for every right equation.


<!DOCTYPE HTML>
<html lang = "en">
<head>
	<meta charset = "utf-9"/>
	<title>Student VS Zombies</title>
	<audio autoplay controls loop>
	</audio>
</head>
<body>
	<canvas id = 'canvasBg' width = 900 height = 600 style = "border:10px solid purple">
	</canvas>
	<canvas id = 'canvasGun' width = 900 height = 600 style = "display:block;margin: -615px 315px">
	</canvas>
	<canvas id = 'canvasZombie1' width = 900 height = 600 style = "display:block;margin: -615px 315px">
	</canvas>
	<canvas id = 'canvasZombie2' width = 900 height = 600 style = "display:block;margin: -615px 315px ">
	</canvas>
	<canvas id = 'canvasZombie3' width = 900 height = 600 style = "display:block;margin: -615px 315px ">
	</canvas>
	<canvas id = 'canvasBullet' width = 900 height = 600 style = "display:block;margin: -615px 315px ">
	</canvas>
	<script>
		var canvasBg = document.getElementById('canvasBg');
		var ctxBg = canvasBg.getContext('2d');
		var canvasGun = document.getElementById('canvasGun');
		var ctxGun = canvasGun.getContext('2d');
		var canvasZombie1 = document.getElementById('canvasZombie1');
		var ctxZombie1 = canvasZombie1.getContext('2d');
		var canvasZombie2 = document.getElementById('canvasZombie2');
		var ctxZombie2 = canvasZombie2.getContext('2d');
		var canvasZombie3 = document.getElementById('canvasZombie3');
		var ctxZombie3 = canvasZombie3.getContext('2d');
		var canvasBullet = document.getElementById('canvasBullet');
		var ctxBullet = canvasBullet.getContext('2d');
		var bgWidth = 900;
		var bgHeight = 600;
		var requestAnimFrame = window.requestAnimationFrame ||			// method to request animation frame for browser
					   window.webkitRequestAnimationFrame ||
					   window.mozRequestAnimationFrame ||
					   window.msRequestAnimationFrame ||
					   window.oRequestAnimationFrame;
					   
		document.addEventListener('keydown', checkKeyDown);
		var imgSprite = new Image();
		imgSprite.src = 'sprite.png';
		imgSprite.addEventListener('load', init, false);
		
		var isPlaying = true;
		var gun = new Gun;
		var zombie1 = new Zombie1; 
		var zombie2 = new Zombie2;
		var zombie3 = new Zombie3;
		var bullet = new Bullet;
		var speed = 1;
		var counter = 0;
		
		// main functions
		function init(){
			for(var i=0; i ; i ++){
				startLoop();
			}
		}
		
		function startLoop(){
			for(var i=0; i < 1000; i ++){
			counter ++;
			ctxBg.drawImage(imgSprite,0,0,bgWidth,bgHeight,0,0,bgWidth,bgHeight);
			zombie1.draw();
			zombie2.draw();
			zombie3.draw();
			updateBullet();
			clearCtxBullet();
			ctxBullet.drawImage(imgSprite,bullet.srcX,bullet.srcY,bullet.width,bullet.height,bullet.drawX,bullet.drawY,bullet.width,bullet.height);
			ctxGun.drawImage(imgSprite,gun.srcX,gun.srcY,gun.width,gun.height,gun.drawX,gun.drawY,gun.width,gun.height);
			//checkKeyDown();
			requestAnimFrame(startLoop);
			}
		}
		
		function updateBullet(){
			bullet.drawY -= speed;
		}
		
		function Gun(){
			this.srcX = 400;
			this.srcY = 600;
			this.width = 100 ;
			this.height = 100;
			this.drawX = bgWidth/2 - this.width/2;
			this.drawY = bgHeight - this.height;
		}
		
		function clearCtxGun(){
			ctxGun.clearRect(0,0,bgWidth,bgHeight);
		}
		
		function Zombie1(){
			this.srcX = 150;
			this.srcY = 600;
			this.width = 50 ;
			this.height = 100;
			this.drawX = 0;
			this.drawY = bgHeight - this.height;
		}
		
		Zombie1.prototype.draw = function(){
			ctxZombie1.drawImage(imgSprite,this.srcX,this.srcY,this.width,this.height,this.drawX,this.drawY,this.width,this.height);
		};		
		
		function clearCtxZombie1(){
			ctxZombie1.clearRect(0,0,bgWidth,bgHeight);
		}
		
		function Zombie2(){
			this.srcX = 0;
			this.srcY = 600;
			this.width = 50 ;
			this.height = 100;
			this.drawX = bgWidth - this.width;
			this.drawY = bgHeight - this.height;
		}
		
		Zombie2.prototype.draw = function(){
			ctxZombie2.drawImage(imgSprite,this.srcX,this.srcY,this.width,this.height,this.drawX,this.drawY,this.width,this.height);
		};		
		
		function clearCtxZombie2(){
			ctxZombie2.clearRect(0,0,bgWidth,bgHeight);
		}
		
		function Zombie3(){
			this.srcX = 0;
			this.srcY = 700;
			this.width = 100 ;
			this.height = 50;
			this.drawX = bgWidth/2 - this.width/2;
			this.drawY = 45;
		
		}
		
		Zombie3.prototype.draw = function(){
			ctxZombie3.drawImage(imgSprite,this.srcX,this.srcY,this.width,this.height,this.drawX,this.drawY,this.width,this.height);
		};		
		
		function clearCtxZombie3(){
			ctxZombie3.clearRect(0,0,bgWidth,bgHeight);
		}
		
		function Bullet(){
			this.srcX = 109;
			this.srcY = 709;
			this.width = 9;
			this.height = 9;
			this.drawX = 430;
			this.drawY = 560;
			this.isShot = false;
			this.direction = 3;
		}		
		
		function clearCtxBullet(){
			ctxBullet.clearRect(0,0,bgWidth,bgHeight);
		}
		
		
		function checkKeyDown(e){
			if(e.keyCode == 37){ //left key
				bullet.direction = 1;
				e.preventDefault();
				clearCtxGun();
				ctxGun.drawImage(imgSprite,gun.srcX - gun.width,gun.srcY,gun.width,gun.height,gun.drawX,gun.drawY,gun.width,gun.height);
			}
			if(e.keyCode == 38){ //up key
				bullet.direction = 3;
				e.preventDefault();
				clearCtxGun();
				ctxGun.drawImage(imgSprite,gun.srcX,gun.srcY,gun.width,gun.height,gun.drawX,gun.drawY,gun.width,gun.height);
			}
			if(e.keyCode == 39){ //right key
				bullet.direction = 2;
				e.preventDefault();
				clearCtxGun();
				ctxGun.drawImage(imgSprite,gun.srcX + gun.width,gun.srcY,gun.width,gun.height,gun.drawX,gun.drawY,gun.width,gun.height);
			}
			if(e.keyCode == 32 && !bullet.isShot){ // spacebar
				e.preventDefault();
				clearCtxBullet();
				bullet.isShot = true;
			}
		}
		
	</script>

</body>


</html><!DOCTYPE HTML>
<html lang = "en">
<head>
	<meta charset = "utf-9"/>
	<title>Student VS Zombies</title>
	<audio autoplay controls loop>
	</audio>
</head>
<body>
	<canvas id = 'canvasBg' width = 900 height = 600 style = "border:10px solid purple">
	</canvas>
	<canvas id = 'canvasGun' width = 900 height = 600 style = "display:block;margin: -615px 315px">
	</canvas>
	<canvas id = 'canvasZombie1' width = 900 height = 600 style = "display:block;margin: -615px 315px">
	</canvas>
	<canvas id = 'canvasZombie2' width = 900 height = 600 style = "display:block;margin: -615px 315px ">
	</canvas>
	<canvas id = 'canvasZombie3' width = 900 height = 600 style = "display:block;margin: -615px 315px ">
	</canvas>
	<canvas id = 'canvasBullet' width = 900 height = 600 style = "display:block;margin: -615px 315px ">
	</canvas>
	<script>
		var canvasBg = document.getElementById('canvasBg');
		var ctxBg = canvasBg.getContext('2d');
		var canvasGun = document.getElementById('canvasGun');
		var ctxGun = canvasGun.getContext('2d');
		var canvasZombie1 = document.getElementById('canvasZombie1');
		var ctxZombie1 = canvasZombie1.getContext('2d');
		var canvasZombie2 = document.getElementById('canvasZombie2');
		var ctxZombie2 = canvasZombie2.getContext('2d');
		var canvasZombie3 = document.getElementById('canvasZombie3');
		var ctxZombie3 = canvasZombie3.getContext('2d');
		var canvasBullet = document.getElementById('canvasBullet');
		var ctxBullet = canvasBullet.getContext('2d');
		var bgWidth = 900;
		var bgHeight = 600;
		var Equations = new Array();
		var requestAnimFrame = window.requestAnimationFrame ||			// method to request animation frame for browser
					   window.webkitRequestAnimationFrame ||
					   window.mozRequestAnimationFrame ||
					   window.msRequestAnimationFrame ||
					   window.oRequestAnimationFrame;
					   
		document.addEventListener('keydown', checkKeyDown);
		var imgSprite = new Image();
		imgSprite.src = 'sprite.png';
		imgSprite.addEventListener('load', init, false);
		
		var isPlaying = true;
		var gun = new Gun;
		var zombie1 = new Zombie1; 
		var zombie2 = new Zombie2;
		var zombie3 = new Zombie3;
		var bullet = new Bullet;
		var speed = 3;
		var counter = 0;
		
		// main functions
		
		setInterval(startLoop, 1000/45);
		
		function startLoop(){
			ctxBg.drawImage(imgSprite,0,0,bgWidth,bgHeight,0,0,bgWidth,bgHeight);
			clearCtxZombie1();
			clearCtxZombie2();
			clearCtxZombie3();
			zombie1.draw();
			zombie2.draw();
			zombie3.draw();
			update();
			clearCtxBullet();
			ctxBullet.drawImage(imgSprite,bullet.srcX,bullet.srcY,bullet.width,bullet.height,bullet.drawX,bullet.drawY,bullet.width,bullet.height);
			ctxGun.drawImage(imgSprite,gun.srcX,gun.srcY,gun.width,gun.height,gun.drawX,gun.drawY,gun.width,gun.height);
			checkKeyDown();
		}
		
		function update(){
			bullet.drawY -= speed;
			zombie1.drawX += speed;
			zombie2.drawX -= speed;
			zombie3.drawY += speed;
		}
		
		function Gun(){
			this.srcX = 400;
			this.srcY = 600;
			this.width = 100 ;
			this.height = 100;
			this.drawX = bgWidth/2 - this.width/2;
			this.drawY = bgHeight - this.height;
		}
		
		function clearCtxGun(){
			ctxGun.clearRect(0,0,bgWidth,bgHeight);
		}
		
		function Zombie1(){
			this.srcX = 150;
			this.srcY = 600;
			this.width = 50 ;
			this.height = 100;
			this.drawX = 0;
			this.drawY = bgHeight - this.height;
			this.part = 1;
			
		}
		
		Zombie1.prototype.draw = function(){
			if(this.part < 8){
				ctxZombie1.drawImage(imgSprite,this.srcX,this.srcY,this.width,this.height,this.drawX,this.drawY,this.width,this.height);
				this.part ++;
			}
			else if(this.part < 16){
				ctxZombie1.drawImage(imgSprite,this.srcX + this.width,this.srcY,this.width,this.height,this.drawX,this.drawY,this.width,this.height);
				this.part ++;
			}
			else if(this.part < 24){
				ctxZombie1.drawImage(imgSprite,this.srcX + this.width * 2,this.srcY,this.width,this.height,this.drawX,this.drawY,this.width,this.height);
				this.part ++;
			}
			else{
				ctxZombie1.drawImage(imgSprite,this.srcX,this.srcY,this.width,this.height,this.drawX,this.drawY,this.width,this.height);
				this.part = 1;
			}
		};		
		
		

						
		
		function clearCtxZombie1(){
			ctxZombie1.clearRect(0,0,bgWidth,bgHeight);
		}
		
		function Zombie2(){
			this.srcX = 0;
			this.srcY = 600;
			this.width = 50 ;
			this.height = 100;
			this.drawX = bgWidth - this.width;
			this.drawY = bgHeight - this.height;
			this.part = 0;
		}
		
		Zombie2.prototype.draw = function(){
			if(this.part < 8){
				ctxZombie2.drawImage(imgSprite,this.srcX,this.srcY,this.width,this.height,this.drawX,this.drawY,this.width,this.height);
				this.part ++;
			}
			else if(this.part < 16){
				ctxZombie2.drawImage(imgSprite,this.srcX + this.width,this.srcY,this.width,this.height,this.drawX,this.drawY,this.width,this.height);
				this.part ++;
			}
			else if(this.part < 24){
				ctxZombie2.drawImage(imgSprite,this.srcX + this.width * 2,this.srcY,this.width,this.height,this.drawX,this.drawY,this.width,this.height);
				this.part ++;
			}
			else{
				ctxZombie2.drawImage(imgSprite,this.srcX,this.srcY,this.width,this.height,this.drawX,this.drawY,this.width,this.height);
				this.part = 1;
			}
		};			
		
		function clearCtxZombie2(){
			ctxZombie2.clearRect(0,0,bgWidth,bgHeight);
		}
		
		function Zombie3(){
			this.srcX = 0;
			this.srcY = 700;
			this.width = 100 ;
			this.height = 50;
			this.drawX = bgWidth/2 - this.width/2;
			this.drawY = 45;
			this.part = 0;
		}
		
		Zombie3.prototype.draw = function(){
			if(this.part < 8){
				ctxZombie3.drawImage(imgSprite,this.srcX,this.srcY,this.width,this.height,this.drawX,this.drawY,this.width,this.height);
				this.part ++;
			}
			else if(this.part < 16){
				ctxZombie3.drawImage(imgSprite,this.srcX,this.srcY + this.height,this.width,this.height,this.drawX,this.drawY,this.width,this.height);
				this.part ++;
			}
			else if(this.part < 24){
				ctxZombie3.drawImage(imgSprite,this.srcX,this.srcY + this.height * 2,this.width,this.height,this.drawX,this.drawY,this.width,this.height);
				this.part ++;
			}
			else{
				ctxZombie3.drawImage(imgSprite,this.srcX,this.srcY,this.width,this.height,this.drawX,this.drawY,this.width,this.height);
				this.part = 1;
			}
		}
		
		function clearCtxZombie3(){
			ctxZombie3.clearRect(0,0,bgWidth,bgHeight);
		}
		
		function Bullet(){
			this.srcX = 109;
			this.srcY = 709;
			this.width = 9;
			this.height = 9;
			this.drawX = 430;
			this.drawY = 560;
			this.isShot = false;
			this.direction = 3;
		}		
		
		function clearCtxBullet(){
			ctxBullet.clearRect(0,0,bgWidth,bgHeight);
		}
		
		
		function checkKeyDown(e){
			if(e.keyCode == 37){ //left key
				bullet.direction = 1;
				e.preventDefault();
				clearCtxGun();
				ctxGun.drawImage(imgSprite,gun.srcX - gun.width,gun.srcY,gun.width,gun.height,gun.drawX,gun.drawY,gun.width,gun.height);
			}
			if(e.keyCode == 38){ //up key
				bullet.direction = 3;
				e.preventDefault();
				clearCtxGun();
				ctxGun.drawImage(imgSprite,gun.srcX,gun.srcY,gun.width,gun.height,gun.drawX,gun.drawY,gun.width,gun.height);
			}
			if(e.keyCode == 39){ //right key
				bullet.direction = 2;
				e.preventDefault();
				clearCtxGun();
				ctxGun.drawImage(imgSprite,gun.srcX + gun.width,gun.srcY,gun.width,gun.height,gun.drawX,gun.drawY,gun.width,gun.height);
			}
			if(e.keyCode == 32 && !bullet.isShot){ // spacebar
				e.preventDefault();
				clearCtxBullet();
				bullet.isShot = true;
			}
		}
		
	</script>

</body>


</html>
