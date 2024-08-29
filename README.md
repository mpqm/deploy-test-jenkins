# 🐈 사부작즈 DevOps 프로젝트 🐿️
<br><br>



<div align=center>
	<h4>
    <!--이미지 넣기? 폴더예시:<img src="https://github.com/beyond-sw-camp/be06-1st-ketchop-mojal/blob/dev/assets/image/project_background.PNG" width="60%" /> -->
 		자동화된 프로세스를 통해 반복 작업을 최소화하고 <br> 개발 속도를 향상시키기 위한 <br> 사부작사부작 데브옵스 환경 구성 프로젝트입니다.
	</h4>
</div>
<br><br><br>




# 🧑‍🔧 팀원
<h4>🐹구은주 <a href="https://github.com/eunjooNine"> @eunjooNine</a></h4>
<h4>🐱박종성 <a href="https://github.com/mpqm"> @mpqm</a></h4>
<h4>🐸서시현 <a href="https://github.com/SihyunSeo"> @SihyunSeo</a></h4>
<h4>🐻서재은 <a href="https://github.com/seo-jae-eun"> @seo-jae-eun</a></h4>
<!--<h4>🦉장유정 </h4>-->
<br><br><br><br>




# 🛠 기술 스택
<img src="https://img.shields.io/badge/GitHub-181717?style=flat&logo=GitHub&logoColor=white" /></a>
<img src="https://img.shields.io/badge/Git-F05032?style=flat&logo=Git&logoColor=white&color=ffa500"></a>
<img src="https://img.shields.io/badge/GitHub Actions-2088FF?style=flat&logo=GitHub Actions&logoColor=white&color=gray"></a>
&nbsp;&nbsp;&nbsp;&nbsp;
<img src="https://img.shields.io/badge/Jenkins-D24939?style=flat&logo=jenkins&logoColor=white"/></a>
<img src="https://img.shields.io/badge/Docker-2496ED?style=flat&logo=Docker&logoColor=black&color=blue"/></a>
<img src="https://img.shields.io/badge/Kubernetes-326CE5?style=flat&logo=Kubernetes&logoColor=blue&color=skyblue"/></a>
&nbsp;&nbsp;&nbsp;&nbsp;
<img src="https://img.shields.io/badge/vuejs-%2335495e.svg?style=flat&logo=vuedotjs&logoColor=%234FC08D"/></a>
<img src="https://img.shields.io/badge/SpringBoot-181717?style=flat&logo=SpringBoot&logoColor=6DB33F&color=white"></a>
<br><br><br><br><br>




# 🏡 CI/CD 프로젝트 목표
git을 이용해 작업하면서 기능별로 빌드, 테스트, 병합까지 하는 번거로운 과정을 지속적인 통합으로 해결할 수 있습니다. <br>
이후, 개발에서의 변경사항이 지속적인 배포로 서비스의 사용자가 최대한 빠른 시간 내에 최신 버전의 서비스를 제공받을 수 있게 할 수 있습니다. <br>
이러한 CI/CD가 필요한 환경속에서 자동화된 `배포 파이프라인 구축`, `효율적인 컨테이너화`, `신속한 배포 및 롤백`, `확장성과 안정성 확보`, <br> `지속적인 통합 및 배포(CI/CD) 프로세스 최적화`의 다섯가지 목표로 안정적이고 빠른 배포 프로세스를 이용하여 더 높은 생산성을 달성하고자 합니다.
<br><br><br><br>




# 🌳 운영 환경
### 서버 구성 ⚙️
Kubernetes Master server 1 🖥️ <br>
Kubernetes Worker server 4 🖥️🖥️🖥️🖥️<br>
Jenkins server 1 🖥️<br>
쿠버네티스의 클러스터 노드 구성입니다.
<br><br><br><br>




