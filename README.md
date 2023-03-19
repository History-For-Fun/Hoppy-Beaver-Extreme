var Beaver = function(x, y) {
    this.x = x;
    this.y = y;
    this.img = getImage("avatars/robot_female_1");
    this.sticks = 0;
};

Beaver.prototype.draw = function() {
    fill(252, 252, 252);
    this.y = constrain(this.y, 0, height-50);
    image(this.img, this.x, this.y, 40, 40);
};

Beaver.prototype.hop = function() {
    this.img = getImage("avatars/robot_female_2");
    this.y -= 5;
};

Beaver.prototype.fall = function() {
    this.img = getImage("avatars/robot_female_2");
    this.y += 5;
};

Beaver.prototype.checkForStickGrab = function(stick) {
    if ((stick.x >= this.x && stick.x <= (this.x + 47)) &&
        (stick.y >= this.y && stick.y <= (this.y + 50))) {
        stick.y = 10000000000000000;
        this.sticks++;
    }
};

var Stick = function(x, y) {
    this.x = x;
    this.y = y;
};

Stick.prototype.draw = function() {
    fill(72, 255, 0);
    rectMode(CENTER);
    rect(this.x, this.y, 5, 40);
};

var beaver = new Beaver(108, 300);

var sticks = [];
for (var i = 0; i < 40; i++) {  
    sticks.push(new Stick(i * 40 + 300, random(20, 260)));
}

var grassXs = [];
for (var i = 0; i < 25; i++) { 
    grassXs.push(i*20);
}

draw = function() {
    
    // static
    background(227, 254, 255);
    fill(130, 79, 43);
    rectMode(CORNER);
    rect(0, height*0.90, width, height*0.10);
    
   
    for (var i = 0; i < grassXs.length; i++) {
        image(getImage("cute/StoneBlockTall"), grassXs[i], height*0.77, 42, 83);
        grassXs[i] -= 1;
        if (grassXs[i] <= -20) {
            grassXs[i] = width;
        }
    }
     for (var i = 0; i < grassXs.length; i++) {
        image(getImage("cute/CharacterHornGirl"), grassXs[i], height*0.63, 42, 83);
        grassXs[i] -= 1;
        if (grassXs[i] <= -20) {
            grassXs[i] = width;
        }
    }
     for (var i = 0; i < grassXs.length; i++) {
        image(getImage("cute/CharacterHornGirl" ), grassXs[i], height*0.69, 42, 83);
        grassXs[i] -= 1;
        if (grassXs[i] <= -20) {
            grassXs[i] = width;
        }
    }
     
    for (var i = 0; i < sticks.length; i++) {
        sticks[i].draw();
        beaver.checkForStickGrab(sticks[i]);
        sticks[i].x -= 1;
    }
     for (var i = 0; i < grassXs.length; i++) {
        image(getImage("cute/StoneBlock"), grassXs[i], height*0.90, 42, 83);
        grassXs[i] -= 1;
        if (grassXs[i] <= -20) {
            grassXs[i] = width;
        }
    }
    for (var i = 0; i < grassXs.length; i++) {
        image(getImage("cute/CharacterHornGirl"), grassXs[i], height*0.83, 42, 83);
        grassXs[i] -= 1;
        if (grassXs[i] <= -20) {
            grassXs[i] = width;
        }
    }
    textSize(18);
    text("Score: " + beaver.sticks, 20, 30);
    
    if (beaver.sticks/sticks.length >= 0.95) {
        textSize(36);
        text("你是小偷 ", 100, 200);
        text("我要报警 ", 100, 296);
    }
    
    if (keyIsPressed && keyCode === 0) {
        beaver.hop();
    } else {
        beaver.fall();
    }
    beaver.draw();
};

