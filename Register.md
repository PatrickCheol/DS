.center {
  display: block;
  margin: auto;
}

# Register
레지스터란 CPU 내부에 존재하는 다목적 저장 공간이다. 리버싱을 위해 프로그램을 들여다보면 대부분 어셈블리 명령어가 레지스터를 조작하고 그 내용을 검사하는 내용이라서 레지스터에 대해 잘 알고 있어야 리버싱이 가능하다고 볼 수 있다.  

##### *IA-32 Register(Intel Architecture 32 Bit)  인텔에서 사용하는 32비트의 레지스터임  

디버깅 초급 단계에서는 Basic program execution register에 대해서 알아두어야 한다. 이후 고급 과정에서 Control registers, Memory management register, Debug register에 대해서도 추가 공부가 필요하다.  

Basic program execution register은 크게 4개의 그룹으로 나눌 수 있다.  
![Alt text](https://i.imgur.com/2Q293YP.png){: .center}

