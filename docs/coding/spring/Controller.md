---
title: Controller 
parent: Spring
nav_order: 1
---

# Controller

* 이 페이지는 Controller 작성 양식과 각 어노테이션의 역할, 사용 방법 등을 서술한 페이지입니다.

---

## Controller의 역할

* Controller는 주로 사용자의 요청을 받고, 요청에 해당하는 부분을 처리하여 돌려주는 역할을 담당합니다.

---

## 어노테이션의 역할

* 어노테이션은 요청이나 값을 처리하는 방식을 정의하는 데에 사용합니다.

---

### @Controller

* 컨트롤러를 지정할 때 사용되는 어노테이션 입니다.

* Class에 사용하여 컨트롤러를 지정할 수 있습니다.

---

### @RequestMapping

* **@RequestMapping("/url/")**
  
  * Class에 사용하여 해당 컨트롤러로 요청받을 URL을 지정할 수 있습니다.

* **@RequestMapping( value = {"main"}, RequestMethod.GET )**

  * 메서드에 지정하여 URL과 GET/POST 방식을 지정할 수 있습니다.
  * GET/POST 지정 시에는 RequestMethod.GET/POST 형식을 사용하여 지정합니다.
  * GET/POST 설정이 없을 시 받은 요청의 형식에 따라서 매핑됩니다.

---

### @RequestBody

  * 요청 데이터를 JSON 형식으로 받습니다.

---

### @ResponseBody

  * 응답 데이터를 JSON 형식으로 보냅니다.

---

## 작성 양식

* 아래는 회원에 관련된 내용을 처리하는 Controller의 구성입니다.

* 개발 시에 주석, 개행, 띄어쓰기 등을 참조하여 작성해주시길 바랍니다.

---

```java

/**
 * UserController Class ( Class 명 Class )
 *
 * @version : 1.0
 * @author  : 생성자 ID ( SVN, GIT 등 )
 * @date    : 생성일자 ( 20xx.xx.xx )
 * @see
 *
 * <pre>
 * << 개정이력(Modification Information) >>
 * -----------------------------------------------------------------
 *     수정일            수정자                 수정내용
 * -----------------------------------------------------------------
 *     20xx.xx.xx        생성자 ID              최초 생성
 *
 * </pre>
 */
@Controller
@RequestMapping("/user/")
public class UserController
{
    // 로그 출력 시 사용 : logger.info(), logger.debug() 등으로 사용
    static final Logger logger = LoggerFactory.getLogger(MethodHandles.lookup().lookupClass());

    @Autowired
    private UserService userService;


    /**
     * 회원가입 팝업 View
     *
     * @version : 1.0
     * @author  : 생성자 ID ( SVN, GIT 등 )
     * @date    : 생성일자 ( 20xx.xx.xx )
     *
     * @param locale
     * @param model
     * @return
     */
    @RequestMapping( value = { "joinViewPopup" }, method = RequestMethod.GET )
    public String joinViewPopup( Locale locale, Model model )
    {
        return "user/joinViewPopup";
    }

    /**
     * 사용자 목록 조회
     *
     * @version : 1.0
     * @author  : 생성자 ID ( SVN, GIT 등 )
     * @date    : 생성일자 ( 20xx.xx.xx )
     *
     * @param map
     * @param model
     * @param session
     * @return
     * @throws Exception
     */
    @RequestMapping( value = { "getUserList" } )
    public @ResponseBody List<UserModel> getUserList( @RequestBody Map<String, Object> map,
                                                      Model model,
                                                      HttpSession session ) throws Exception
    {
        /** 사용자 목록 조회 */
        List<UserModel> userModels = userService.getUserList( map );

        return userModels;
    }

    /**
     * 사용자 정보 등록
     *
     * @version : 1.0
     * @author  : 생성자 ID ( SVN, GIT 등 )
     * @date    : 생성일자 ( 20xx.xx.xx )
     *
     * @param userJoinModel
     * @param model
     * @param locale
     * @param session
     * @return
     * @throws Exception
     */
    @PostMapping( value = "regUser" )
    public @ResponseBody Map<String, Object> regUser( @RequestBody UserJoinModel userJoinModel,
                                                       Model model
                                                       Locale locale
                                                       HttpSession session ) throws Exception
    {
        // 결과 Return 모델
        ResultModel resultModel = new ResultModel();

        try
        {
            /**
             * 사용자 정보 등록
             */
            userService.regUser( userJoinModel );

            resultModel.setResultCode(Constants.SUCCESS);
        }
        catch( BusinessException be )
        {
            resultModel = be.getResultModel();
        }
        catch( Exception e )
        {
            resultModel = new ResultModel(Constants.FAIL);
            resultModel.setResultMsg(e.getMessage());
        }

        Map<String, Object> ret = new HashMap<String, Object>();
        ret.put("result", resultModel);

        return ret;
    }


    /**
     * 사용자 정보 저장
     *
     * @version : 1.0
     * @author  : 생성자 ID ( SVN, GIT 등 )
     * @date    : 생성일자 ( 20xx.xx.xx )
     *
     * @param userJoinModel
     * @param model
     * @param locale
     * @param session
     * @return
     * @throws Exception
     */
    @PostMapping( value = "saveUser" )
    public @ResponseBody Map<String, Object> saveUser( @RequestBody UserModel userModel,
                                                       Model model
                                                       Locale locale
                                                       HttpSession session ) throws Exception
    {
        // 결과 Return 모델
        ResultModel resultModel = new ResultModel();

        try
        {
            /**
             * 사용자 정보 저장
             */
            userService.saveUser( userModel );

            resultModel.setResultCode(Constants.SUCCESS);
        }
        catch( BusinessException be )
        {
            resultModel = be.getResultModel();
        }
        catch( Exception e )
        {
            resultModel = new ResultModel(Constants.FAIL);
            resultModel.setResultMsg(e.getMessage());
        }

        Map<String, Object> ret = new HashMap<String, Object>();
        ret.put("result", resultModel);

        return ret;
    }

    /**
     * 사용자 정보 삭제
     *
     * @version : 1.0
     * @author  : 생성자 ID ( SVN, GIT 등 )
     * @date    : 생성일자 ( 20xx.xx.xx )
     *
     * @param map
     * @param model
     * @param locale
     * @param session
     * @param request
     * @return
     * @throws Exception
     */
    @PostMapping("userSecession")
    public @ResponseBody Map<String, Object> userSecession( @RequestBody Map<String, Object> map,
                                                            Model model,
                                                            Locale locale,
                                                            HttpSession session,
                                                            HttpServletRequest request ) throws Exception
    {
        // 결과 Return 모델
        ResultModel resultModel = new ResultModel();

        try
        {
            /**
             * 사용자 정보 삭제
             */
            userService.userSecession( map, request );

            resultModel.setResultCode(Constants.SUCCESS);
        }
        catch ( BusinessException be )
        {
            resultModel = be.getResultModel();
        }
        catch( Exception e )
        {
            resultModel = new ResultModel(Constants.FAIL);
            resultModel.setResultMsg(e.getMessage());
        }

        Map<String, Object> ret = new HashMap<String, Object>();
        ret.put("result", resultModel);

        return ret;
    }

}

```
