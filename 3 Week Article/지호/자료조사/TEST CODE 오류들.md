### Argument passed to verify() should be a mock but is null!

- verify(hostRepository.countIvtPpl(1L), times(numberOfOrders));
- verify 메서드를 다르게 작성함
- https://stackoverflow.com/questions/28895450/jersey-mockito-nullinsteadofmockexception-on-client-post-call-verification

### java.lang.RuntimeException: java.lang.NullPointerException

- 주입 받고 있는 객체에 null 포인트 익셉션
- https://cornswrold.tistory.com/479
