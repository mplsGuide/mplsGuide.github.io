---
title: Update
parent: xml
nav_order: 3
---

```xml

<mapper namespace="연결할 Mapper의 경로 및 Mapper 파일명(../../UserMapper)">

····// UPDATE 활용 예시
····<!--
········사용자 수정
········생성일자( 20xx.xx.xx )····수정자( SVN, GIT 등 )····내용( 최초 생성 )
········수정일자( 20xx.xx.xx )····수정자( SVN, GIT 등 )····수정 내용( 조회 조건 추가 )
····-->
····<update id="updateUser" parameterType="UserModel">
········/* UserMapper.updateUser */
········UPDATE··TB_USER
········SET·····USER_NM···=·#{userNm}
··············,·MOBILE_NO·=·#{mobileNo}
··············,·UPD_ID····=·#{userId}
··············,·UPD_DT····=·GETDATE()

················<if test="userTyCd != null and userTyCd != ''">
····················,·USER_TY_CD·=·#{userTyCd}
················</if>

················<if test="password != null and password != ''">
····················,·PASSWORD·=·#{password}
················</if>

········WHERE···SEQ·····=·#{seq}
········AND·····COMP_CD·=·#{compCd}
········AND·····USER_ID·=·#{userId}
····</update>

</mapper>

```
