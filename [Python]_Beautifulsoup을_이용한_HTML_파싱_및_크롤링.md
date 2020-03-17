# Beautifulsoup을 이용한 HTML 파싱 및 크롤링



### Python을 이용한 공공데이터포털의 파일데이터 목록 크롤링



#### BeautifulSoup ?

: HTML 파싱 라이브러리, 기본적으로 UTF-8 인코딩 방식이지만 XML 파싱도 가능하다.



#### BeautifulSoup4 설치

- C:\Users\skybl\AppData\Local\Programs\Python\Python37-32\Scripts
- 관리자 CMD 실행, beautifulsoup4 설치 : pip install beautifulsoup4



#### **BeautifulSoup 기본 설정**

---

**▶ package import**

```python
from bs4 import BeautifulSoup
```



**▶ urllib을 통해 웹에 있는 소스 가져오기**

**url에 원하는 URL 추가**

```python
import urllib.request
import urllib.parse


html = urllib.request.urlopen(url).read()
soup = BeautifulSoup(html, 'html.parser')
```

- **urllib.requset.urlopen()** 함수는 웹 서버에 정보를 요청한 후, 돌려받은 응답을 저장하여 '응답 객체(HTTPResponse)'를 반환한다.

- 반환된 응답 객체의 **read()** 메서드를 실행하여 웹 서버가 응답한 데이터를 바이트 배열로 읽어 들인다.



#### **공공데이터포털 파싱 및 크롤링**

------

- URL 주소는 공공데이터포털 **페이지 소스보기**를 통해 얻어왔다. 현재는 **파일데이터**에 한해서만 크롤링이 가능하다. 
- OPEN API 또는 표준 데이터 목록을 크롤링을 하고 싶으면 **index 뒤에 원하는 데이터 타입을 입력**하면 된다. 공공데이터포털의 경우 키워드를 검색하면 한 페이지 당 10개의 리스트(**countPerPage**)가 검색된다.

이를 이용해서 **데이터 이름, URL 주소, 상세 설명**을 파싱 및 크롤링 해본다.

```python
import urllib.request
import urllib.parse
from bs4 import BeautifulSoup


plusUrl = urllib.parse.quote_plus(input('검색어 입력:'))
# 사용자가 원하는 키워드 입력

pageNum=1


i = input('몇페이지 크롤링?\n')
lastPage = int(i)

while pageNum < lastPage + 1:// while 문을 통해 원하는 페이지까지 크롤링 설정


    url = f'https://www.data.go.kr/search/index.do?index=DATA&currentPage={pageNum}&countPerPage=10&sortType=VIEW_COUNT&data-order="DESC"&query={plusUrl}'
	

    html = urllib.request.urlopen(url).read()
    soup = BeautifulSoup(html, 'html.parser')


    for j in soup.find_all('div', class_='data-item'):
        // 총 10개의 'data-item' 리스트를 for 문을 이용하여 호출
        
        
        tag1 = j.find('div',attrs={'class':'data-title'}).find('a')
		//div class='data-item'내에 존재하는 'data-title'을 찾고, 그 안에 a 태그를 찾는다.

        tag2 = j.find('div',attrs={'class':'data-desc'})
		//div class='data-item'내에 존재하는 'data-desc'를 찾는다.

        tag3 = tag1['href']
        url1 = f'https://www.data.go.kr{tag3}'
        // tag1 중 'href' 태그를 찾고, URL 형태로 만들어 준다.
        

        html1 = urllib.request.urlopen(url1).read()
        soup1 = BeautifulSoup(html1, 'html.parser')
        tag4 = soup1.find('a', {'id': 'url-in-detail-btn'})
        print(tag4)

        print('--------------------')
        # tag1 중 text만 추출(.text)하고, 왼쪽의 공백을 제거(.lstrip())한다
        print(tag1.text.lstrip())
        print(url1)
        print(tag2.text.lstrip())


    pageNum += 1
```

![img](https://k.kakaocdn.net/dn/cDPH5O/btqCD9zKF1y/JPldME67gGGhPu5KMnAFDk/img.png)



![img](https://k.kakaocdn.net/dn/bJlrjl/btqCF6PNVE1/4zd8PMWkOSSl7VidQt4LQ1/img.png)

​																	**[실행 결과]**



**※ URL 뒤에 jsessionid 가 같이 출력되는 경우 해결 방법을 찾아야 함.**



**참고:**

**https://twpower.github.io/84-how-to-use-beautiful-soup**

https://victorydntmd.tistory.com/245

[https://toentoi.tistory.com/43﻿](https://toentoi.tistory.com/43)