## Concurrently
(여러개의 commands를 동시에 작동 시킬수 있게 해주는 Tool)   
-> 프론트, 백 서버 한번에 켜기   

### 방법
루트 디렉토리에서
```
npm install concurrently - -save
```

package.json의 start 부분에 추가한다.    

`"start": "concurrently \"command1 arg\" \"command2 arg\""`