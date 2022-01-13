![3](https://user-images.githubusercontent.com/68761119/149259550-144fef81-28c3-43c8-a3bc-a10e095c4538.jpg)

```
const express = require('express');  
const app = express();  
const request = require('request');  
const cheerio = require('cheerio');  
const moment = require('moment');  


// 광주버스만 취급하기 위함 (나주,장성 X)
var fs = require('fs'); 
var 광버 = fs.readFileSync('광주버스.txt', 'utf-8');
const 광버a = 광버.split(',');

/*  배열 선언해서 편하게 사용하기 위함
var 이름 = fs.readFileSync('역이름.txt', 'utf-8');
var id = fs.readFileSync('역ID.txt', 'utf-8');
const 이름a = 이름.split('\n');
const ida = id.split('\n');
*/


const 이름a = ["녹동역","소태역","학동.증심사입구역","남광주역","문화전당역","금남로4가역","금남로5가역","양동시장역","돌고개역","농성역","화정역","쌍촌역","운천역","상무역","김대중컨벤션센터역","공항역","송정공원역","광주송정역","도산역","평동역"]
const ida = ["SUB50110","SUB50111","SUB50112","SUB50113","SUB50114","SUB50115","SUB50116","SUB50117","SUB50118","SUB50119","SUB50120","SUB50121","SUB50122","SUB50123","SUB50124","SUB50125","SUB50126","SUB50127","SUB50128","SUB50129"]

var dicObject = {}
for( var i=0; i<이름a.length; i++){
    dicObject[이름a[i]] = ida[i]; 
}
                                            

var line = "문화전당역"
require('moment-timezone');
  const url1 = 'http://openapi.tago.go.kr/openapi/service/SubwayInfoService/getSubwaySttnExitAcctoBusRouteList?serviceKey= " 비밀 키 "&subwayStationId=';
  const stationId = dicObject[line]
  const all_url = url1 + stationId + "&numOfRows=999";



var parseString = require('xml2js').parseString;
const {type} = require('express/lib/response');
const {all} = require('express/lib/application');

request(all_url, function (err, res, body) {

    const bn = [];
    const ex = [];

    $ = cheerio.load(body);
    $('item').each(function (idx) {

        let busRouteNo = $(this)
            .find('busRouteNo')
            .text();
        let exitNo = $(this)
            .find('exitNo')
            .text();

        bn.push(busRouteNo);
        ex.push(exitNo);

    });
    for (var i = 0; i < bn.length; i++) {
        if (광버a.includes(bn[i])) {
            console.log(ex[i] + "번 출구 : " + bn[i]);
        }
    }
});

app.listen(3000, function () {
    console.log('Port 3000, On.');
});
```