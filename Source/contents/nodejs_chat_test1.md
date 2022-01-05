<img src="https://user-images.githubusercontent.com/68761119/148173049-4a9da802-d9e3-4a6a-83da-f1bdd8036d29.png" width="250" height="400"/>

```
const express = require('express');
const app = express();
const logger = require('morgan');
const bodyParser = require('body-parser');
const apiRouter = express.Router();

app.use(logger('dev', {}));
app.use(bodyParser.json());
app.use(bodyParser.urlencoded({
  extended: false
}));

app.use('/api', apiRouter);

apiRouter.post('/sayHello', function(req, res) {
	var msg = req.body.userRequest.utterance;
	//console.log("입력 메시지 : " + msg); 
	//console.log(msg === "여보세요 나야");
	
	if (msg === "여보세요 나야"){	
	                                   // if문 돌렸을때 오류가 생길 때, 주석 풀어서 실행 후 다시 if문 돌리면 되더라
	var responseBody = {
    version: "2.0",
    template: {
    outputs: [
		{
        simpleImage: {
            imageUrl: "https://image.xportsnews.com/contents/images/upload/article/2021/0625/mb_1624603605696988.jpg",
            altText: "hello I'm Ryan"
          }
        }
      ]
    }
  };
	}
	else{
	var responseBody = {
    version: "2.0",
    template: {
    outputs: [
		{
        simpleText: { text: "못 지낸다. " }
        }
      ]
    }
  };
}
	res.status(200).send(responseBody);
	});


// msg = req.body.userRequest.utterance로 비교하는건 그만해야 할 지도 모르겠다.
// True였다가 False였다가 자기 맘대로다.
// 다들 req.body["content"] 하던데 안되는 이유는 뭘ㄲ
// https://github.com/KeonHeeLee/Kakao-chatbot-example 얘는 그렇게 하던데.

app.listen(3000, function() {
  console.log('Port 3000에서 돌아간다.');
});

```