<script>
var canvas = document.createElement("canvas");
var ctx    = canvas.getContext('2d');

canvas.width  = 180;
canvas.height = 100;

document.body.insertBefore(canvas, document.body.firstElementChild);

 
function draw() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);
  
  var sizeX = 32;
  var sizeY = 32;
  var sizeZ = 8; 
   
  ctx.scale(2, 2);
 
  drawCube(50, 50, sizeX, sizeY, sizeZ);
}

requestAnimationFrame(draw);


function drawCube(x, y, wx, wy, h, color) {

    // LINE MODE
    ctx.lineJoin = "round";
    
    // left face
    ctx.beginPath();
    ctx.moveTo(x, y);
    ctx.lineTo(x - wx, y - wx * 0.5);
    ctx.lineTo(x - wx, y - h - wx * 0.5);
    ctx.lineTo(x, y - h * 1);
    ctx.closePath();
    ctx.fillStyle = "#bdbebd"
    ctx.strokeStyle = "#545454";
    ctx.stroke();
    ctx.fill();

    // right face
    ctx.beginPath();
    ctx.moveTo(x, y);
    ctx.lineTo(x + wy, y - wy * 0.5);
    ctx.lineTo(x + wy, y - h - wy * 0.5);
    ctx.lineTo(x, y - h * 1);
    ctx.closePath();
    ctx.fillStyle = "#a9a9a9";
    ctx.strokeStyle = "#545454";
    ctx.stroke();
    ctx.fill();

    // center face
    ctx.beginPath();
    ctx.moveTo(x, y - h);
    ctx.lineTo(x - wx, y - h - wx * 0.5);
    ctx.lineTo(x - wx + wy, y - h - (wx * 0.5 + wy * 0.5));
    ctx.lineTo(x + wy, y - h - wy * 0.5);
    ctx.closePath();
    ctx.fillStyle = "#d3d3d3";
    ctx.strokeStyle = "#989898";
    ctx.stroke();
    ctx.fill();
}
</script>