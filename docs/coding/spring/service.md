---
title: Service 
parent: Spring
nav_order: 3
---

# Service

* 이 페이지는 Service 작성 양식과 역할, 사용 방법 등을 서술한 페이지입니다.

---

## Service란?

* Service는 Controller와 DB 사이의 데이터 처리 및 흐름을 제어하는 역할을 담당합니다.
* 본 구조에서는 Service의 영역을 추상체( Service )와, 구현체( ServiceImpl )로 분리하여 관리합니다.
* 추상체( Service )는 **무엇을 할지**를 구현하고, 구현체( ServiceImpl )는 **어떻게 할지**를 구현합니다.

## Service의 역할 ( 추상체 / Interface )

* Service는 비즈니스 로직에서 사용되는 기능의 정의를 담당합니다.
* 각 기능의 명칭과 함께 요청(Request) 및 응답(Response)에 사용되는 파라미터와 반환 타입을 선언합니다.
* Controller와 ServiceImpl 사이를 연결하는 기준 역할을 수행합니다.
* 기능 구현은 포함하지 않으며, ServiceImpl( 구현체 )에서 해당 기능을 구현합니다.
* 선언 방법
  * **public interface UserService**

## ServiceImpl의 역할 ( 구현체 / Implements )

* ServiceImpl은 Service에 정의된 기능을 실제로 구현하는 역할을 합니다.
* Controller로부터 전달받은 데이터를 기반으로 비즈니스 로직을 수행하고 필요한 경우에는 DB를 호출하여 데이터 처리를 진행합니다.
* 처리 전 데이터를 가공하여 데이터 처리를 진행하거나 처리 결과를 가공하여 Controller에 반환할 수 있습니다.
* 선언 방법
  * **@Service( value = "userService" )**
  * **public class UserServiceImpl implements UserService**


---

### @Service

  * 해당 클래스가 Service 역할을 수행하는 클래스임을 선언하는 어노테이션입니다.

  * Spring이 해당 클래스를 Bean으로 관리하여, 다른 계층에서 자동으로 주입받아 사용할 수 있도록 합니다.

---

## Service 작성 양식

* 아래는 회원에 관련된 내용을 처리하는 Service의 구성입니다.

* 개발 시에 주석, 개행, 띄어쓰기 등을 참조하여 작성해주시길 바랍니다.

---

```java

/**
 * UserService Class ( Class 명 Class )
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
public interface UserService
{
    /**
     * 사용자 목록 조회
     *
     * @version : 1.0
     * @author  : 생성자 ID ( SVN, GIT 등 )
     * @date    : 생성일자 ( 20xx.xx.xx )
     *
     * @param map
     * @throws Exception
     */
    public List<UserModel> getUserList( Map<String, Object> map ) throws Exception;

    /**
     * 사용자 등록
     *
     * @version : 1.0
     * @author  : 생성자 ID ( SVN, GIT 등 )
     * @date    : 생성일자 ( 20xx.xx.xx )
     *
     * @param userJoinModel
     * @throws Exception
     */
    public void regUser( UserJoinModel userJoinModel ) throws Exception;

    /**
     * 사용자 수정
     *
     * @version : 1.0
     * @author  : 생성자 ID ( SVN, GIT 등 )
     * @date    : 생성일자 ( 20xx.xx.xx )
     *
     * @param userModel
     * @throws Exception
     */
    public void updateUser( UserModel userModel ) throws Exception;

    /**
     * 사용자 삭제
     *
     * @version : 1.0
     * @author  : 생성자 ID ( SVN, GIT 등 )
     * @date    : 생성일자 ( 20xx.xx.xx )
     *
     * @param map
     * @throws Exception
     */
    public void deleteUser( Map<String, Object> map ) throws Exception;

}

```

---

## ServiceImpl 작성 양식

* 아래는 회원에 관련된 내용을 처리하는 ServiceImpl의 구성입니다.

* 개발 시에 주석, 개행, 띄어쓰기 등을 참조하여 작성해주시길 바랍니다.

