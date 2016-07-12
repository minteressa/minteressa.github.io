---
position: 6
layout: default
title: Visualization
permalink: visualization.html
published: true
---
<html lang="en">
  <head>
    <title>dc.js - m'interessa</title>
    <meta charset="UTF-8">
    <link rel="stylesheet" type="text/css" href="assets/bootstrap/css/bootstrap.min.css">
    <link rel="stylesheet" type="text/css" href="assets/ds/dc.css"/>
  </head>
  <body>

<div class="container">
<!--script type="text/javascript" src="http://dc-js.github.io/dc.js/examples/header.js"></script-->
<div class="row">

    <div class="col-xs-3">
		<h3>Loss Function</h3>
       <div id="chart-ring-lossfunc" class="col-xs-3"></div>
    </div>

    <div class="col-xs-3">
		<h3>Kernel</h3>
        <div id="chart-ring-kernel" class="col-xs-3"></div>
    </div>

    <div class="col-xs-3">
        <h3>Decay</h3>
        <div id="chart-ring-decay"></div>
    </div>
	
    <div class="col-xs-3">
        <h3>Ngram</h3>
        <div id="chart-ring-ngram"></div>
    </div>

</div>

<div class="row">   
    <div class="col-xs-4">
     <h3>Skip</h3>
    <div id="chart-ring-skip"></div>
    </div>    
  
     <div class="col-xs-4">
        <h3>Learning Rate</h3>
    <div id="chart-ring-learning_rate"></div>
    </div>     	
  	
    <div class="col-xs-4">
        <h3>Pred Threshold</h3>
    <div id="chart-ring-pred_thresh"></div>
    </div>   	
  	
</div>

<div class="row">
	<div class="col-xs-4">
		<h3>Precision</h3>
		<div id="chart-PRE"></div>
	</div>
	<div class="col-xs-4">
		<h3>Recall</h3>
		<div id="chart-REC"></div>
	</div>
	<div class="col-xs-4">
		<h3>Accuracy</h3>
		<div id="chart-ACC"></div>
	</div>
  	<div class="col-xs-4">
		<h3>F-measure</h3>
		<div id="chart-PRF"></div>
	</div>
  	<div class="col-xs-4">
		<h3>ROC</h3>
		<div id="chart-ROC"></div>
	</div>
</div>

</div>
	
    <script type="text/javascript" src="assets/ds/d3.js"></script>
    <script type="text/javascript" src="assets/ds/crossfilter.js"></script>
    <script type="text/javascript" src="assets/ds/dc.js"></script>
    <script type="text/javascript">

	
var lossfuncRingChart = dc.pieChart("#chart-ring-lossfunc"),
	kernelRingChart = dc.pieChart("#chart-ring-kernel"),
    decayRingChart = dc.pieChart("#chart-ring-decay"),
    ngramRingChart = dc.pieChart("#chart-ring-ngram"),
    skipRingChart = dc.pieChart("#chart-ring-skip"),
    learning_rateRingChart = dc.pieChart("#chart-ring-learning_rate"),
    pred_threshRingChart = dc.pieChart("#chart-ring-pred_thresh"),
    PRERowChart = dc.lineChart("#chart-PRE"),
	RECRowChart = dc.lineChart("#chart-REC"),
	ACCRowChart = dc.lineChart("#chart-ACC"),
	PRFRowChart = dc.lineChart("#chart-PRF"),
	ROCRowChart = dc.lineChart("#chart-ROC")
	PRECols = 100,
	ACCCols = 100,
	RECCols = 100,
    PRFCols = 100,
	ROCCols = 100;
	

