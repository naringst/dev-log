
# 정의
- 웹 상의 수많은 서버의 흐름을 균형있게 흘려보내는 데에 중추적인 역할
- 하나의 서버로 traffic이 몰리는 병목현상(bottleneck) 방지
- Traffic의 흐름을 Unhealthy instance -> healthy instance로
	- ec2 인스턴스가 갑자기 셧다운이 생기거나 시간초과가 생기는 경우 unhealthy 해진다. 
	- 이때 ELB가 건강한 인스턴스로 트래픽을 보내준다.


# 종류
## 1. Application Load Balancer
- OSI Layer7(application layer)에서 작동
- HTTP, HTTPS와 같은 traffic의 load balancing에 가장 적합
- 라우팅 설정이 별도로 존재. 고급 request 라우팅 설정을 통해 특정서버로 request 보낼 수 있음.


## 2. Network Load Balancer
- OSI Layer4(transport layer)에서 작동. 
- 매우 빠른 속도를 자랑하며 Production 환경에서 종종 쓰임.
- 극도의 performance가 요구되는 TCP 트래픽에서 적합. (TCP 트래픽 정리에 적합)
- 초당 수백만개의 request를 아주 미세한 delay로 처리 가능.
- 구글, 네이버와 같은 큰 서버에서 적합.

## 3. Classic Load Balancer
- 현재 legacy로 간주.
- Layer 7 + Layer 4 라우팅 기능을 한 번에 지원.

# 에러
- 어플리케이션이나 서버가 응답을 받지 못하는 경우 504 에러를 발생시킴.
- 이때 주로 web server layer, db layer에서 해결 가능


# X-Forwarded-For
- 152.12.3.225(Public IP 주소) -> dns 요청 -> elb 도달 -> elb는 10.0.0.23이라는 프라이빗 어드레스로 인식 -> ec2 인스턴스로 해당 요청 전송 
- 이때 EC2는 private IP 주소밖에 알 수 없다. 따라서 출처를 알 수 없다. 
- 이때 X-Forwarded-For 헤더를 통해 원래 public ip 주소를 찾아볼 수 있다.
