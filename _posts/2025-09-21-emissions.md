---
layout: post
title: SCALE Emissions
date: 2025-09-21 13:37:00
description: SCALE Emissions
tags: scale liquidity
categories: sample-posts sample-posts-2
---

gmgm




	<div>
		<div class="echarts">
        	<div id="echart-1" class="echart" style="height:70vh"></div>
        	<div id="echart-2" class="echart" style="height:70vh"></div>
        	<div id="echart-3" class="echart" style="height:70vh"></div>
        </div>

			<script src="https://ftm.guru/ethers-5.2.umd.min.js" type="application/javascript"></script>
		    <script src="https://cdn.jsdelivr.net/npm/echarts@5.5.1/dist/echarts.min.js"></script>
		    <script>

eo0 = {
  toolbox: {
    feature: {
      dataView: { show: true, readOnly: false },
      magicType: { show: true, type: ['line', 'bar'] },
      restore: { show: true },
      saveAsImage: { show: true },
    },
  },
  tooltip: {
    trigger: 'axis',
    axisPointer: {
      type: 'cross',
      label: {
        backgroundColor: '#6a7985'
      }
    }
  },
  legend: { type: 'scroll' , top: 30},
  xAxis: {type:'time'},
  yAxis: [{type:'value'},{type:'value'}],
}

