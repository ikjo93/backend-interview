### Q. @Transactional의 readOnly = true 속성은?

<details>
<summary>답변 확인하기</summary>
  
```
트랜잭션의 범위를 유지하되, 조회 기능만 남겨둠으로써 조회 속도가 개선되기 때문에,
등록/수정/삭제 기능이 전혀 없는 서비스 메서드에 사용 시 성능이 개선된다.
```

</details>