```java

/**
 * UserService Class ( Class 명 Class )
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
@Service( value = "userService" )
public class UserServiceImpl Implements UserService
{
    // 로그 출력 시 사용 : logger.info(), logger.debug() 등으로 사용
    static final Logger logger = LoggerFactory.getLogger(MethodHandles.lookup().lookupClass());

    /**
     * 사용자 목록 조회
     *
     * @version : 1.0
     * @author  : 생성자 ID ( SVN, GIT 등 )
     * @date    : 생성일자 ( 20xx.xx.xx )
     *
     * @param map
     * @throws Exception
     */
    public List<UserModel> getUserList( Map<String, Object> map ) throws Exception
    {
        return userMapper.getUserList( map );
    }

    /**
     * 사용자 등록
     *
     * @version : 1.0
     * @author  : 생성자 ID ( SVN, GIT 등 )
     * @date    : 생성일자 ( 20xx.xx.xx )
     *
     * @param userJoinModel
     * @throws Exception
     */
    public void regUser( UserJoinModel userJoinModel ) throws Exception
    {
        Map<String, Object> paramMap = null;

        boolean isDup = false;

        paramMap = new HashMap<String, Object>();
        paramMap.put("userId", userJoinModel.getUserId());

        /**
         * 사용자 ID 중복 확인
         */
        isDup = this.isDuplicationUserId(paramMap);
        
        if ( !isDup )
        {
            try
            {
                userJoinModel.setUserTyCd("ROLE_USER");

                userMapper.createUser( userJoinModel );
            }
            catch ( Exception e )
            {
                logger.error(CommonUtils.getPrintStackTrace(e));

                throw new Exception("오류가 발생하였습니다. 관리자에게 문의해주세요.");
            }
        }
        else
        {
            ResultModel resultModel = new ResultModel(Constants.FAIL);
            resultModel.setResultMsg("중복된 사용자 ID입니다.");

            throw new BusinessException(resultModel);
        }
        
        
    }

    /**
     * 사용자 수정
     *
     * @version : 1.0
     * @author  : 생성자 ID ( SVN, GIT 등 )
     * @date    : 생성일자 ( 20xx.xx.xx )
     *
     * @param userModel
     * @throws Exception
     */
    public void updateUser( UserModel userModel ) throws Exception
    {
         userMapper.updateUser( userModel );
    }

    /**
     * 사용자 삭제
     *
     * @version : 1.0
     * @author  : 생성자 ID ( SVN, GIT 등 )
     * @date    : 생성일자 ( 20xx.xx.xx )
     *
     * @param map
     * @throws Exception
     */
    public void deleteUser( Map<String, Object> map ) throws Exception;
    {
        String userId = (String) map.get("userId");

        Map<String, Object> paramMap = new HashMap<String, Object>();
        paramMap.put("userId", userId);
        paramMap.put("password", password);

        /**
         * 사용자 정보 조회
         */
        UserModel userModel = userMapper.getUser( map );

        if ( !ObjectUtils.isEmpty(userModel) && !StringUtils.isEmpty(userModel.getUserId()) )
        {
            userModel.setPassword(password);

            int deleteUserCnt = userMapper.deleteUser(userModel);

            if ( deleteUserSpprnCnt == 0 || deleteUserCnt == 0 )
            {
                logger.error("=============================== [ERROR Start] ==================================");
                logger.error("[UserServiceImpl.deleteUser] 사용자 삭제 처리 오류 발생. ");
                logger.error("아이디 : " + userModel.getUserId()");
                logger.error("=============================== [ERROR End] ==================================");

                ResultModel resultModel = new ResultModel(Constants.FAIL);
                resultModel.setResultMsg("오류가 발생하였습니다. 관리자에게 문의해주세요.");

                throw new BusinessException(resultModel);
            }

        }
        else
        {
            ResultModel resultModel = new ResultModel(Constants.FAIL);
            resultModel.setResultMsg("비밀번호가 일치하지 않습니다.");

            throw new BusinessException(resultModel);
        }
    }

    /**
     * 사용자 ID 중복 확인
     *
     * @version : 1.0
     * @author  : 생성자 ID ( SVN, GIT 등 )
     * @date    : 생성일자 ( 20xx.xx.xx )
     *
     * @param map
     * @throws Exception
     */
    public boolean isDuplicationUserId( Map<String, Object> map ) throws Exception
    {
        boolean isDup = true;

        /**
         * 사용자 ID 존재 여부
         */
        CargoMap cargoMap = userMapper.isExistUserId( map );

        String isExistUserId = (String)cargoMap.get("isExistUserId");

        if ( "N".equals(isExistUserId))
        {
            isDup = false;
        }

        return isDup;
    }

}

```
