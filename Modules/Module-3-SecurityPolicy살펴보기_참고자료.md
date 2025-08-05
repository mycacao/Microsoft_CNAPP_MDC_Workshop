# 참고 내용


## MDC 기능을 off 하도, 하루 지나면 자동으로 on 됨

애저포탈에서 '정책' > '할당' 들어 가신후에
'MCAPSGov Deploy and Modify Policies' 이니셔티브 검색하셔서 해당 이니셔티브 들어가서

<img width="1829" height="455" alt="image" src="https://github.com/user-attachments/assets/a5b9bdbf-7327-479d-8465-df07b6bb2bd6" />

이니셔티브에 포함된 정책정의들을 볼 수 있는데 항목에 기본 효과 보시면 'DeployIfNotExists'로 정책이 선언되어있어서 자동으로 서버 Defender가 비활성화되어있다면 활성화로 변경됩니다. 

<img width="1843" height="591" alt="image" src="https://github.com/user-attachments/assets/6e857e5f-c744-48cd-9bf7-507c448aecce" />

그래서 할당 편집으로 들어가셔서 '서버를 사용 설정하도록 Azure Defender 구성' 정책의 기본 효과를 'DeployIfNotExists'에서 'AuditIfNotExists' 감사모드로 변경해주시면 자동으로 수정안되실거에요
