![2](https://user-images.githubusercontent.com/68761119/149260008-c4c71812-157a-4e60-8198-1e0cca14df1e.jpg)


```
const express = require('express');
const app = express();
const logger = require('morgan');
const bodyParser = require('body-parser');
const request = require('request');
const cheerio = require('cheerio');
const apiRouter = express.Router();

app.use(logger('dev', {}));
app.use(bodyParser.json());
app.use(bodyParser.urlencoded({ extended: true }));
app.use('/api', apiRouter);


apiRouter.post('/bus', function(req, res) {
var msg = req.body.action.params.stations_line1;						

const 이름 = ["녹동역","소태역","학동.증심사입구역","남광주역","문화전당역","금남로4가역","금남로5가역","양동시장역","돌고개역","농성역","화정역","쌍촌역","운천역","상무역","김대중컨벤션센터역","공항역","송정공원역","광주송정역","도산역","평동역"]
const id = ["SUB50110","SUB50111","SUB50112","SUB50113","SUB50114","SUB50115","SUB50116","SUB50117","SUB50118","SUB50119","SUB50120","SUB50121","SUB50122","SUB50123","SUB50124","SUB50125","SUB50126","SUB50127","SUB50128","SUB50129"]

								// 죄다 전역으로 선언하기
var str = ""
var ple = [];
var bn = [];
var ex = [];
var dicObject = {}
var responseBody = ""
								// 오류찾기 번거로움, Text Format 수정 시 같이 수정

var fs = require('fs');
var 광버 = fs.readFileSync('gb.txt', 'utf-8');
const 광버a = 광버.split(',');


for (var i = 0; i < 이름.length; i++) {
    dicObject[이름[i]] = id[i];
}
	
var line = "문화전당역"
require('moment-timezone');
const url1 = 'http://openapi.tago.go.kr/openapi/service/SubwayInfoService/getSubwaySttnExitAcctoBusRouteList?serviceKey= " 비밀 키 " &subwayStationId=';
const stationId = dicObject[msg]
const all_url = url1 + stationId + "&numOfRows=999";

request(all_url, function (err, res, body) { //request 구간

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
            ple.push(ex[i] + "번 출구 : " + bn[i] + "\r");

        }
    }
    str = ple.join('');
                            // 강제 비동기
    rr();
    rrr();
							// promise, async, await 안배웠습니다.
});
function rr() {
    responseBody = {
        'version': "2.0",
        'template': {
            'outputs': [
                {
                    'simpleText': {
                        'text': `${str}`
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
