# AmneziaWG Cross-Platform Starter Stack

아래 파일은 **크로스플랫폼(Windows/macOS/Linux/Android/iOS) 클라이언트 + Linux 릴레이 2단** 운영을 시작하기 위한 최소 템플릿입니다.

## 포함 내용

- `ansible/inventory.ini.example`: Relay 노드 인벤토리 예시
- `ansible/group_vars/all.yml`: 공통 변수(인터페이스/포트/DNS/egress)
- `ansible/playbook.yml`: 공통 베이스라인(패키지, 포워딩, 기본 방화벽 정책)

## 빠른 시작

1. 인벤토리 복사
   - `cp ansible/inventory.ini.example ansible/inventory.ini`
2. 변수 수정
   - `ansible/group_vars/all.yml`에서 인터페이스/포트/DNS/egress NIC 수정
3. 점검 실행
   - `ansible-playbook -i ansible/inventory.ini ansible/playbook.yml --check`
4. 실제 적용
   - `ansible-playbook -i ansible/inventory.ini ansible/playbook.yml`

## 완료 기준 (Done Checklist)

아래 항목이 모두 충족되면 "작업 완료"로 볼 수 있습니다.

- [ ] Relay-1, Relay-2 서버에 플레이북 적용 완료
- [ ] 클라이언트(최소 2개 OS)에서 터널 연결/재연결 확인
- [ ] DNS leak / IPv6 leak 테스트 통과
- [ ] 터널 끊김 시 Kill Switch 동작 확인
- [ ] Relay-2 egress IP가 의도한 IP로만 노출되는지 확인
- [ ] 로그 보관 정책(최소화) 및 키 관리 정책(SOPS/Vault) 적용

## 주의

- 본 템플릿은 **운영 기초 자동화** 목적이며, 실제 AmneziaWG 피어/키 배포는 별도 비밀관리(SOPS/Vault 등)로 분리하세요.
- `nftables` 규칙은 환경별로 조정이 필요합니다.
