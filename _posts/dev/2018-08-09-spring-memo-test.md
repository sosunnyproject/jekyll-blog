---
layout: post
categories: dev
title: "spring 데모 만들기"
date: 2018-08-09T13:01:27-05:00
last_modified_at: 2018-08-09T13:01:27-05:00
share: true
---

**메모장 만들기 구조**

### web-app
- **manager** : maven dependencies ::: .., model, rest-client
  - web
    - controller
      - [7] MemoController.java
      - MemoController가 MemoClient를 요청하는 형식
      - `import MemoVo, MemoClient, HttpServlet...`
      - tomcat 돌려서 전체 웹사이트 + uri 지정 (/setting/memo)
      ```java
        @Controller
        @RequestMapping(value="/setting/memo")
        public class MemoController extends ExceptionHandleController {
            @Autowired
            private MemoClient memoClient;
            @Autowired
            private AuthTokenStore authTokenStore;
            @RequestMapping(value="/list", method=RequestMethod.GET)
            public String getMemoList(HttpServletRequest request, Model model) throws GenericException {
                List<MemoVo> memoList = memoClient.getMemoList(authTokenStore.getAccessToken(request.getSession().getId()));		
                model.addAttribute("memoList", memoList);
                return "setting/memo/list";
            }
        }
      ```
    - WEB-INF/setting/memo
      - [8] list.jsp
        - c: 서버쪽 코드, JSTL 라이브러리의 core, 
        - memoController 의 memoList 가지고 와서 루프 돌리면서 프린트해주는 형식. 
        ```jsp
        		<tbody>
                    <c:if test='${not empty memoList}'>
                        <c:forEach items='${memoList}' var="m" varStatus="loop">
                            <tr class="row-mid">
                                <td style="width: 30px"><label> <input type="checkbox" rel="icheck" class="table-checkable-row" name="memo" value="${m.memoId}"></label></td>
                                <td>${m.memoId}</td>
                                <td>${m.memoTitle}</td>
                                <td>${m.memoContents}</td>
                                <td><fmt:formatDate value="${m.createDate}" pattern="yyyy-MM-dd HH:mm"/></td>
                            </tr>
                        </c:forEach>
                    </c:if>
                </tbody>
        ```

- **auth** : maven dependencies :: .., data, model

- **api**
  - resources/mybatis
    - [7] mybastis-config.xml: `typeAlias type="com.example.model.MemoVo" alias="memo" />` 추가
  - web
    - cloud
        - [4] MemoResource.java: memoService의 getMemoList 콜, memo 접근할 Request URL 지정
        ```java
        @RestController
        @RequestMapping(value="/memo")
        public class MemoResource extends ExceptionHandleResource {
            @Autowired
            private MemoService memoService;
            /*
            * 메모 목록 
            * @return List<MemoVo>
            */
            @GetMapping(value="/list")
            public List<MemoVo> getMemoList() throws GenericException {
                return memoService.getMemoList();
                //return null;
            }
        }
        ```



### rest-client
- [6] MemoClient.java
  - extends OauthRestClient
  - @Autowired restTemplate
  ``` java
    public List<MemoVo> getMemoList(String accessToken) throws RestClientException {
            try {
                ResponseEntity<List<MemoVo>> responseEntity = restTemplate.exchange(message.getMessage("....")+"/memo/list", HttpMethod.GET, getOauthNonParamsEntity(accessToken), new ParameterizedTypeReference<List<MemoVo>>() {});
                return responseEntity!=null ? responseEntity.getBody() : null;
            } catch(RestClientException e) {
                logger.error(e);
                throw new RestClientException(e.getLocalizedMessage());
            }
        }
   ```

