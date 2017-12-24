	$(document).ready(function(){
	$('#test').click(function(){
		$("div").text('Changing test')
		.removeClass('pclass')
		.css("background-color","red")
		.animate({width:"200px",height:"30px"}, 2000);
	  });
	$('#test').mouseover(function(){
	var $myelement = $("div");
		$myelement.text('Original Text');
		$myelement.addClass('pclass');
		$myelement.css("background-color","blue");
		
		$myelement.animate({width:"200px",height:"60px"}, 2000);
	  });
	  
	  $('#drwchrt').click(drawchart);
		$('#drwRectchrt').click(rectChart);
	});
	$("a[href='#top']").click(function() {  
  $("table").animate({width:"200px",height:"60px"}, 2000);  
}); 
$(document).ready(function(){  
    $("tr:odd").addClass("zebra");  
});	


    function Remove_options()  
    {  
    $('#myColor')  
        .empty()  
        .append('<option selected="selected" value="test">White</option>');  
    }  
    
    $(document).ready(function(){   
  $("a[href='#trow']").click(function(){   
    $("#mytable").find("tr:nth-child(2n)").toggle();  
  });  
  
  $('#btn-getjson').click(function(){
	      $.getJSON("test.json", function(result){
        $.each(result, function(i, field){
            $("table tr:last-child").after("<tr><td>" + i + "</td><td>" + field + "</td></tr>");
        });
    });
    
  });
  $('#showtable').click(function(){
	  $("table").slideToggle(2000);
  });
});

function drawLine(ctx, startX, startY, endX, endY){
    ctx.beginPath();
    ctx.moveTo(startX,startY);
    ctx.lineTo(endX,endY);
    ctx.stroke();
}

function drawArc(ctx, centerX, centerY, radius, startAngle, endAngle){
    ctx.beginPath();
    ctx.arc(centerX, centerY, radius, startAngle, endAngle);
    ctx.stroke();
}

function drawPieSlice(ctx,centerX, centerY, radius, startAngle, endAngle, color ){
    ctx.fillStyle = color;
    ctx.beginPath();
    ctx.moveTo(centerX,centerY);
    ctx.arc(centerX, centerY, radius, startAngle, endAngle);
    ctx.closePath();
    ctx.fill();
}
  
var Piechart = function(options){
    this.options = options;
    this.canvas = options.canvas;
    this.ctx = this.canvas.getContext("2d");
    this.colors = options.colors;
 
    this.draw = function(){
        var total_value = 0;
        var color_index = 0;
        for (var categ in this.options.data){
            var val = this.options.data[categ];
            total_value += val;
        }
 
        var start_angle = 0;
        for (categ in this.options.data){
            val = this.options.data[categ];
            var slice_angle = 2 * Math.PI * val / total_value;
 
            drawPieSlice(
                this.ctx,
                this.canvas.width/2,
                this.canvas.height/2,
                Math.min(this.canvas.width/2,this.canvas.height/2),
                start_angle,
                start_angle+slice_angle,
                this.colors[color_index%this.colors.length]
            );
 
            start_angle += slice_angle;
            color_index++;
        }
 
    }
}   



 function drawchart(){
	var mycanvas = document.getElementById("chartarea");
	mycanvas.width = 400;
	mycanvas.height = 400;
	
	var ctx = mycanvas.getContext("2d");
 	var myVinyls = getJson('test.json');
//var myVinyls;

console.log(myVinyls);

//$.getJSON("test.json",function(data){
//myVinyls = data;
//console.log(myVinyls);
//});

	var colors = ["#1235aa","#ddaa45","#448845","#92ff45","#aaff45","#448845"];

var total_value = 0;
for(category in myVinyls){
var val = myVinyls[category];
total_value += val;
}
var color_index = 0;
var st_angle = 0;
for(category in myVinyls){
val = myVinyls[category];
var slice_angle = val/total_value * 2 * 22 / 7;

drawPieSlice(
                ctx,
                mycanvas.width/2,
                mycanvas.height/2,
                mycanvas.width/2,
                st_angle,
                st_angle + slice_angle,
                colors[color_index%colors.length]
            );
st_angle += slice_angle;
color_index++;
}

 }
 
	
function getJson(url) {
 return JSON.parse($.ajax({
     type: 'GET',
     url: url,
     dataType: 'json',
     global: false,
     async:false,
     success: function(data) {
         return data;
     }
 }).responseText);
}

function rectChart(){
var mycanvas = document.getElementById("chartarea");
var myData = getJson('test.json');
var width = mycanvas.width;
var height = mycanvas.height;
var ctx = mycanvas.getContext("2d");
ctx.clearRect(0, 0, width, height);
var colors = ["#1235aa","#ddaa45","#448845","#92ff45","#aaff45","#448845"];
var max = 0;
var count = 0;
for(category in myData){
		if(max < myData[category])
			max = myData[category];
			count++;
	}
	console.log(myData);
var color_index = 0;
var scale_factor = (height - 5)/max;
console.log("scalefactor " + scale_factor);
var start_x = 0;
var gap = width/(2*count+1);
var start_y = 0;
	for(category in myData){
		start_y = myData[category]*scale_factor;
		drawRectangale(ctx,
		start_x + gap,
		height-start_y,
		gap,
		start_y,
		colors[color_index%colors.length]);
		color_index++;
		start_x += 2*gap;
	}
}

function drawRectangale(ctx, startx, starty, width, height, color){
	ctx.fillStyle = color;
	ctx.fillRect(startx, starty, width, height);
	ctx.fill();
}