d3.csv("gridsearch-nourls-isis.csv", function(error, experiments) {
  experiments.forEach(function(x) {
    x.PRE = Math.floor( parseFloat( x.PRE ) * PRECols );
	x.ACC = Math.floor( parseFloat( x.ACC ) * ACCCols );
	x.REC = Math.floor( parseFloat( x.REC ) * RECCols );
    x.PRF = Math.floor( parseFloat( x.PRF ) * PRFCols );
	x.ROC = Math.floor( parseFloat( x.ROC ) * ROCCols );
  });
  // lossDimension = return map[d.lossfunc]
  
  // set crossfilter with first dataset
	var ndx = crossfilter(experiments),
	
	
    lossfuncDim  = ndx.dimension(function(d) {return d.lossfunc;}),
    kernelDim  = ndx.dimension(function(d) {return d.kernel;}),
	decayDim  = ndx.dimension(function(d) {return d.decay;}),
    ngramDim  = ndx.dimension(function(d) {return d.ngram;}),
    skipDim  = ndx.dimension(function(d) {return d.skip;}),
    learning_rateDim  = ndx.dimension(function(d) {return d.learning_rate;}),
    pred_threshDim  = ndx.dimension(function(d) {return d.pred_thresh;}),
    PREDim = ndx.dimension(function(d) {return d.PRE;}),
	ACCDim = ndx.dimension(function(d) {return d.ACC;}),
	RECDim = ndx.dimension(function(d) {return d.REC;}),
    PRFDim = ndx.dimension(function(d) {return d.PRF;}),
	ROCDim = ndx.dimension(function(d) {return d.ROC;});

	countPerLoss = lossfuncDim.group().reduceCount(),
	countPerKernel = kernelDim.group().reduceCount(),
    countPerDecay = decayDim.group().reduceCount(),
    countPerNgram = ngramDim.group().reduceCount(),
    countPerSkip = skipDim.group().reduceCount(),
    countPerLearning_rate = learning_rateDim.group().reduceCount(),
    countPerPred_thresh = pred_threshDim.group().reduceCount(),
    countPerPRE = PREDim.group().reduceCount(),
	countPerREC = RECDim.group().reduceCount(),
	countPerACC = ACCDim.group().reduceCount();
  	countPerROC = ROCDim.group().reduceCount(),
	countPerPRF = PRFDim.group().reduceCount();
  
function render_plots(){
    lossfuncRingChart
        .width(150).height(150)
        .dimension(lossfuncDim)
        .group(countPerLoss)
        .innerRadius(0)
		
		;
	

	kernelRingChart	
        .width(150).height(150)
        .dimension(kernelDim)
        .group(countPerKernel)
        .innerRadius(0)
		
		;	

  
    decayRingChart	
        .width(150).height(150)
        .dimension(decayDim)
        .group(countPerDecay)
        .innerRadius(0)
		
		;	

  
	ngramRingChart	
        .width(150).height(150)
        .dimension(ngramDim)
        .group(countPerNgram)
        .innerRadius(0)
		
		;	

  
	skipRingChart	
        .width(150).height(150)
        .dimension(skipDim)
        .group(countPerSkip)
        .innerRadius(0)
		
		;	

  
	learning_rateRingChart	
        .width(150).height(150)
        .dimension(learning_rateDim)
        .group(countPerKernel)
        .innerRadius(0)
		
		;	

  
	pred_threshRingChart
        .width(150).height(150)
        .dimension(pred_threshDim)
        .group(countPerPred_thresh)
        .innerRadius(0)
		
		;	


    ACCRowChart
        .width(250)
		.height(200)
		.renderArea(true)
        .dimension(ACCDim)
		.x(d3.scale.linear().domain([0, ACCCols]))
        .group(countPerACC)
		.title("Accuracy");
  
    PRERowChart
        .width(250)
		.height(200)
		.renderArea(true)
        .dimension(RECDim)
		.x(d3.scale.linear().domain([0, PRECols]))
        .group(countPerREC)
		.renderTitle(true)
		.title("Precision");

    RECRowChart
        .width(250)
		.height(200)
		.renderArea(true)
        .dimension(RECDim)
		.x(d3.scale.linear().domain([0, PRECols]))
        .group(countPerPRE)
		.title("Recall");
			
    PRFRowChart
        .width(250)
		.height(200)
		.renderArea(true)
        .dimension(PRFDim)
		.x(d3.scale.linear().domain([0, PRFCols]))
        .group(countPerPRF)
		.renderTitle(true)
		.title("F-measure");

    ROCRowChart
        .width(250)
		.height(200)
		.renderArea(true)
        .dimension(ROCDim)
		.x(d3.scale.linear().domain([0, ROCCols]))
        .group(countPerROC)
		.title("ROC");
		
    dc.renderAll();
}
render_plots();

});




    </script>

</div>
  </body>
</html>
