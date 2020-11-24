# Memo Script For DCinside
## 개요
DCinside PC버전에서 모바일에서 사용하는 메모 기능을 이용하기 위해

확장 프로그램에 적용할 수 있는 스크립트

![image](https://user-images.githubusercontent.com/66747535/100087170-a77c2a00-2e91-11eb-9a92-f0b716547861.png)
- 특정한 IP나 ID에 메모를 추가하는 기능

- SKT, KT, LGU의 통신사 IP나 Proxy IP를 표시해주는 기능

- 기존에 DC 공식앱용으로 사용하던 메모 목록 변환해서 사용 가능

## 적용법

### 1. 크롬에서 아래 확장 프로그램 설치

https://chrome.google.com/webstore/detail/user-javascript-and-css/nbhcbdghjpllgmfilhnhkllmkecfmpld/related?hl=ko

### 2. 확장 프로그램을 누르고 Add new 클릭

(이미 다른 코드가 있어서 버튼이 없으면 톱니바퀴 누르고 Add new site 클릭)

![image](https://user-images.githubusercontent.com/66747535/100087699-718b7580-2e92-11eb-8e37-b67a2b00e722.png)

### 3. Settings 옆에 dcinside.com 또는 gall.dcinside.com을 입력

![image](https://user-images.githubusercontent.com/66747535/100087711-74866600-2e92-11eb-86a0-c0c078f69e76.png)

### 4. 아래의 소스 코드를 복사해서 왼쪽 JS 영역에 입력
<details>
  
```
(function(){
	
	// id, 메모, 글자색, 배경색
	// 글자색, 배경색 생략 가능
	var memo = new Array(
		['anyid', 'TEST','#FFFFFF', '#FF0000'],
		['255.255', 'TEST2']

	)
	//생략시 기본 글자색, 배경색
	var textColor2 = '#666666'
	var backColor2 = '#FFDF0E'
	
	//-----------------------------------------------------------------------------------------------------

	// SKT, KT, LGU, Proxy
	var ipname = ['SKT','KT','LGU','Proxy']
	var ip = new Array(
		['203.226', '223.63', '211.234', '115.161', '121.190', '122.202', '122.32', '175.202', '223.32', '223.33', '223.62', '223.38', '223.39', '223.57'],
		['118.235', '39.7', '110.70', '175.223', '175.252', '211.246', '210.125'],
		['106.101', '61.43', '114.200', '117.111', '211.36', '106.102', '125.188'],
		['67.207', '67.205', '46.101', '45.55', '37.139', '208.68', '207.154', '206.189', '198.211', '198.199', '192.81', '192.34', '192.241', '188.166', '178.62', '174.138', '167.99', '165.227', '162.243', '159.89', '159.65', '159.203', '146.185', '139.59', '138.68', '138.197', '128.199', '107.170', '104.236', '104.131', '188.226', '104.232', '164.132', '185.242', '38.132', '172.98', '188.172', '95.174', '185.217', '185.163', '139.99', '128.199', '178.62', '193.107', '222.251', '209.82', '139.59', '192.241', '70.71', '198.211', '87.101', '146.185', '145.239', '104.236', '109.224', '103.102', '178.62', '46.101', '95.174', '.181.40', '107.178', '45.33', '194.99', '141.0', '209.97', '203.175', '.96.245', '81.18', '5.199', '213.6', '166.216', '51.254', '207.189', '31.13', '216.162', '84.39', '27.118', '217.78', '82.102', '31.207', '168.235', '159.122', '89.46', '165.84', '90.254', '162.222', '178.128', '82.196', '12.129', '174.210', '85.115', '8.37', '185.236', '183.91', '185.104', '185.158', '185.232', '192.162', '157.82', '206.225', '172.58', '113.197', '91.235', '50.196', '216.9', '198.52', '77.111', '195.206', '185.4', '122.252', '96.74', '113.192', '101.15' ]
	);
	var textColor = ['#398764', '#D38402', '#A24CA0', '#ff0000'];
	var backColor = ['#D9FFDB', '#FFEDD2', '#FEE6FD', '#FEC3C3'];
	
	//-----------------------------------------------------------------------------------------------------
	// Made By KeNai
	// blog.naver.com/skahjqkrtk


	Array.from(document.getElementsByClassName('ub-writer')).forEach(function(e){
		
		//메모
		memo.forEach(function(x){
			if(x[0] == e.getAttribute('data-uid')){
				var mem = document.createElement("span");
				mem.appendChild(document.createTextNode(x[1]));
				mem.setAttribute('style', 'color:' + ((x[2]===undefined)?textColor2:x[2]) + ';background-color:' + ((x[3]===undefined)?backColor2:x[3]) + ';padding:3px;');
				e.appendChild(mem);
			}
			if(x[0] == e.getAttribute('data-ip')){
				var mem = document.createElement("span");
				mem.appendChild(document.createTextNode(x[1]));
				mem.setAttribute('style', 'color:' + ((x[2]===undefined)?textColor2:x[2]) + ';background-color:' + ((x[3]===undefined)?backColor2:x[3]) + ';padding:3px;');
				e.appendChild(mem);
			}
			
		});
		
		//통피, 프록시
		if(e.getAttribute('data-ip')){
			ip.forEach(function(x){
				if(-1 != x.indexOf(e.getAttribute('data-ip'))){
					e.getElementsByClassName('ip')[0].innerHTML = e.getElementsByClassName('ip')[0].innerHTML + " " + ipname[ip.indexOf(x)]
					e.getElementsByClassName('ip')[0].setAttribute('style', "color:" + textColor[ip.indexOf(x)]);
					e.style.backgroundColor = backColor[ip.indexOf(x)];
				}
			});
		}
	});
})();
```
</details>

### 5. 메모 목록 추가
```
	var memo = new Array(
	    // id, 메모, 글자색, 배경색
	    // 글자색, 배경색 생략 가능
	    ['anyid', 'TEST','#FFFFFF', '#FF0000'],
        ['anyid2', 'TEST2'],
		['255.255', 'TEST3']

	)
```
  
### 5-1. 메모 목록 변환기 이용
```
anyid-TEST
anyid2-TEST2
255.255-TEST3
```
DC 공식 앱의 메모 기능을 이용하기 위해

흔히 위와 같은 형식으로 메모 목록이 올라온다.

[메모_목록_변환기.xlsx](https://github.com/ke-nai/JavaScript-MemoScriptForDCinside/blob/main/%EB%A9%94%EB%AA%A8_%EB%AA%A9%EB%A1%9D_%EB%B3%80%ED%99%98%EA%B8%B0.xlsx)를 받아서

![image](https://user-images.githubusercontent.com/66747535/100087857-a7305e80-2e92-11eb-8ea5-76488c140bcc.png)

메모 목록을 변환기에 복사해 넣고

변환된 내용을 복사해서 코드에 넣으면 된다.

### 6. 적용시 아래와 같이 적용된다.
![image](https://user-images.githubusercontent.com/66747535/100087170-a77c2a00-2e91-11eb-9a92-f0b716547861.png)
