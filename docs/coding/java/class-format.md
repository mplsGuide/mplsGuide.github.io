---
title: Class Format 
parent: java
nav_order: 1
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
