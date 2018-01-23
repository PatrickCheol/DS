

# Register
레지스터란 CPU 내부에 존재하는 다목적 저장 공간이다. 리버싱을 위해 프로그램을 들여다보면 대부분 어셈블리 명령어가 레지스터를 조작하고 그 내용을 검사하는 내용이라서 레지스터에 대해 잘 알고 있어야 리버싱이 가능하다고 볼 수 있다.  

##### *IA-32 Register(Intel Architecture 32 Bit)  인텔에서 사용하는 32비트의 레지스터다. 

디버깅 초급 단계에서는 Basic program execution register에 대해서 알아두어야 한다. 이후 고급 과정에서 Control registers, Memory management register, Debug register에 대해서도 추가 공부가 필요하다.  

Basic program execution register은 크게 4개의 그룹으로 나눌 수 있다.  
![Alt text](https://i.imgur.com/2Q293YP.png)  
레지스터 이름에 E(Extenede)가 붙은 경우는 예전 16비트 CPU에서 32비트 크기로 확장 시켰다는 뜻이다.  

#### 범용 레지스터 (General Register)  
범용적으로 사용되는 레지스터이다. 여러곳에 쓰임 각 크기는 32비트(4바이트)이며, 보통 상수/주소 등을 저장할 때 사용된다. 
특정 어셈블리 명령에서는 특정 레지스터를 조작하기도 한다.
EAX를 기준으로 4바이트를 다 사용하고 싶을 때는 EAX를 사용하고 2바이트만 사용할 때는 EAX의 하위 16비트인 AX를 사용하면 된다. 그 절반 도 AH/AL로
상황에 맞게 8,16,32비트로 사용가능 하다.  

> - EAX : Accumulator for opeands and results data
> - EBX : Pointer to data in the DS segment
> - ECX : Counter for string adn loop operations
> - EDX : I/O pointer  

위 4개의 레지스터들은 주로 산술연산(ADD,SUB,XOR,OR 등) 명령어에서 상수/변수 저장 용도로 많이 사용된다.  
추가적으로 ECX, EAX는 특수한 용도로 사용되며 ECX는 반복문에서 카운터로 사용되고 EAX는 보통 함수 리턴 값에 사용된다. 모든 WIn32 API 함수들은 리턴값을 EAX에 저장한 후 리턴한다.  

> - EBP : Pointer to data on the stack
> - ESI : Source pounter for string operations
> - EDI : destination pointer for string operations
> - ESP : Stack pointer (in the SS segment)

위 4개의 레지스터들은 주로 메모리 주소를 저장하는 포인터로 사용된다.  
ESP는 스택 메모리 주소를 가르킨다. 어떤 명령어들(PUSH,POP,CALL,RET)는 ESP를 직접 조작하기도 한다.  
EBP는 함수가 호출되었을 때 그 순간의 ESP를 저장하고 있다가, 함수가 리턴하기 직전에 다시 ESP에 값을 되돌려줘서 그택이 꺠지지 않도록 한다. (함수 호출 이후 원래 주소로 돌아가기 위해 쓰이는것으로 생각 해당 기법을 Stack Frame 이라고 하는듯)  
ESI와 EDI는 특정 명령어들(LODS,STOS,REP MOVS 등)과 함께 주로 메모리 복사에 사용된다.  

#### 세그먼트 레지스터(Segment Register)  
IA-32 보호 모드에서 세그먼트란 메모리를 조각내어 각 조각마다 시작 주소, 범위, 접근 권한 등을 부여해서 메모리를 보호하는 기법을 말한다.  
세그먼트 메모리는 Segment Descriptor Table(SDT)이라고 하는 곳에 기술되어 있는데, 세그먼트 레지스터는 바로 이 SKT의 index를 가지고 있다.  
세그먼트 레지스터는 총 6개(CS, SS, DS, ES, FS, GS)이며 각각 크기는 16비트(2바이트)이다.  
각 세그먼트 레지스터가 가리키는 세그먼트 리스크립터와 가상 메모리가 조합되어 선영주소가 되며, 페이징 기법에 의해서 선형 주소가 최종적으로 물리적 주소로 변환된다. 

> - CS : Code Segment
> - SS : Stack Segment
> - DS : Data Segment
> - ES : Extra(data) Segment
> - FS : Data Segment
> - GS : Data Segment 
![Alt text](/segment_register.png)  




