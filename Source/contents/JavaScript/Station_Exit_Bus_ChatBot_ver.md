![ㅌㅌㅌ](https://user-images.githubusercontent.com/68761119/153342798-7aaa8b9d-edde-4f0a-b2ce-e3c05ef6ce0f.png)

```
const express = require('express');
const app = express();
const logger = require('morgan');
const bodyParser = require('body-parser');
const request = require('request');
const cheerio = require('cheerio');
const moment = require('moment');
const readline = require('readline');
const apiRouter = express.Router();

app.use(logger('dev', {}));
app.use(bodyParser.json());
app.use(bodyParser.urlencoded({ extended: true }));
app.use('/api', apiRouter);


apiRouter.post('/bus', function(req, res) {
var msg = req.body.action.params.stations_line1 +" "+ req.body.action.params.exit; //파라미터 2개 받기

var str = ""
var ple = [];
var responseBody = ""
	
								
var fs = require('fs'); 
var 이름 = fs.readFileSync('in.txt', 'utf-8');
var id = fs.readFileSync('out.txt','utf-8');
var sta = fs.readFileSync('station.txt','utf-8');
var url = fs.readFileSync('url.txt','utf-8');
	
const 이름a = 이름.split('\n'); 
const ida = id.split('\n');                                     //문자열에 /r이 남아있다.
const staa = sta.split('\n');
const urla = url.split('\n');	
	
var dicObject = {}
for( var i=0; i<이름a.length; i++){
    dicObject[이름a[i]] = ida[i];
}
	
var dicObject1 = {}
for( var i=0; i<ida.length; i++){
    dicObject1[ida[i]] = staa[i];
}
	
var dicObject2 = {}
for( var i=0; i<ida.length; i++){
    dicObject2[이름a[i]] = urla[i];
}

//var line = "상무역 2번 출구";
require('moment-timezone');
const url1 = 'http://api.gwangju.go.kr/xml/arriveInfo';
const key = "wow"; //제공받은 Key 값
const stationId = dicObject[msg]; // 정류장 ID
const all_url = url1 + '?serviceKey=' + key +  '&BUSSTOP_ID=' + stationId;	
	
var title = dicObject1[stationId];	
var returnurl = dicObject2[msg];
	
request(all_url, function (err, res, body) {
var bn = [];
var rm = [];
var af = [];
    $ = cheerio.load(body);
$('ARRIVE').each(function(idx){    
  
  const line_name  = $(this).find('LINE_NAME').text();    
  const remain_min = $(this).find('REMAIN_MIN').text();   
  const arrive_flag = $(this).find('ARRIVE_FLAG').text(); 
	
  bn.push(line_name);
  rm.push(remain_min);
  af.push(arrive_flag);
    
});	
	for (var i = 0; i < bn.length; i++) {
            ple.push(bn[i] + '번 : ' + rm[i] + "분"+ (af[i] == "1"? af[i] = " (곧 도착)": af[i] = "") +"\n");
    }
	
    str = ple.join('');					
	if(str == ""){
	   str = "도착 정보가 없습니다.";
	   }
	
    rr();					// 강제 동기
    rrr();
							// promise, async, await 대신
});
function rr() {
    responseBody = {
        'version': "2.0",
        template: { //카드형식
            outputs: [
                {
					"basicCard": {
         				 "title": `${title}`,
          				 "description": `${str}`,
          				 "thumbnail": {
            				"imageUrl": `${returnurl}`
         		 }
                }
				}
            ]
        }
    }
}
function rrr() {
    res
        .status(200)
        .send(responseBody);
}
});

app.listen(3000, function () {
console.log('Port 3000에서 돌아간다.');
});


```