### model
- [1] MemoVO.java
  - Vo: Value Object
  - 필요한 변수 및 변수의 타입들 생성+정의: memoId, memoTitle, memoContents, createDate ...
  - 마우스 우클릭 -- Source -- Generate Getter/Setter
  - 마우스 우클릭 -- Source -- Generate toString() 

    ```java
        private long memoId;  
        private String memoTitle; 
        private String memoContents;
        private Date createDate;

        public long getMemoId() {
            return memoId;
        }
        public void setMemoId(long memoId) {
            this.memoId = memoId;
        }
        public String getMemoTitle() {
            return memoTitle;
        }
        public void setMemoTitle(String memoTitle) {
            this.memoTitle = memoTitle;
        }
        public String getMemoContents() {
            return memoContents;
        }
        public void setMemoContents(String memoContents) {
            this.memoContents = memoContents;
        }
        public Date getCreateDate() {
            return createDate;
        }
        public void setCreateDate(Date createDate) {
            this.createDate = createDate;
        }

        @Override
        public String toString() {
            StringBuilder builder = new StringBuilder();
            builder.append("MemoVo [memoId=").append(memoId).append(", memoTitle=").append(memoTitle)
                    .append(", memoContents=").append(memoContents).append(", createDate=").append(createDate).append("]");
            return builder.toString();
        }
    ```

### data 
  - **src/main/java/.../data**
    - **persistence**
        - implementationClasses
            - [3] MemoDaoImpl.java  _____ 구현 클래쓰
                - `import MemoVo, MemoDao`
                - `memoMapper`도 data 하위에 있음.
                ```java
                    @Repository
                    public class MemoDaoImpl implements MemoDao {
                    
                        @Autowired
                        private SqlSession sqlSession;
                        @Override
                        public List<MemoVo> getMemoList() throws DataAccessException {
                            return sqlSession.selectList("memoMapper.getMemoList");
                        }
                    }
                ```

        - [2] MemoDao.java _____ 인터페이스
            - `import MemoVo`
            - DAO: DataAccessObject
            - getMemoList() 라는 함수를 정의한다.
            ```java
                public interface MemoDao {
                /**
                * @return List<MemoVo>
                * @throws DataAccessException
                */
                public List<MemoVo> getMemoList() throws DataAccessException; 
                }
            ```
    - **service**
        - implementationClasses
            - [5] MemoServiceImpl.java ____ 구현클래쓰
            - `import MemoVo, MemoDao, MemoService`
            ```java
                public class MemoServiceImpl implements MemoService {
                private static final Logger logger = LogManager.getLogger(MemoServiceImpl.class);           
                @Autowired
                private MemoDao memoDao;
                @Override
                public List<MemoVo> getMemoList() throws GenericException {
                    try {
                        return memoDao.getMemoList();
                    } catch(GenericException e) {
                        logger.error(e);
                        throw new GenericException(e.getLocalizedMessage());
                    }
                }	
                }
            ```

        - [4] MemoService.java ____ 인터페이스
         ```java
         public interface MemoService {
            public List<MemoVo> getMemoList() throws GenericException;
        }
        ```

  
- **src/main/resources/.../data/mapper**
  - memo-mapper.xml
  ```xml
    <?xml version="1.0" encoding="UTF-8" ?>
    <!DOCTYPE mapper ~~~ >

    <mapper namespace="memoMapper">

        <resultMap id="memo-result" type="memo">
            <result property="memoId" column="MEMO_ID" jdbcType="NUMERIC" />
            <result property="memoTitle" column="MEMO_TITLE" jdbcType="VARCHAR" />
            <result property="memoContents" column="MEMO_CONTENTS" jdbcType="VARCHAR" />
            <result property="createDate" column="CREATE_DATE" jdbcType="CHAR" typeHandler="com.example.jmf.jdbc.handler.DateTypeHandler" />
        </resultMap>
        
        <select id="getMemoList" parameterType="map" resultMap="memo-result">
            SELECT *
            FROM YOURDB.DB_MEMO
            ORDER BY MEMO_ID DESC
        </select>
        
    </mapper>
  ```