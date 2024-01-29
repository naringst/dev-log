EC2 인스턴스에 붙는 가상 하드 디스크.

스토리지 볼륨을 생성하여 EC2 인스턴스에 부착되어 사용되어진다. 컴퓨터를 새로 사면 하드 디스크가 딸려 나오는 것과 같음.
EBS는 디스크 볼륨 위에 파일 시스템이 생성된다. 따라서 EC2 인스턴스에 접근이 가능하게 되고, 파일을 로컬 디스크로 작업도 가능.
EBS는 Availability zone을 설정해줘야 한다.  
하나의 regeion 안에 여러개의 availability zone 존재 가능. 중심부로부터 그의 복사본들이 az로 뿌려지며 유사 시 한쪽 서버가 망가지거나 셧다운 됐을 경우 az라는 백업을 통해 서비스 제공을 가능하게 해주는 일종의 디제스트 리커버리.

- 저장 공간이 생성되어지며 EC2 인스턴스에 부착된다.
- 디스크 볼륨 위에 FileSystem이 생성된다.
- EBS는 특정 Availability zone에 생성된다.


## EBS 볼륨 타입
### 1. SSD 
- General Purpose SSD(GP2) : 
	- 최대 10K IOPS를 지원하며, 1GB당 3IOPS 속도가 나온다.
	- 속도가 매우 빠르고 SSD 중에서 가장 보편적으로 사용됨.
- Provisioned IOPS SSD(I01) : 
	- 극도의 I/O률 을 요구하는(매우 큰 db 관리 등) 환경에서 주로 사용됨. 10K 이상의 IOPS를 지원.
	- 아주 방대한 양의 데이터 처리 할 때 필요.
	-  입출력 빈번하고 그 양이 방대할 경우 뛰어난 효능 자랑
	- 그만큼 가격 높음.

### 2. Magnetic/HDD군
- Throughput Optimized HDD(ST1) 
	- 빅데이터 Datawarehouse, Log 프로세싱 시 주로 사용(boot volume으로 사용 불가)
	- 빅데이터 보관, 컴퓨터 로그 파일 보관하고 읽어들일시 추천
	- boot volume으로 사용 불가 == window처럼 운영체제를 가지고 있을 수 없다.
- CDD HDD(SC1) 
	-  파일 서버와 같이 드문 volume 접근 시 주로 사용.
	- 오래 보관해도 괜찮은 데이터들을 처리할 때 사용
	-  boot volume으로 사용 불가하나 비용 저렴
- Magnetic(St\
- 
- andard)
	- 디스크 1GB당 가장 싼 비용 
	- Boot volume으로 가능