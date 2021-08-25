# HyperFrameOE-WildFly

# 설치 방법
다음 tar 파일의 압축 해제
tar -zxvf wildfly-preview-22.0.0.Final.tar.gz

# 파일 기동 

${WILDFLY_HOME}/bin > ./standalone.sh

http:// ip:8080 주소로 접속하여 WEB UI 화면을 확인

# 종료 

${WILDFLY_HOME}/bin > jboss-cli.sh --controller=IP:9990 --connect command=:shutdown 명령어로 종료

controller의 IP는 standalone.xml에서 설정한 management IP

# 실행 / 종료 명령어


실행
${WILDFLY_HOME}/bin > ./standalone.sh

종료
${WILDFLY_HOME}/bin > jboss-cli.sh --controller=IP:9990 --connect command=:shutdown

# 디렉토리 구조

wildfly
    ├── applicient	 	<----------------------- Application 클라이언트 컨테이너에서 사용하는 파일 담당
    ├── bin		       	<----------------------- WildFly 파일의 기동 및 종료 등의 shell 경로
    ├── docs		     	<----------------------- 라이선스 파일, xml스키마 정의 파일, 예제 구성 파일 및 기타 문서 담당
    ├── domain   	   	<----------------------- domain 모드에서 사용하는 파일 등을 담당 ( *domain 모드 : 다중 서버를 관리할 수 있는 모드 )
    ├── modules		   	<----------------------- 서버에서 사용하는 클래스 라이브러리
    ├── standalone	 	<----------------------- standalone 모드에서 사용하는 파일 등을 담당 ( *standalone 모드 : 단일 서버 인스턴스를 구성할 때 사용하는 모드 )
    └── welcome-content	
standalone 디렉토리 구조
wildfly
    ├───── standalone	
    |         └── configuration 	
    ├── data			<----------------------- standalone server 실행 시 생성되는 파일들을 보관
    ├── deployments		<----------------------- App 배포 디렉토리 
    └── lib			<----------------------- 설치된 라이브러리가 위치 
   	 └── tmp		<----------------------- 임시 파일 위치
domain 디렉토리 구조
wildfly
    ├── domain	
    ├── configuration
   	     └── tmp	

# 로그

${WILDFLY_HOME}/standalone/log/server.log : 서버가 시작된 이후 모든 로그 메시지가 기록되는 파일

# 로그 경로 변경

${WILDFLY_HOME}/bin/standalone.sh에

export JAVA_OPTS=" $JAVA_OPTS -Djboss.server.log.dir=경로"

위와 같이 로그 디렉터리를 변경하는 옵션 추가

# 환경 설정 파일

${WILDFLY_HOME}/standalone/configuration/standalone.xml

ip 변경
외부 접근 허용 가능하게 할 시
  <!--<inet-address value="${jboss.bind.address:192.168.3.87}"/> -->    해당 부분 주석처리 후

  <any-address/> 추가
port 번호 변경
     <socket-binding-group name="standard-sockets" default-interface="public" port-offset="${jboss.socket.binding.port-offset:0}">
       
         <socket-binding name="ajp" port="${jboss.ajp.port:8009}"/>
       
         <socket-binding name="http" port="${jboss.http.port:8080}"/>
       
         <socket-binding name="https" port="${jboss.https.port:8443}"/>
       
         <socket-binding name="management-http" interface="management" port="${jboss.management.http.port:9990}"/>
       
         <socket-binding name="management-https" interface="management" port="${jboss.management.https.port:9993}"/>
       
...

# 버전 확인
Wildfly : ${WILDFLY-HOME}/bin : $ ./standalone.sh --version

Java : $java -version

# 라이센스

# 버전 이력

wildfly-preview-22.0.0.Final
