
![api 서버 사용 test 1](https://user-images.githubusercontent.com/68761119/148173453-6073ad60-08fe-412e-b543-cae3a906a04c.png)


```
const express = require('express');
const app = express();
const request = require('request');
const cheerio = require('cheerio');
const moment = require('moment');


  

require('moment-timezone');
  const url1 = 'http://api.gwangju.go.kr/xml/arriveInfo';
  const key = "비밀이다."; //제공받은 Key 값
  const stationId = "1017"; // 정류장 ID

  const all_url = url1 + '?serviceKey=' + key +  '&BUSSTOP_ID=' + stationId;
  
  var parseString = require('xml2js').parseString;
  const { type } = require('express/lib/response');

  setInterval(() => {
  console.clear();

  request(all_url, function (err, res, body) {
    //var obj = JSON.parse(res.body);

    const bn = [];
    const rm = [];
    const af = []
    
    $ = cheerio.load(body);
$('ARRIVE').each(function(idx){    
  
  let line_name  = $(this).find('LINE_NAME').text();    // console.log(`버스번호:      ${line_name}`)
  let remain_min = $(this).find('REMAIN_MIN').text();   //console.log(`남은시간: ${remain_min} m `)
  let arrive_flag = $(this).find('ARRIVE_FLAG').text(); //console.log(`곧도착:   ${arrive_flag}`)
  
  bn.push(line_name);
  rm.push(remain_min);
  af.push(arrive_flag);
 
});

for(var i=0; i<bn.length; i++) {
  console.log(bn[i]+'번 남은시간 : ' + rm[i]+" 분  "  + (af[i] == "1" ? af[i] = "(곧 도착)" : af[i] = "")); // 3항연산자, 곧도착=1, 나머지=0을 문자로전환
}
  });
//requset 종료구간

}, 10000); //10초 간격
//interval 끝나는 구간.

app.listen(3000, function() {
  console.log('Port 3000, On.');
});



//남은 일
//Json 형태로 웹에 뿌리는 일
```