## what spring rest docs?
요즘 개발하다가 문득 귀찮아서 계속 미루고있던 API문서 자동화에 대해서 간단하게 

적용한 예시를 적어본다

아래는 spring boot 기반 gradle 프로젝트 내부에서 작성한 코드이다.

우선각 버전에 맞는 디펜던시를 추가해준다(스프링과 그래들의 최소컷은 맞춰주어야함)

아래 코드와 같이 rest dosc는 TDD를 강제시 하기때문에 내가 테스트를 하고싶지않아도

어쩔수없이 작성을 해야만한다(테스트가 통과되야 문서가 만들어지는 아주 개같은놈..)

보기엔 되게 간단한 엔드포인트가 있는 rest API로 보이겠지만 실제로 적용하기까지

매우 많은 시행착오를 겪었다..

``` java
gradle dependency

dependencies {
    implementation 'org.springframework.boot:spring-boot-starter-web'
    testImplementation 'org.springframework.restdocs:spring-restdocs-mockmvc'
}
```

``` java
@RestController
@RequestMapping("/books")
public class BookController {

    public static class Book {
        private String title;
        private String author;

        public Book(String title, String author) {
            this.title = title;
            this.author = author;
        }

        public String getTitle() {
            return title;
        }

        public void setTitle(String title) {
            this.title = title;
        }

        public String getAuthor() {
            return author;
        }

        public void setAuthor(String author) {
            this.author = author;
        }
    }

    @GetMapping
    public List<Book> getBooks() {
        return Arrays.asList(
                new Book("The Catcher in the Rye", "J.D. Salinger"),
                new Book("To Kill a Mockingbird", "Harper Lee"),
                new Book("The Great Gatsby", "F. Scott Fitzgerald")
        );
    }

}
```

``` java
@RunWith(SpringRunner.class)
@WebMvcTest(BookController.class)
public class BookControllerTest {

    @Autowired
    private MockMvc mockMvc;

    @Autowired
    private ObjectMapper objectMapper;

    @Autowired
    private WebApplicationContext context;

    private RestDocumentationContextProvider restDocumentation = 
        new RestDocumentationContextProvider();

    @Rule
    public JUnitRestDocumentation restDocumentation = 
        new JUnitRestDocumentation("target/generated-snippets");

    @Before
    public void setUp() {
        this.mockMvc = MockMvcBuilders.webAppContextSetup(this.context)
                .apply(documentationConfiguration(this.restDocumentation))
                .build();
    }

    @Test
    public void getBooks() throws Exception {
        this.mockMvc.perform(get("/books"))
                .andExpect(status().isOk())
                .andExpect(content().contentType(MediaType.APPLICATION_JSON))
                .andExpect(jsonPath("$", hasSize(3)))
                .andDo(document("get-books",
                        preprocessRequest(prettyPrint()),
                        preprocessResponse(prettyPrint()),
                        responseFields(
                                fieldWithPath("[].title").description("The title of the book"),
                                fieldWithPath("[].author").description("The author of the book")
                        )
                ));
    }
}
```