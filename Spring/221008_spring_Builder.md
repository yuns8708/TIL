# Builder

빌더 패턴이란, 복잡한 객체의 생성 과정 및 표현 방법을 분리해 동일한 생성 절차에서 서로 다른 표현 결과를 만들 수 있게 하는 패턴이다.

## Builder의 장점
- 필드에 어떤 값을 넣을지 명확하게 지정 가능함
- 생성자 방식보다 가독성이 좋다
- setter을 이용하는 방식보다 안전하다
- setter 생성을 방지해 불변성을 보장한다 (객체를 변경할 수 없음)

---

## Builder 만들기
1. 클래스에 annotation 붙이기
```java
@AllArgsConstructor
@Builder
```

2. builder만들기
```
생성자 이름 from (매개변수) {
	return 생성자이름.builder()
    	.필드이름()
        .필드이름()
        .build();
}
```

ex) BoardListResponseDto.java

```java
// builder 사용했을 때
    public BoardListResponseDto from (Board board) {
        return BoardListResponseDto.builder()
                .title(board.getTitle())
                .createdAt(board.getCreatedAt())
                .modifiedAt(board.getModifiedAt())
                .username(board.getAccount().getUsername())
                .build();
    }

// 기존 생성자를 사용했을 때
    public BoardListResponseDto(Board board) {
        this.title = board.getTitle();
        this.createdAt = board.getModifiedAt();
        this.modifiedAt = board.getCreatedAt();
        this.username = board.getAccount().getUsername();
    }
```

boardService.java
```java
// builder 사용 글 생성
    public BoardResponseDto createBoard(BoardRequestDto requestDto, Account account) {
        Board board = new Board(requestDto, account);
        boardRepository.save(board);
        return new BoardResponseDto().from(board);
    }

// 기본 생성자 사용 글 생성
    public BoardResponseDto createBoard(BoardRequestDto requestDto, Account account) {
        Board board = new Board(requestDto, account);
        boardRepository.save(board);
        return new BoardResponseDto(board);
    }
```
---

## @Builder.Default

builder에서 필드의 값을 지정하지 않으면 타입에 따라 0, null, false로 초기화된다.

만약 원하는 값으로 초기화시키고싶을 때는, 필드에 @Builder.Default를 사용한다.

```java
    @Builder.Default
    private String title = "default title";
```