### 시스템 아키텍처 ⚙️
![시스템 아키텍처](https://github.com/user-attachments/assets/166c8c21-9515-4329-ae5a-cc828f3f9735)
<br>

**구성 요소 간의 연결**

- **젠킨스 <-> 깃허브**: 웹훅을 통해 젠킨스가 깃허브에서 변경 사항을 감지하고 파이프라인을 시작합니다.
- **젠킨스 <-> 도커**: 젠킨스는 도커를 사용하여 애플리케이션의 빌드를 자동화하고, 빌드된 이미지를 도커 허브에 저장합니다.
- **젠킨스 <-> 쿠버네티스**: 젠킨스는 쿠버네티스 클러스터와의 연결을 위해 SSH를 사용하여 디플로이먼트를 적용합니다.
- **쿠버네티스**: 클러스터 내부에서는 마스터 서버가 디플로이먼트를 관리하고, 워커 서버들이 실제로 애플리케이션을 호스팅합니다.
<br><br><br><br>




### CI/CD 시나리오 🎬
---
1. **개발자의 코드 푸시**
    - 개발자가 새로운 코드를 깃허브에 푸시하면 이벤트가 트리거됩니다.
      
2. **젠킨스 CI/CD 파이프라인**
    - 젠킨스가 깃허브 푸시 이벤트를 감지하고 파이프라인이 시작됩니다.

    - 젠킨스 파이프라인이 다음 단계들을 처리합니다.
        1. **깃허브 클론**: 젠킨스가 깃허브로부터 최신 코드를 클론합니다. <br><br>
        2. **빌드**: 클론된 코드를 기반으로 각각의 빌드 작업을 수행합니다. 이 과정에서 도커 이미지를 생성합니다. <br><br>
           - 백엔드 빌드 : `./gradlew bootJar`를 통해 빌드합니다. <br><br>
           - 프론트엔드 빌드 : 젠킨스가 node.js의 환경에서 npm install로 npm 설치 후, `npm run build`로 빌드합니다. <br><br>
        3. **도커 빌드**: 빌드가 완료된 후, 젠킨스는 `Dockerfile`을 기반으로 백엔드와 프론트엔드의 Docker 이미지를 생성합니다. <br><br>
        4. **도커 허브 푸시**: 젠킨스가 도커에 로그인 한 후 $BUILD_ID변수를 태그로 사용하여, 빌드된 도커 이미지를 도커 허브에 푸시합니다.
           
3. **쿠버네티스 배포**
    - 젠킨스가 빌드 완료 후, 각 파이프라인은 `frontend-deployment-blue.yml`, `frontend-deployment-green.yml`, `backend-deployment-green.yml`, `backend-deployment-green.yml`파일을 기반으로 SSH를 통해 쿠버네티스 마스터 서버에 접근하여 디플로이먼트를 만듭니다.
    - 디플로이먼트는 기존 버전을 유지하면서 새로운 버전을 배포합니다. 여기서 **블루-그린 배포** 방식을 사용하여, 새로운 버전이 문제없이 작동하는지 확인한 후 트래픽을 전환합니다.

4. **블루/그린 배포 시나리오**
   - **코드 버전 업데이트 및 새로운 컨테이너 생성**:
    	1. 백엔드와 프론트엔드 코드의 새로운 버전이 깃허브에 푸시되면, 젠킨스 파이프라인이 시작됩니다.
    	2. 젠킨스는 해당 코드를 빌드하여 새로운 도커 이미지를 생성하고, 이를 도커 허브에 푸시합니다.
 
    -  **블루 디플로이먼트 업데이트 및 파드 스케일 조정**:
    	1. 홀수 번째 배포라면 블루 디플로이먼트를 선택합니다. 젠킨스 파이프라인은 블루 디플로이먼트의 컨테이너 이미지를 새로운 버전으로 업데이트합니다.
    	2. 이때 블루 디플로이먼트에 속한 파드의 수를 2로 스케일링하여 트래픽을 처리할 준비를 합니다.
 
    -  **블루 파드 상태 확인 및 서비스 라벨 변경**:
    	1. 새로운 블루 파드가 정상적으로 실행되는지 확인합니다. 이는 `rollout`과 `wait`를 통한 `timeout` 설정을 통해 자동으로 이루어질 수 있으며, 문제가 없을 경우 다음 단계로 진행합니다.
    	2. 블루 파드가 정상적으로 작동하면, 서비스의 라벨을 변경하여 트래픽이 이전의 그린 파드에서 새로운 블루 파드로 전환되도록 합니다.
    
    -  **구버전 그린 디플로이먼트의 파드 스케일 조정**:
    	1. 블루 파드로의 트래픽 전환이 완료된 후, 이전 버전의 그린 디플로이먼트 파드의 스케일을 0으로 줄여 더 이상 사용되지 않도록 합니다.
    	2. 이는 구버전의 애플리케이션을 완전히 종료시키는 과정으로, 필요 시 롤백할 수 있도록 설정할 수도 있습니다.

---
<br><br><br><br>




### Blue/Green 배포 방식 📦

		블루그린 배포 방식은 안정성과 가용성이 중요한 환경에서 선호됩니다.
		특히 무중단 배포와 빠른 롤백이 중요한 경우 블루그린 배포 방식이 매우 좋을 것으로 예상되고, 인사관리 서비스에서도 블루그린 배포 방식을
		사용하면 고객이 원하는 안정성과 신속한 업데이트를 동시에 제공할 수 있기에 이 배포 방식을 선택했습니다.
<br>

**❓인사관리 서비스의 관점과 다른 배포 방식과의 비교에서 블루/그린을 선택한 이유❓** <br> 

인사관리 서비스는 고객의 요구사항을 반영하여 직원 정보, 급여, 근태 관리 등의 데이터를 관리하고 제공하는데, 이 서비스의 관점에서 저희가 블루그린 배포 방식을 선택한 이유는 다음과 같습니다.

1. 직관적이고 안정적인 서비스 업데이트: <br> 인사관리 서비스는 사용자 인터페이스와 기능이 변화할 때, 사용자들이 혼란 없이 새롭게 반영된 기능을 직관적으로 인식할 수 있어야 합니다. 블루그린 배포 방식을 사용하면, 새로운 버전이 안정적으로 배포된 후 트래픽이 전환되므로, 사용자에게는 무중단으로 새로운 기능이 제공됩니다.

2. 신속한 롤백 가능성: <br> 만약 새로운 버전에서 문제가 발생하더라도, 블루그린 배포 방식은 빠르고 안전한 롤백을 가능하게 합니다. 기존의 그린 버전을 유지하고 있기 때문에, 문제가 발생할 경우 즉시 구버전으로 전환하여 서비스 연속성을 유지할 수 있습니다.

3. 테스트 환경과 동일한 프로덕션 환경: <br> 블루그린 배포는 프로덕션 환경에서 새로운 버전을 실제 트래픽 없이 테스트할 수 있기 때문에, 사전에 모든 환경에서 동일한 조건으로 테스트가 가능합니다. 이는 카나리 배포처럼 일부 트래픽만을 사용하는 테스트 방식보다 안전합니다.

4. 변경 영향 최소화: <br> 블루그린 배포는 전체 시스템에 걸친 변경을 한 번에 적용하므로, 점진적인 업데이트 방식에 비해 변경의 영향을 더 명확하게 파악할 수 있습니다. 따라서 배포 시 발생할 수 있는 문제를 더 쉽게 관리할 수 있습니다. 기존 서비스의 가용성을 유지하면서 새로운 버전을 배포할 수 있어서 롤링 업데이트와 같은 방식이 배포 도중 잠재적인 중단이나 성능 저하를 초래할 수 있는 것과 대비됩니다.

<br><br><br><br><br>



# 💡 CI/CD 테스트 및 결과
<!--예시 [시연영상](https://youtu.be/rzBV5B_kKbU)-->
### 백엔드 Blue/Green 배포
![백엔드 배포](https://github.com/user-attachments/assets/e42db20c-8a54-433f-85e6-bc4857d2e7cf)
<br>
➡️백엔드(프론트) 버전을 바꾸고 깃에 푸시 
➡️ 젠킨스 파이프라인이 작동 
➡️ 쿠버네티스에서 백엔드파드가 자동으로 새로 생성되는거 확인 블루<->그린
➡️ 바뀐 스프링 서버 버전 확인
<br>

### 프론트엔트 Blue/Green 배포
https://youtu.be/Oh7cYU5cf8E
<br>
➡️프론트엔드를 수정하고 깃에 푸시
➡️ 젠킨스 파이프라인이 작동 
➡️ 쿠버네티스에서 프론트엔드파드가 자동으로 새로 생성되는거 확인 블루<->그린
➡️ 바뀐 화면 글씨 확인

<br><br><br><br><br>


