<img src="https://user-images.githubusercontent.com/68761119/148173049-4a9da802-d9e3-4a6a-83da-f1bdd8036d29.png" width="250" height="400"/>


```
const express = require('express');
const app = express();
const logger = require('morgan');
const bodyParser = require('body-parser');
const request = require('request');
const apiRouter = express.Router();

app.use(logger('dev', {}));
app.use(bodyParser.json());
app.use(bodyParser.urlencoded({ extended: true }));

app.use('/api', apiRouter);


apiRouter.post('/sayHello', function(request, response) {
	var msg = request.body.action.params.yeah;						//utterance보다 이게 낫겟다. 이건 챗봇측에서 엔티티만 만들면 되니까..
	console.log(msg); 
	//console.log(msg === "여보세요 나야");
	//console.log(req.body);
	var send = {};
	
	switch(msg) {
		case '여보세요 나야':
			send = {
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
 }
			break;
	
		case '거기 잘 지내니':
			send = {
			version: "2.0",
    		template: {
    		outputs: [
					{
        	simpleText: { 
			text: "못 지낸다. " 
		   }
        }
      ]
    }
  }
			break;
}    

	response.status(200).send(send);
	});

// 우선 채팅입력을 3초간 텀을주고하면 잘 알아먹는다.
// 엔티티를 설정해서 비슷한 발화가 하나의 대표 엔티티로 가게 만든다음 그걸 파라미터로 설정하면 utterance보다 정확하다. 아니 이게 맞다. utterance는 if("여보세요 나야) 인데 "여보세요" 라고 하면 못알아먹으니까..

//이제 여기서 api를 써 볼까?

app.listen(3000, function() {
  console.log('Port 3000에서 돌아간다.');
});


```