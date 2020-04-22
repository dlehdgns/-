# 블록 암호 운용 방식
***
## 전자 코드북 (ECB)
운용 방식 중 가장 간단한 구조, 암호화하려는 메시지를 여러 블록으로 나누어 각각 암호화하는 방식이다.   
![ECB](https://user-images.githubusercontent.com/53828976/79926858-f6d02700-8478-11ea-861c-69184139e4f5.PNG)   
전자 코드북(ECB)은 모든 블록이 같은 암호화 키를 사용하기 때문에 보안에 취약, 만약 암호화 메시지를 여러 부분으로 나누었을 때 두 블록이 같은 값을 가진다면, 암호화 결과도 역시 같다. 즉, 반복공격에 취약하다.   
![사진을 암호화](https://user-images.githubusercontent.com/53828976/79927506-e620b080-847a-11ea-9fae-eb1b9057e93e.PNG)   
원본그림 - ECB 방식으로 암호화 - ECB 이외의 방식으로 암호화 

## 암호 블록 체인 방식(CBC)
암호 블록 체인 방식(CBC)은 각 블록은 암호화되기 전에 이전 블록의 암호화 결과와 XOR되며, 첫 블록의 경우에는 초기화 벡터가 사용, 초기화 벡터가 같은 경우 출력 결과가 항상 같기 때문에, 매 암호화마다 다른 초기화 벡터를 사용해야 한다.   
![CBC](https://user-images.githubusercontent.com/53828976/79928154-15382180-847d-11ea-8454-a8e1c71fc071.PNG)   
암호화 입력 값이 이전 결과에 의존하기 때문에 병렬화가 불가능하지만 복호화의 경우 각 블록을 복호화한 다음 이전 암호화 블록과 XOR하여 복구할 수 있기 때문에 병렬화가 가능, 현재 널리 사용되는 운용 방식 중 하나이다.   

## 증식적 암호 블록 체인 방식(PCBC)
![PCBC](https://user-images.githubusercontent.com/53828976/79928357-b32bec00-847d-11ea-8250-1075fc335070.PNG)   

## 암호 피드백(CFB)
암호 피드백(CFB) 방식은 CBC의 변형으로, 블록 암호를 자기 동기 스트림 암호로 변환한다. CFB의 동작 방식은 CBC와 비슷하며, CFB 암호 해제 방식은  CBC 암호화의 역순과 거의 비슷하다.   
![캡처](https://user-images.githubusercontent.com/53828976/79928699-9a700600-847e-11ea-929f-e7b71cea94eb.PNG)   
![캡처1](https://user-images.githubusercontent.com/53828976/79928701-9ba13300-847e-11ea-83f1-defef6c5e5f5.PNG)   
![캡처2](https://user-images.githubusercontent.com/53828976/79928702-9c39c980-847e-11ea-98f7-b0a6144f9923.PNG)   
블록 암호화 알고리즘에 따라 Shift 연산을 사용하기도 한다. 이러한 방법을 Shift되는 비트의 양에 따라 CFB-8, 혹은 CFB-1이라고 한다. 암호화, 복호화 연산의 각 Round마다 IV로부터 Shift된 값을 사용한다.   

## 출력 피드백(OFB)
출력 피드백(OFB)은 블록 암호를 동기식 스트림 암호로 변환한다. XOR 명령의 대칭 때문에 암호화와 암호 해제 방식은 완전히 동일하다.     
![캡처](https://user-images.githubusercontent.com/53828976/79929447-b1aff300-8480-11ea-8a95-309fae7482ef.PNG)   
![캡처1](https://user-images.githubusercontent.com/53828976/79929450-b379b680-8480-11ea-9458-c14237bf4393.PNG)   
![캡처2](https://user-images.githubusercontent.com/53828976/79929451-b4aae380-8480-11ea-9b2e-571763daa543.PNG)   

## 카운터(CTR)
카운터(Counter, CTR) 방식은 블록 암호를 스트림 암호로 바꾸는 구조를 가진다. 카운터 방식에서는 각 블록마다 현재 블록이 몇 번째인지 값을 얻어, 그 숫자와 nonce를 결합하여 블록 암호의 입력으로 사용한다. 그렇게 각 블록 암호에서 연속적인 난수를 얻은 다음 암호화하려는 문자열과 XOR한다.

카운터 모드는 각 블록의 암호화 및 복호화가 이전 블록에 의존하지 않으며, 따라서 병렬적으로 동작하는 것이 가능하다. 혹은 암호화된 문자열에서 원하는 부분만 복호화하는 것도 가능하다.   
![캡처3](https://user-images.githubusercontent.com/53828976/79929624-3995fd00-8481-11ea-8b40-148b903e2036.PNG)
