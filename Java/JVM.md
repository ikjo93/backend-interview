### Q. Java에서 정수형 데이터를 처리할 때 int 자료형을 사용하는 것이 효율적인 이유는?

<details>
<summary>답변 확인하기</summary>
  
```
JVM의 피연산자 스택(operand stack)이 피연산자를 4byte 단위로 저장하기 때문에
크기가 4 byte 보다 작은 자료형(byte, short)의 값을 계산할 때는 4 byte로 변환하여 연산이 수행된다.
그래서 오히려 int를 사용하는 것이 더 효율적이다.
```
  
</details>
