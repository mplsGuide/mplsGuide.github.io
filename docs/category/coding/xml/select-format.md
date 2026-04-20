```xml

<mapper namespace="연결할 Mapper의 경로 및 Mapper 파일명(../../UserMapper)">

····// Case 1) SELECT, CASE 활용 예시
····<!--
········사용자 정보 조회
········생성일자( 20xx.xx.xx )····수정자( SVN, GIT 등 )····내용( 최초 생성 )
········수정일자( 20xx.xx.xx )····수정자( SVN, GIT 등 )····수정 내용( 조회 조건 추가 )
····-->
····<select id="selectUser" parameterType="Map" resultType="UserModel">
········/* UserMapper.selectUser */
········SELECT··A.USER_ID
··············,·A.SEQ
··············,·A.USER_TY_CD
··············,·(··········
··················CASE·WHEN·B.MOBILE_NO·IS·NULL·OR·B.MOBILE_NO·=·''·THEN·REPLACE(A.MOBILE_NO,·'-',·'')
·······················ELSE·REPLACE(B.MOBILE_NO,·'-'·'')
··················END
················)·AS·MOBILE_NO
········FROM····TB_USER·A····-- 사용자 테이블
················LEFT·OUTER·JOIN·TB_EMP·B·ON·(·A.SEQ·=·B.USER_ID_SEQ·)····-- 사원 테이블
········WHERE·····A.USER_ID·=·#{userId}
········AND·······A.USE_YN··=·'Y'
····</select>

····// Case 2) SELECT, SubQuery 활용 예시
····<!--
········사용자 목록 조회
········생성일자( 20xx.xx.xx )····수정자( SVN, GIT 등 )····내용( 최초 생성 )
········수정일자( 20xx.xx.xx )····수정자( SVN, GIT 등 )····수정 내용( 조회 조건 추가 )
····-->
····<select id="selectUserList" parameterType="Map" resultType="UserModel">
········/* UserMapper.selectUserList */
········SELECT··A.USER_ID
··············,·A.SEQ
··············,·A.COMP_CD
··············,·(··········
··················SELECT··CMMN_NM
··················FROM····TB_CMMN_D
··················WHERE···CMMN_GROUP_CD·=·'USER_TY_CD'
··················AND·····CMMN_CD·=·A.USER_TY_CD
··················AND·····COMP_CD·=·A.COMP_CD
················)·AS·USER_TY_NM
········FROM····TB_USER·A····-- 사용자 테이블
················INNER·JOIN·TB_COMP·B·ON·(·A.COMP_CD·=·B.COMP_CD·)····-- 회사 구분 테이블
········WHERE·····A.USE_YN··=·'Y'

········-- 파라미터 값 있을 시에만 동작
········<if test="userId != null and userId != ''">
············AND·A.USER_ID·=·#{userId}
········</if>

········-- 파라미터 값 있을 시에만 동작
········<if test="compCd != null and compCd != ''">
············AND·A.COMP_CD·=·#{compCd}
········</if>

····</select>

</mapper>

```
