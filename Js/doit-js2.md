제어문
=========

* 제어문은 프로그램의 흐름을 제어할 수 있도록 도와주는 문장이다.


* 제어문의 종류
	* 조건문 (if, else, else if)
	* 선택문 (switch)
	* 반복문 (while, for)

	
선택문
--------

* switch문은 변수의 저장된 값과 switch문에 있는 case를 검사하여 변수와    
case의 값에서 일치하는 값이 있을때 그에 해당하는 코드를 실행한다.   
* if문과 비슷하지만 if문은 만족하는 데이터가 여러 개일 경우에 주로 사용하고     
switch문은 여러 경우의 값 중 일치하는 데이터를 찾을 경우에 주로 사용한다.   
 
```
var 변수 = 값;
switch(변수) {
case 값1 : 코드1;
break;
case 값2 : 코드2;
break;
case 값3 : 코드3;
break;
case 값4 : 코드4;
break;

dafault: 코드5;
}
```

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script>
        var site = prompt("네이버, 구글, 네이트 중 \
            즐겨 사용하는 포털 검색 사이트는?","");
        var url;
        switch(site) {
            case "구글" : url = "www.google.co.kr";
            break;
            case "네이버" : url = "www.naver.com";
            break;
            case "네이트" : url = "www.nate.com";
            break;
            default : alert("보기중에 없는 사이트입니다."); 
        }

        location.href = "https://" + url;
    </script>
</head>
<body>
   
</body>
</html>
```

반복문
---------

* while문은 조건식을 만족할 때까지 중괄호 안에 있는 코드를 반복하여 실행한다.


* while문의 실행 순서    
	1. 조건문 검사    
	2. 만족하면 중괄호 안 코드와 증감식 실행    
	3. 다시 조건식 검사   

```
var 변수  = 갑;
while(조건식) {
스크립트 코드;
증감식;
}
```

* 20부터 10까지 숫자중 짝수일 경우에는 파란색 출력 홀수일 경우에는 빨간색으로 출력

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        *{margin: 0;}
        .blue{color: #00f;}
        .red{color: #f00;}
    </style>
    <script>
        var i = 20;
        while(i >= 10) {
            if(i % 2 == 0) {
                document.write("<p class='blue'>" + i + "</p>");
            }
            else {
                document.write("<p class='red'>" + i + "</p>");
            }
            i--;
        }
        document.write("---------End---------");
    </script>
</head>
<body>
    
</body>
</html>
```

* do while문은 반드시 코드를 한번은 실행하고 조건식을 검사한다.

```
var = 변수 값;

do{ 
	스크립트 코드;
	증감식;
	} while(조건식)
```

* for문은 조건식을 만족할 때까지 코드를 반복하여 실행한다.

```
for(초깃값; 조건식; 증감식) {
스크립트 코드
}
```

* break문은 while문 또는 for문에서 사용되며 조건식과 상관없이 강제로 반복문을 종료한다.

```
for(초깃값; 조건문; 증감식) {
break; // 반복문을 강제로 종료시켜 뒤에 코드가 실행이 안됨
스크립트 코드;
}
```

* continue문은 반복문에서만 사용 가능하며 continue문 뒤에 있는 코드는 무시하고 조건식으로 이동해 조건 검사를 한다.

* 중첩 for문은 for문 안에 for문을 사용한 것으로 바깥족 for문이 한번 실행될 때마다  
안쪽 for문이 실행된다.

```
for(초깃값, 조건식, 증감식) {
	for(초깃값; 조건식; 증감식) {
	스크립트 코드;
	}
}
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script>
        for(var i = 1; i < 4; i++) {
            for(var k = 1; k<3; k++) {
                document.write(i + "행" + k + "열", "<br>");
            }
            document.write("<br>");
        }
    </script>
</head>
<body>
    
</body>
</html>
```
