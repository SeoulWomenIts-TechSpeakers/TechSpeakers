### 🙋‍♀️ API 연결 통신 오류

![Image](https://github.com/user-attachments/assets/5f2fc089-ecbc-4114-a897-1df6e471e18e)

- [서버 에러 문구]
  - `HttpMessageNotReadableException` Cannot deserialize instance of com.example.springboot.controller.dto.reserv.ResrvHistRequestDto out of START_ARRAY token; nested exception is com.fasterxml.jackson.databind.exc.MismatchedInputException
- [원인]
  - MappingJackson2HttpMessageConverter는 JsonParsingException할 때 발생하는 에러

#### API TEST CODE 로 에러 상황 분석

- API 연동에서 400 에러 발생
- 프론트에서 테스트 하는 것에 번거로움

##### mockMvc 서버 의존성 주입

```java
@DisplayName("apiUserCreateTest")
@Test
public void createUserTest() throws Exception {
    // given
    //요청 생성
    User user = userRepository.save(User.builder()
            .name("Jeeho Kim")
            .email("email")
            .build());

    // Resrv_hist 저장
    ResrvHistRequestDto histRequestDto = ResrvHistRequestDto.builder()
            .hnum("1")
            .userid(user.getId())
            .reqPpl(2)
            .build();

    String json = new ObjectMapper().writeValueAsString(histRequestDto);
    mockMvc.perform(
            MockMvcRequestBuilders.post("http://localhost:8080/api/resrv/save")
                    .content(MediaType.APPLICATION_JSON)
                    .content(json)
            ).andExpect(
                    MockMvcResultMatchers.status().isOk()
            ).andExpect(
                    MockMvcResultMatchers.jsonPath("$.result").value("0")
            ).andExpect(
                    MockMvcResultMatchers.jsonPath("$.response.resultCode").value("OK")
            )
            .andDo(MockMvcResultHandlers.print());
}
```

##### 테스트 코드 에러 문구

```
 null pointer exception
```

- 해당 경우는 Principal 객체가 없어서 발생하는 예
- 서버 상에는 핸들러 매퍼가 값을 잘 매칭해서 가져오는 것을 확인할 수 있음

  <br>  
  <br>

### ❓여전히 풀리지 않는 질문들
