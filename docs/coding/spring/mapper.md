---
title: Mapper 
parent: Spring
nav_order: 4
---

# Mapper

* 이 페이지는 Mapper 작성 양식과 역할, 어노테이션 등을 서술한 페이지입니다.

---

## Mapper의 역할

* Mapper는 데이터베이스 처리에서 사용되는 기능의 정의를 담당합니다.
* Service( 추상체 )와 유사하게 메서드의 형태(파라미터, 반환 타입)만 정의하고 실제 SQL은 작성하지 않습니다.
* ServiceImpl과 데이터베이스 사이를 연결하는 기준 역할을 수행합니다.
* 정의된 메서드는 MyBatis XML의 SQL 구문과 연결되어 실행됩니다.

---

### @Mapper

* 해당 인터페이스가 MyBatis Mapper임을 선언하는 어노테이션입니다.
* Spring이 해당 인터페이스를 Bean으로 등록하고, XML과 연결하여 사용할 수 있도록 합니다.
* 이를 통해 별도의 구현 클래스 없이도 SQL을 실행할 수 있습니다.
* Mapper로 선언된 인터페이스에 정의된 메서드는 MyBatis XML의 SQL과 매핑되어 실행됩니다.

---

### @Repository

* 해당 클래스가 DB 처리 역할을 수행하는 DAO 계층임을 선언하는 어노테이션입니다.
* Spring이 해당 객체를 관리하여 Service에서 자동으로 주입받아 사용할 수 있도록 합니다.
* DB 관련 예외를 Spring 표준 예외로 변환하여 일관된 예외 처리가 가능하도록 합니다.
* @Mapper와 함께 사용할 경우 해당 인터페이스는 MyBatis Mapper이면서 동시에 Spring의 DAO 컴포넌트로 관리됩니다.

---

## Mapper 작성 양식

* 아래는 회원에 관련된 내용을 처리하는 Mapper의 구성입니다.

* 개발 시에 주석, 개행, 띄어쓰기 등을 참조하여 작성해주시길 바랍니다.

---

```java

/**
 * UserMapper Class ( Class 명 Class )
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
@Mapper
@Repository
public interface UserMapper
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
