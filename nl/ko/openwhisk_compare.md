---

copyright:
  years: 2016, 2018
lastupdated: "2018-05-31"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# FaaS(Function as a Service) 비교
{: #openwhisk_faas_compared}

{{site.data.keyword.openwhisk}}는 확장성이 뛰어난 서버리스 환경에 OpenWhisk를 제공합니다. {{site.data.keyword.openwhisk_short}}의 서버리스 아키텍처 및 비용 효율적 컴퓨팅과 다른 아키텍처 모델을 비교할 수 있습니다.
{: shortdesc}

## OpenWhisk 아키텍처의 비교
{: #architecture_comparison}

다음 OpenWhisk 아키텍처가 비교 대상입니다.

1. [{{site.data.keyword.openwhisk_short}}](https://console.bluemix.net/openwhisk)의 **FaaS(Function as a Service)**. IBM은 관리 OpenWhisk를 제공하는 유일한 공급업체입니다. FaaS 플랫폼을 사용하는 서버리스 프로그래밍 모델에 대한 소개는 [Martin Fowler의 블로그](https://martinfowler.com/articles/serverless.html)에 있으며, 서버리스 디자인의 OpenWhisk를 실행하기 위한 [유스 케이스](./openwhisk_use_cases.html)를 볼 수 있습니다.

2. OpenWhisk RYO(Roll Your Own)가 포함된 **IaaS(Infrastructure as a Service)**. Apache Incubation Project에서 OpenWhisk를 다운로드하여 [{{site.data.keyword.Bluemix_notm}} IaaS](https://console.ng.bluemix.net/catalog/?category=devices)에서 실행할 수 있습니다.

3. 관리 애플리케이션 런타임인 **PaaS(Platform as a Service)**. {{site.data.keyword.Bluemix_notm}} Foundry 구현에 의해 관리되는 [Liberty for Java](https://console.ng.bluemix.net/catalog/starters/liberty-for-java) 런타임이 좋은 예입니다.

4. 관리 컨테이너 환경인 **CaaS(Container as a Service)**. [{{site.data.keyword.containerlong_notm}}](/docs/containers/container_index.html#container_index)가 좋은 예입니다.

5. Java EE 런타임이 포함된 **IaaS(Infrastructure as a Service)**. [{{site.data.keyword.Bluemix_notm}}의 WebSphere Application Server VM](https://console.ng.bluemix.net/catalog/services/websphere-application-server)이 좋은 예입니다.

다음 표에서는 애플리케이션을 작성하고 운영하는 개발자의 관점에서 각 아키텍처 요소를 비교합니다.


|주제 | (1) {{site.data.keyword.openwhisk_short}}의 FaaS | (2) OpenWhisk RYO의 IaaS |(3) PaaS |(4) CaaS | (5) Java EE의 IaaS |
| --- | --- | --- | --- | --- | --- |
|	애플리케이션 단위	|	단일 함수(일반적으로 JavaScript, Swift 또는 Docker 컨테이너의 소형 코드 블록) - 1Kb 미만일 수 있지만 더 클 수 있습니다. 일반적으로 수 Kb를 초과하지 않습니다.	|	열 (1)과 동일함	|	사용되는 런타임에 따라 다릅니다. 일반적으로 상대적으로 큰 EAR 또는 WAR 파일 또는 기타 언어 특정 애플리케이션 번들 - 번들에 많은 서비스가 포함된 Kb 또는 심지어는 Mb 단위의 크기지만, 단일 서비스처럼 작을 수도 있습니다.	|	Docker 컨테이너는 배치 단위입니다.	|	EAR 또는 WAR 파일 또는 기타 종속 항목이 포함된 앱 서버의 VM - 일반적인 크기는 Gb 단위입니다.	|
|	리소스 풋프린트	|	일반 사용자가 메모리, CPU 또는 기타 리소스의 비용을 지불하지 않거나 이에 대해 신경쓰지 않습니다. 액션에 일부 풋프린트가 있지만 사용자는 이에 대해 염려할 필요가 없습니다. |	높음. 일반 사용자가 우선 IaaS 환경을 프로비저닝해야 하며, 이 경우에만 그 위에 OpenWhisk를 설치하고 구성할 수 있습니다.	|	소형. 일반 사용자는 앱 실행을 위한 메모리와 CPU의 비용을 지불하지만, 실행 중이 아닌 앱에 대해서는 비용을 지불하지 않습니다.	|	소형에서 중형	|	높음. 일반 사용자는 앱이 실행될 때 디스크 스토리지, 메모리, CPU 및 기타 가능한 컴포넌트에 대해 비용을 지불해야 합니다. 중지된 경우에는 스토리지 비용만 발생합니다.	|
|	설치 및 설정	|	필요하지 않음	|	어려움 - 모두 일반 사용자가 수행함	|	필요하지 않음	|	중간 - 하드웨어, 네트워킹, OS, 컨테이너 관리 도구는 CaaSs 공급업체가 제공하며 이미지, 연결성 및 인스턴스는 일반 사용자가 제공함	|	어려움 - 하드웨어, 네트워킹, OS 및 초기 Java EE 설치는 공급업체가 제공하며 추가 구성, 클러스터링 및 스케일링은 일반 사용자가 제공함	|
|	프로비저닝 시간	|	밀리초	|	열 (4) 및 (5) 참조	|	분	|	분	|	시간	|
|	지속적 관리	|	없음	|	어려움	|	없음	|	중간	|	어려움	|
|	탄력적 스케일링	|	각 액션은 항상 로드에 따라 즉시 기본적으로 스케일링됩니다. 사전에 VM 또는 기타 리소스를 프로비저닝할 필요가 없습니다.	|	제공되지 않음 - 일반 사용자가 IaaS의 컴퓨팅 용량을 제공하고 VM의 스케일링을 관리해야 합니다. 일단 VM이 스케일링되면 OpenWhisk가 액션을 자동으로 스케일링하지만, 리소스는 사전에 이미 프로비저닝되어 있어야 합니다. |	자동적이지만 느린 스케일링입니다. 로드가 증가하는 동안 사용자는 수 분 정도 스케일링 액션이 완료될 때까지 대기해야 할 수 있습니다. 자동 스케일링에서는 신중한 튜닝이 필요합니다.	|	자동적이지만 느린 스케일링입니다. 로드가 증가하는 동안 사용자는 수 분 정도 스케일링 액션이 완료될 때까지 대기해야 할 수 있습니다. 자동 스케일링에서는 신중한 튜닝이 필요합니다.	|	제공되지 않음	|
|	용량 계획	|	필요하지 않습니다. FaaS가 자동으로 필요한 만큼의 용량을 제공합니다.	|	사전에 충분한 용량을 프로비저닝하거나 이를 스크립팅해야 합니다.	|	일부 용량 계획은 필요하지만 일부 자동 용량 늘리기가 제공됩니다.	|	일부 용량 계획은 필요하지만 일부 자동 용량 늘리기가 제공됩니다.	|	최대 워크로드를 처리하기 위해 정적으로 프로비저닝된 충분한 용량을 제공해야 합니다.	|
|	지속적 연결 및 상태	|	제한됨 - 컨테이너 캐싱의 경우를 제외하면 지속적 연결을 유지할 수 없습니다. 일반적으로 상태는 외부 리소스에서 유지되어야 합니다.	|	열 (1)과 동일함	|	지원됨 - 장시간 오픈 소켓 또는 연결을 유지할 수 있으며 호출 간에 메모리에 상태를 저장할 수 있음	|	지원됨 - 장시간 오픈 소켓 또는 연결을 유지할 수 있으며 호출 간에 메모리에 상태를 저장할 수 있음	|	지원됨 - 장시간 오픈 소켓 또는 연결을 유지할 수 있으며 호출 간에 메모리에 상태를 저장할 수 있음	|
|	유지보수	|	없음 - 전체 스택을 IBM이 관리합니다.	|	중요 - 대상 환경에 따라 사용자는 하드웨어, 네트워킹, OS, 스토리지, DB를 프로비저닝하고 OpenWhisk 등을 설치 및 유지보수해야 합니다.	|	없음 - 전체 스택을 공급업체가 관리합니다.	|	중요 - 사용자가 사용자 정의 이미지를 작성하고 유지보수해야 하며 컨테이너 배치 및 관리, 컨테이너 간의 연결 등을 수행해야 합니다.	|	중요 - 사용자가 VM을 할당하고 Java EE 서버를 개별적으로 관리 및 스케일링해야 합니다.	|
|	고가용성(HA) 및 재해 복구(DR)	|	기본 제공됨/추가 비용 없음	|	RYO(Roll Your Own) 	|	추가 비용을 지불하고 사용 가능함	|	장애가 발생한 컨테이너의 자동 재시작이 가능함	|	추가 비용을 지불하고 사용 가능함, 반자동 VM의 자동 장애 복구가 가능함	|
|	보안	|	공급업체에서 제공	|	RYO(Roll Your Own)	|	RYO 및 공급업체 제공이 혼합됨	|	RYO 및 공급업체 제공이 혼합됨	|	RYO(Roll Your Own)	|
|	개발자 속도	|	최고	|	최고	|	최고	|	보통	|	느림	|
|	리소스 활용도(계속 비용을 지불해야 하는 유휴 리소스)	|	요청 시에만 호출되므로 유휴 리소스가 없습니다. 워크로드가 없으면 비용 또는 리소스 할당이 발생하지 않습니다.	|	이 옵션이 IaaS 또는 CaaS를 사용하므로 열 (4) 및 (5)에서와 유사한 고려사항이 적용됨	|	일부 리소스가 유휴 상태일 수 있으며, Auto-Scaling은 유휴 리소스를 제거하는 데 도움이 됩니다. 얼마간의 실행 중인 인스턴스가 항상 존재해야 하며, 해당 용량의 50%  미만으로 사용될 가능성이 높습니다. 중지된 인스턴스는 비용을 유발하지 않습니다.	|	열 (3)과 유사함	|	일부 리소스가 유휴 상태일 수 있지만, Auto-Scaling은 지원되지 않습니다. 얼마간의 실행 중인 인스턴스가 항상 존재해야 하며, 해당 용량의 50%  미만으로 사용될 가능성이 높습니다. 중지된 인스턴스가 스토리지 비용을 유발할 수 있습니다.	|
|	완성도	|	조기 완성도	|	조기 완성도	|	조기 완성도	|	보통의 완성도	|	고도의 완성도	|
|	리소스 한계	|	[일부 한계가 존재함](./openwhisk_reference.html#openwhisk_syslimits)	|	할당된 리소스에 따라 다름	|	없음	|	없음	|	없음	|
|	드물게 사용되는 서비스에 대한 대기 시간	|	드문 요청은 초기에 수 초의 응답 시간을 나타내지만, 후속 요청인 경우에는 ms 범위를 유지함	|	종속	|	낮음	|	낮음	|	낮음 - 시스템의 리소스가 충분하다고 가정함	|
|	애플리케이션의 스윗 스팟 유형	|	이벤트 처리, IoT, 모바일 백엔드, 마이크로서비스. 모놀리식 애플리케이션의 경우에는 명백히 아닙니다. [유스 케이스](./openwhisk_use_cases.html)를 참조하십시오.	|	열 (1)과 동일하지만, 사용자가 비-IBM 클라우드 또는 온프레미스에서 실행하고자 하는 경우.	|	24x7 워크로드 로드가 있는 웹 애플리케이션 및 장시간 동안 열린 연결을 유지해야 하는 stateful 서비스. 마이크로서비스 또는 모놀리식 애플리케이션의 실행에 사용될 수 있습니다.	|	마이크로서비스 애플리케이션에 이상적입니다.	|	온프레미스에서 클라우드로 마이그레이션된 전통적인 엔터프라이즈 애플리케이션. 모놀리식 애플리케이션에 이상적입니다.	|
|	입자성 및 비용 청구	|	[100밀리초의 블록당](https://console.ng.bluemix.net/openwhisk/learn/pricing)	|	구현에 종속됨 - IaaS 또는 CaaS가 사용되는 경우, 유사한 고려사항이 적용됨 - 열 (4) 및 (5) 참조	|	리소스 번들(CPU + 메모리 + 일부 디스크 공간)에 대해 일반적으로 시간당(드물게 분당) 비용 청구됨	|	열 (3)과 유사함	|	열 (3)과 유사함	|
|	총소유비용(TCO)	|	스윗 스팟의 경우, 애플리케이션은 대체 애플리케이션 미만의 크기 배열로 비용이 청구될 수 있습니다. 리소스가 자동으로 스케일링되므로 초과 프로비저닝이 발생하지 않습니다.	|	클라우드 배치의 경우, 이는 OpenWhisk FaaS보다 비쌀 수 있지만 온프레미스 배치는 전통적인 아키텍처보다 비용이 저렴할 수 있습니다.	|	상대적으로 낮음 - 사용자가 리소스를 프로비저닝하거나 관리할 필요가 없으며 애플리케이션 개발에만 집중할 수 있습니다. 서버리스와 비교하여 일정 레벨의 초과 프로비저닝	|	적절 - 사용자가 컨테이너와 애플리케이션을 프로비저닝하고 관리해야 하며 서버리스 또는 PaaS와 비교하여 일정 레벨의 초과 프로비저닝이 나타날 수 있습니다.	|	상대적으로 높음 - 클라우드 고유 모델로 레거시 애플리케이션의 마이그레이션은 엄청나게 고가일 수 있음을 고려하십시오. 이는 해당 앱에 대한 실행 가능한 경제적 선택사항일 수 있습니다.	|

## 비용 고려사항
{: #cost_considerations}

테스트, 스테이징, 로드 테스트 및 기타 환경의 인프라에 비용이 많이 들 수 있습니다. 인프라 설정에는 시간이 걸리며, 인프라는 대개 일주일 내내 종일 작동하므로 종종 충분히 활용되지 않고 많은 용량을 사용합니다. 서버리스 아키텍처를 사용하면 임의 수의 환경에 대한 비용이 정의된 환경 수 대신 로드를 기준으로 생성됩니다.
{: shortdesc}

서버리스 애플리케이션에 대한 비용을 예측하기 위해 [가격 책정 계산기 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.bluemix.net/openwhisk/learn/pricing)를 사용할 수 있습니다.

### 무제한 용량
{: #limitless_capacity}

기존 아키텍처에서 각 서비스는 할당된 용량을 사용하며 사용량에 대한 비용이 사용자에게 청구됩니다. {{site.data.keyword.openwhisk_short}}의 서버리스 아키텍처는 마이크로서비스 아키텍처의 세분화에 대한 제한조건을 줄입니다.

사용하지 않을 경우 {{site.data.keyword.openwhisk_short}}에 비용이 들지 않습니다. 코드는 HTTP 호출, 데이터베이스 상태 변경 또는 코드 실행을 트리거하는 기타 유형의 이벤트가 있을 때 실행됩니다. 해당 VM이 유용한 작업을 수행 중인지 여부와 무관하게 VM 활용 시간당 비용이 청구되지 않고 실행 시간(밀리초)에 따라 사용자에게 비용이 청구됩니다(가장 가까운 100ms로 반올림됨). 이벤트가 이용되고 환경 수를 기준으로 하지 않을 때만 비용을 지불하므로 앱을 100, 1,000 또는 심지어 마이크로서비스로 나눌 수 있습니다.

### 임의 지역에서 액션 실행
{: #actions_region}

기존 아키텍처에서 코드는 실행될 각 지역에서 실행 중이어야 하고 이 지역의 인프라에 대한 비용도 지불해야 합니다. {{site.data.keyword.openwhisk_short}}의 경우 액션을 배치하고 추가 비용 없이 임의 지역에서 실행할 수 있습니다. 기존 비용 제한 없이 코드의 가용성 및 탄력성을 높일 수 있습니다.

### 디자인에 의한 중복성
{: #redundancy_design}

기존 아키텍처에서는 앱에 중복성이 있어야 합니다. {{site.data.keyword.openwhisk_short}}에서는 서버리스 앱이 Stateless하고 디자인에 의한 요청 이벤트이기 때문에 프로세스가 고가용성(HA)이 아니어도 됩니다. 명시적으로 중복성을 작성할 필요가 없으므로 서버리스 앱의 Stateless 네이처로 인해 인프라 비용을 크게 줄일 수 있습니다.
