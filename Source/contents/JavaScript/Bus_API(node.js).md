
![api 서버 사용 test 1](https://user-images.githubusercontent.com/68761119/148173453-6073ad60-08fe-412e-b543-cae3a906a04c.png)


```
const express = require('express');
const app = express();
const request = require('request');
const cheerio = require('cheerio');
const moment = require('moment');
const readline = require('readline');

const rl = readline.createInterface({   //             정류장 입력받기    
  input: process.stdin,
  output: process.stdout
});

rl.on('line', function(line) {
 


//                                  정류소 ID를 모르기때문에, 정류소 이름을 한글로 입력하면 정류소ID와 매핑되어 응답할 수 있도록
var fs = require('fs'); 
var 이름 = fs.readFileSync('이름.txt', 'utf-8');
var id = fs.readFileSync('id.txt', 'utf-8');

const 이름a = 이름.split('\n'); 
const ida = id.split('\n');                                     //문자열에 /r이 남아있다.

var dicObject = {}
for( var i=0; i<이름a.length; i++){
    dicObject[이름a[i]] = ida[i];
}
//var line = "금남로5가역"
//                                                                 여기까지

require('moment-timezone');
  const url1 = 'http://api.gwangju.go.kr/xml/arriveInfo';
  const key = "비밀"; //제공받은 Key 값
  const stationId = dicObject[line+"\r"]; // 정류장 ID

  const all_url = url1 + '?serviceKey=' + key +  '&BUSSTOP_ID=' + stationId;
  
  var parseString = require('xml2js').parseString;
  const { type } = require('express/lib/response');

  setInterval(() => {                           //서버에서는 그냥 변하계속 변하는거 보려고 인터벌 넣었는데, 챗봇에서는 갱신하는거 볼필요없으니 빼도될 듯
  console.clear();

  request(all_url, function (err, res, body) {
    //var obj = JSON.parse(res.body);

    const bn = [];
    const rm = [];
    const af = [];
    const st = [];
    const de = [];

    $ = cheerio.load(body);
$('ARRIVE').each(function(idx){    
  
  let line_name  = $(this).find('LINE_NAME').text();    // console.log(`버스번호:      ${line_name}`)
  let remain_min = $(this).find('REMAIN_MIN').text();   //console.log(`남은시간: ${remain_min} m `)
  let arrive_flag = $(this).find('ARRIVE_FLAG').text(); //console.log(`곧도착:   ${arrive_flag}`)
  let DIR_START = $(this).find('DIR_START').text();
  let DIR_END = $(this).find('DIR_END').text();

  bn.push(line_name);
  rm.push(remain_min);
  af.push(arrive_flag);
  st.push(DIR_START);
  de.push(DIR_END);
 
});

// 이 부분을 어떻게 Json으로 담지..
for(var i=0; i<bn.length; i++) {
  console.log(bn[i]+'번 남은시간 : ' + rm[i]+" 분  "  + (af[i] == "1" ? af[i] = "(곧 도착)              " : af[i] = "             방향 : ") + st[i] + " --> " + de[i]); // 3항연산자, 곧도착=1, 나머지=0을 문자로전환
}
  });
//                                                                       requset 종료구간


}, 10000); //10초 간격
//                                                                       interval 끝나는 구간.

//                                                                             입력
rl.close(); //callback 종료
}).on("close", function() {
});
app.listen(3000, function() {
  console.log('Port 3000, On.');
});
//                                                                             함수
//남은 일
//Json 형태로 웹에 뿌리는 일
```