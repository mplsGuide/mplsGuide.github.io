---
title: Delete
parent: xml
nav_order: 4
---

```xml

<mapper namespace="연결할 Mapper의 경로 및 Mapper 파일명(../../UserMapper)">

····// Case 1) DELETE 활용 예시
····<!--
········사용자 삭제
········생성일자( 20xx.xx.xx )····수정자( SVN, GIT 등 )····내용( 최초 생성 )
········수정일자( 20xx.xx.xx )····수정자( SVN, GIT 등 )····수정 내용( 조회 조건 추가 )
····-->
····<delete id="deleteUser" parameterType="UserModel">
········/* UserMapper.deleteUser */
········DELETE
········FROM····TB_USER
········WHERE···SEQ·····=·#{seq}
········AND·····COMP_CD·=·#{compCd}
········AND·····USER_ID·=·#{userId}
····</delete>

····// Case 2) UPDATE를 이용한 DELETE 활용 예시
····<!--
········사용자 삭제 ( 비활성화 )
········생성일자( 20xx.xx.xx )····수정자( SVN, GIT 등 )····내용( 최초 생성 )
········수정일자( 20xx.xx.xx )····수정자( SVN, GIT 등 )····수정 내용( 조회 조건 추가 )
····-->
····<update id="deleteUser" parameterType="UserModel">
········/* UserMapper.deleteUser */
········UPDATE··TB_USER
········SET·····USE_YN·=·'N'
········WHERE···SEQ·····=·#{seq}
········AND·····COMP_CD·=·#{compCd}
········AND·····USER_ID·=·#{userId}
····</update>

</mapper>

```