async function main() {
/*
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
// old emi chart
elapsedIndex= 2
rd = (new Array(6)).fill(0);
rd = rd.map((e,i)=>1758153600e3 + 7*86400e3*i)
// time, elapsed, upcoming, usd elapsed, usd potential
rd = rd.map((e,i)=>([e, (i<elapsedIndex?200:0), (i<elapsedIndex?0:200), (i<elapsedIndex ? 200*0.05*(1+(Math.random()-0.5)/2	) : 0)]))
rd = rd.map((e,i,a)=>[...e, (i>=elapsedIndex?a[elapsedIndex-1][3]:0)]) // usd potential


eo_tvl_the = {
  ...eo0 ,
  title: {left: 'center', top: 10, text: "Reward Rates: History & Projection"},
  series: [
    {
      name: 'SCALE per Day (elapsed)',
      type: 'bar',
      smooth: true,
      emphasis: { focus: 'series' },
      data: rd.map(i=>([i[0],i[1]])),
      stack: "in SCALE",
      itemStyle:{color:'#fddd60',opacity:1}
    },
    {
      name: 'USD per Day (elapsed)',
      type: 'bar',
      smooth: true,
      emphasis: { focus: 'series' },
      data: rd.map(i=>([i[0],i[3]])),
      stack: "in USD",
      yAxisIndex: 1,
      itemStyle:{color:'#4992ff',opacity:1}
    },
    {
      name: 'SCALE per Day (assured)',
      type: 'bar',
      smooth: true,
      emphasis: { focus: 'series' },
      data: rd.map(i=>([i[0],i[2]])),
      stack: "in SCALE",
      itemStyle:{color:'#fddd60',opacity:1}
    },
    {
      name: 'USD per Day (potential)',
      type: 'bar',
      smooth: true,
      emphasis: { focus: 'series' },
      data: rd.map(i=>([i[0],i[4]])),
      stack: "in USD",
      yAxisIndex: 1,
      itemStyle:{color:'#4992ff',opacity:0.5}
    },
  ]
}
echart1 = echarts.init(document.getElementById('echart-1'),'dark'); echart1.setOption(eo_tvl_the);
*/


////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
/*
	// scale revenues
	dl_fees = (await (await fetch("https://api.llama.fi/summary/fees/scale?dataType=dailyFees")).json()).totalDataChart;
	console.log(dl_fees);
	dl_revn = (await (await fetch("https://api.llama.fi/summary/fees/scale?dataType=dailyRevenue")).json()).totalDataChart;
	dl_brib = (await (await fetch("https://api.llama.fi/summary/fees/scale?dataType=dailyBribesRevenue")).json()).totalDataChart;

	eo_frb = {
  		...eo0 ,
  		title: {left: 'center', top: 10, text: "Historical Fees, Revenue, Bribes"},
  		series: [
    		{
      			name: 'Fees from Classic pools',
      			type: 'bar',
      			//smooth: true,
      			emphasis: { focus: 'series' },
      			data: dl_fees.map(i=>( [i[0]*1e3 , i[1]] )),
    		},
    		{
      			name: 'Revenue from Classic pools',
      			type: 'bar',
      			//smooth: true,
      			emphasis: { focus: 'series' },
      			data: dl_revn.map(i=>( [i[0]*1e3 , i[1]] )),
      			stack: 'All Revenue',
    		},
    		{
      			name: 'Revenue from non-Classic Pools & all Bribes',
      			type: 'bar',
      			//smooth: true,
      			emphasis: { focus: 'series' },
      			data: dl_brib.map(i=>( [i[0]*1e3 , i[1]] )),
      			stack: 'All Revenue',
    		},
    		{
      			name: 'All Revenue',
      			type: 'line',
      			//smooth: true,
      			emphasis: { focus: 'series' },
      			data: dl_brib.map(i=>( [i[0]*1e3 , i[1]] )),
      			//stack: 'All Revenue',
    		},
  		],
  		dataZoom: [
    		{
      			type: 'slider',
      			show: true,
      			xAxisIndex: [0],
      			start: Math.max(dl_fees.length, dl_revn.length, dl_brib.length) - 15 ,
      			end: Math.max(dl_fees.length, dl_revn.length, dl_brib.length)
    		},
    		{
      			type: 'inside',
      			xAxisIndex: [0],
    		},
    		{
      			type: 'inside',
      			yAxisIndex: [0],
    		}
  		],
  		legend: {
    		...eo0.legend,
    		show:true,
    		selected:{
      			'Fees from Classic pools': false,
      			'Revenue from Classic pools',
      			'Revenue from non-Classic Pools & all Bribes',
    		}
  		}
	}

	echart1 = echarts.init(document.getElementById('echart-1'),'dark'); echart1.setOption(eo_frb);
*/
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
// emissions chart
	ehd = (
		await (
			(new ethers.Contract(
				"0x73E01Ae0F263ac26F40558c51Cb57137944b3937",
				["function fullEmissionsHistory() external view returns(uint[5][] memory)"],
				(new ethers.providers.JsonRpcProvider("https://mainnet.base.org"))
			))
			.fullEmissionsHistory()
		)
	)
	.map( (i,iid) => [
		Number(i[0]), //id	0
		Number(i[1])*1e3, //ts	1
		Number(i[2])/1e18, //m	2
		Number(i[3])/1e18, //d	3
		Number(i[4])/1e18, //p	4
		Number(i[3])/1e18 * 0.02, //team	5
		Number(i[3])/1e18 * 0.01, //pool2	6
		Number(i[3])*1.03/1e18 - Number(i[2])/1e18, //recylced	7
		Number(i[2])/1e18 * Number(i[4])/1e18, //usd_m	8
		Number(i[3])/1e18 * Number(i[4])/1e18, //usd_d	9
		Number(i[3])/1e18 * 0.02 * Number(i[4])/1e18, //usd_team	10
		Number(i[3])/1e18 * 0.01 * Number(i[4])/1e18, //usd_pool2	11
		( Number(i[3])*1.03/1e18 - Number(i[2])/1e18 ) * Number(i[4])/1e18, //usd_recylced	12
		0, //totalSupply = totalMinted	13
		0, //usd_totalMinted	14
		0, //FDV = totalSupply x price	15
		0, //recycled	16
		0, //usd_recycled	17
	] )
	.map( e => { // manually adjust team emission changes (should fall into bpg ideally, as these extra were lp bribed to farmers to compensate reverese rebase)
		if(e[1]==1695859200*1e3) { // ep 0 - GENESIS
			// all zeros by default
			e[2] = 10e6; // genesis mint
			//3.6m airdrop, 4.9m eco nft, 0.5m treasury, 1m liquidity @ $0.019 @ $1641/ETH @ 11.614 ETH + 1m SCALE
			e[3] = 3.6e6; //dist = airdrop
			e[4] = 0.019; //price
			e[5] = 4.9e6+ 0.5e6;//team
			e[6] = 1e6;//pool2
			e[7] = 0;//recylced
			e[8] = e[2] * e[4];//usd_mints
			e[9] = e[3] * e[4];//usd_dists
			e[10] = e[5]* e[4];//usd_team
			e[11] = e[6]* e[4];//usd_pool2
			e[12] = e[7]* e[4];//usd_recycled
		}
		if(e[1]==1703116800*1e3) { // ep 12
			e[5] = e[3] * 0.543; //team
			e[10] = e[9] * 0.543; //usd_team
			e[7] = e[3]+e[5]+e[6] - e[2] //recycled
			e[12] = e[9]+e[10]+e[11] - e[8] //usd_recycled
		}
		if(e[1]==1703721600*1e3) { // ep 12
			e[5] = e[3] * 0.115; //team
			e[10] = e[9] * 0.115; //usd_team
			e[7] = e[3]+e[5]+e[6] - e[2] //recycled
			e[12] = e[9]+e[10]+e[11] - e[8] //usd_recycled
		}
		return e;
	});
	ehd.reverse();
	ehd = ehd.map( (e,i,a) => {
		e[13] = ( i == 0 ? e[2] : e[2] + a[i-1][13] );	//totalSupply = totalMinted	13
		e[14] = ( i == 0 ? e[8] : e[8] + a[i-1][14] );	//usd_totalMinted	14
		e[15] = ( e[13] * e[2] ); //FDV = totalSupply x price	15
		e[16] = ( i == 0 ? e[7] : e[7] + a[i-1][16] );	//recycled	16
		e[17] = ( i == 0 ? e[12] : e[12] + a[i-1][17] );	//usd_recycled	17
		return e;
	})
	//.map( j =>
	// 	j.map( (e,i) => {
	//		if(i>1&&i!=4) { return e.toFixed(); }
	//		else { return e; }
	//	})
	//);



	eo_eh = {
  		...eo0 ,
  		title: {left: 'center', top: 10, text: "Historical Emissions (in Tokens)"},
  		series: [
    		{
      			name: 'Freshly Minted',
      			type: 'bar',
      			stack: 'Distributions',
      			emphasis: { focus: 'series' },
      			data: ehd.map(i=>( [i[1] , i[2].toFixed()] )),
    		},
    		{
      			name: 'Recycled',
      			type: 'bar',
      			stack: 'Distributions',
      			emphasis: { focus: 'series' },
      			data: ehd.map(i=>( [i[1] , i[7].toFixed()] )),
    		},
    		{
      			name: 'To Team',
      			type: 'bar',
      			stack: 'Distributions',
      			emphasis: { focus: 'series' },
      			data: ehd.map(i=>( [i[1] , i[5].toFixed()] )),
    		},
    		{
      			name: 'For Pool2',
      			type: 'bar',
      			stack: 'Distributions',
      			emphasis: { focus: 'series' },
      			data: ehd.map(i=>( [i[1] , i[6].toFixed()] )),
    		},
    		{
      			name: 'Total Supply',
      			type: 'line',
      			yAxisIndex: 1,
      			stack: 'Supplies',
      			emphasis: { focus: 'series' },
      			data: ehd.map(i=>( [i[1] , i[13].toFixed()] )),
    		},
    		{
      			name: 'Total Recycled',
      			type: 'line',
      			yAxisIndex: 1,
      			stack: 'Supplies',
      			emphasis: { focus: 'series' },
      			data: ehd.map(i=>( [i[1] , i[16].toFixed()] )),
    		},
    		{
      			name: 'Total Distributions',
      			type: 'scatter',
      			yAxisIndex: 1,
      			emphasis: { focus: 'series' },
      			data: ehd.map(i=>( [i[1] , (i[13]+i[16]).toFixed() ] )),
    		},
  		],
  		dataZoom: [
    		{
      			type: 'slider',
      			show: true,
      			xAxisIndex: [0],
      			start: ehd.length - 10,
      			end: ehd.length
    		},
    		{
      			type: 'inside',
      			xAxisIndex: [0],
    		},
  		],
  		legend: {
    		...eo0.legend,
    		show:true,
  		}
	}
	echart1 = echarts.init(document.getElementById('echart-1'),'dark'); echart1.setOption(eo_eh);




	eo_ehu = {
  		...eo0 ,
  		title: {left: 'center', top: 10, text: "Historical Emissions (in USD)"},
  		series: [
    		{
      			name: 'Freshly Minted',
      			type: 'bar',
      			stack: 'Total Distribution',
      			emphasis: { focus: 'series' },
      			data: ehd.map(i=>( [i[1] , i[8].toFixed()] )),
    		},
    		{
      			name: 'Recycled',
      			type: 'bar',
      			stack: 'Total Distribution',
      			emphasis: { focus: 'series' },
      			data: ehd.map(i=>( [i[1] , i[12].toFixed()] )),
    		},
    		{
      			name: 'To Team',
      			type: 'bar',
      			stack: 'Total Distribution',
      			emphasis: { focus: 'series' },
      			data: ehd.map(i=>( [i[1] , i[10].toFixed()] )),
    		},
    		{
      			name: 'For Pool2',
      			type: 'bar',
      			stack: 'Total Distribution',
      			emphasis: { focus: 'series' },
      			data: ehd.map(i=>( [i[1] , i[11].toFixed()] )),
    		},
  		],
  		dataZoom: [
    		{
      			type: 'slider',
      			show: true,
      			xAxisIndex: [0],
      			start: ehd.length - 10,
      			end: ehd.length
    		},
    		{
      			type: 'inside',
      			xAxisIndex: [0],
    		},
  		],
  		legend: {
    		...eo0.legend,
    		show:true,
  		}
	}



	echart2 = echarts.init(document.getElementById('echart-2'),'dark'); echart2.setOption(eo_ehu);

}

main()
</script>

</div>