---
title: Model 
parent: Spring
nav_order: 1
---

# Model

* 이 페이지는 Model 작성 양식과 역할, 어노테이션 등을 서술한 페이지입니다.

---

## Model의 역할

* Model은 모든 구간에서 데이터를 전달하는 공통 객체로 사용됩니다.
* 주로 요청(Request), 응답(Response), DB 데이터 등을 담는 용도로 사용됩니다.
* 일관된 데이터 구조를 유지하여 코드의 가독성과 재사용성을 높이는 역할을 합니다.

---

### @Getter, @Setter

* Lombok에서 제공하는 어노테이션으로, 필드에 getter/setter 메서드를 자동 생성합니다.
* 코드의 반복 작성을 줄이고, 객체 접근을 간결하게 구성할 수 있습니다.

---

### @ToString

* 객체의 필드 값을 문자열 형태로 출력할 수 있도록 toString() 메서드를 자동 생성합니다.
* 로그 확인이나 디버깅 시 객체 내용을 쉽게 확인할 수 있습니다.

---

### Serializable

* 해당 객체를 직렬화(Serialization)할 수 있도록 하는 인터페이스입니다.
* 객체를 파일로 저장하거나, 네트워크 전송, 세션 저장 등에 활용할 수 있습니다.
* 클래스 변경 시 발생할 수 있는 직렬화 호환 문제를 방지하기 위해 serialVersionUID을 별도로 설정할 수 있습니다.
* 사용 예시 ) private static final long serialVersionUID = 생성한 UID;

---

## Model 작성 양식

* 아래는 회원에 관련된 내용을 담고있는 Model의 구성입니다.

* 개발 시에 주석, 개행, 띄어쓰기 등을 참조하여 작성해주시길 바랍니다.

---

```java

/**
 * UserModel Class ( Class 명 Class )
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
@Getter
@Setter
@ToString
public class UserModel implements Serializable
{
    private static final long serialVersionUID = 생성한 UID;

    /** SEQ */
    private int seq;
    
    /** 사용자 ID */
    private String userId;
    
    /** 사용자 권한 코드 */
    private String userTyId;
    
    /** 사용자 전화번호 */
    private String mobileNo;

    /** 비밀번호 */
    private String password;
    
    /** 회사 코드 */
    private String compCd;
    
    /** 사용여부 */
    private String useYn;

    /** 등록자 */
    private String regId;

    /** 등록일자 */
    private String regDt;

    /** 수정자 */
    private String updId;

    /** 수정일자 */
    private String updDt;

}

```
