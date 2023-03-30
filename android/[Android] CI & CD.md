# CI & CD
#### *CODE → BUILD → TEST → RELEASE → DEPLOY*
<br>

### 1. **CI (Continuous Integration 지속적인 통합)**
* 새로운 코드 변경 사항이 정기적으로 빌드, 테스트 되어 공유 repository 에 통합되는 것.
* 여러 명의 개발자가 형상관리 툴 (Git, SVN) 을 사용하는 경우 기능을 추가할 때마다 commit 으로 버전 업데이트를 하는데 이렇게 번거로운 일을 자동화하는 이점을 제공함.
* 개발 생산성을 향상시킬 수 있고, 버그 수정이 용이하며 문제점을 빠르게 발견할 수 있다는 장점이 있다. 

<br><br>

### 2. **CD (Continuous Delivery / Continuous Deployment)**
* 지속적인 서비스 제공 & 배포
* 둘의 차이점
  * Delivery 는 공유 repository 로 자동 release 하는 것 까지만 자동화되고, Deployment 는 production 레벨까지 자동으로 deploy 하는 것을 의미.

<br><br>

#### *→ DevOps 엔지니어는 CI/CD 를 위한 파이프라인을 구성하고 자동화단계까지 끌어 올리는 것 역할을 주로 함.*
#### *→ 대표적인 툴로는 Jenkins, Travis CI, Bamboo 등이 있다.*
