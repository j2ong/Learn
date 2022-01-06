![1](https://user-images.githubusercontent.com/68761119/148337711-9b1f70d4-9114-4498-89ab-b204fa69d011.png)



```
tree = elemTree.parse('데이터\광주광역시_버스정류장.xml') 
//http://api.gwangju.go.kr/xml/stationInf
root = tree.getroot()

a = [] # 아이디 -> 값 넣을 곳
b = [] # 이름 -> 키 넣을 곳

for root_e in root.iter('BUSSTOP_ID'):
    a.append(root_e.text)

for root_e in root.iter('BUSSTOP_NAME'):
    b.append(root_e.text)

df = pd.DataFrame(data = list(zip(b)), columns = ['이름'])
df = df.set_index("이름")

df2 = pd.DataFrame(data = list(zip(a)), columns = ['id'])
df2 = df2.set_index("id")

df.to_csv('이름.txt',encoding='euc-kr')
df2.to_csv('id.txt',encoding='euc-kr')

#키,값으로 분리된 상태로 넣기위해 텍스트 파일로 따로 저장
#csv 파일로 저장하면, 인덱스가 생겨서 스크립트에서 어려워짐
```