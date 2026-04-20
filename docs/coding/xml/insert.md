---
title: Insert
parent: xml
nav_order: 2
---

```xml

<mapper namespace="연결할 Mapper의 경로 및 Mapper 파일명(../../UserMapper)">

····// INSERT 활용 예시
····<!--
········사용자 등록
········생성일자( 20xx.xx.xx )····수정자( SVN, GIT 등 )····내용( 최초 생성 )
········수정일자( 20xx.xx.xx )····수정자( SVN, GIT 등 )····수정 내용( 조회 조건 추가 )
····-->
····<insert id="insertUser" parameterType="UserModel">
········/* UserMapper.insertUser */
········INSERT·INTO·TB_USER·(
··············USER_ID
············,·COMP_CD
············,·PASSWORD
············,·USER_NM
············,·USER_TY_CD
············,·MOBILE_NO
············,·REG_ID
············,·REG_DT
········)
········VALUES·(
··············#{userId}
············,·#{compCd}
············,·#{password}
············,·#{userNm}
············,·#{userTyCd}
············,·#{mobileNo}
············,·#{userId}
············,·GETDATE()
········)
····</insert>

</mapper>

```
