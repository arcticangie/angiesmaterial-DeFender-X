# 📊 DeFenderX 기간별 리포트 기획안

**문서 버전**: 1.0  
**최초 작성일**: 2024-12-09  
**프로젝트명**: DefenderX-Client-AI-Reports  
**목적**: 월간/주간/일간 보안 리포트 구조 및 기능 정의  
**대상**: 프론트엔드 개발자, 보안 담당자, 경영진 

---

## 0. 프로젝트 개요 ⭐

### 0.1 기본 정보

| 항목 | 내용 |
|------|------|
| **프로젝트명** | DeFenderX-Client: AI Report |
| **버전** | 0.1.0 |
| **패키지 매니저** | pnpm 10.15.0+ |
| **기본 언어** | 한국어 (ko) |
| **지원 언어** | 한국어(ko), 영어(en), 일본어(ja) |

### 0.2 핵심 프레임워크

| 라이브러리 | 버전 | 용도 |
|-----------|------|------|
| Next.js | 15.5.7 | React 프레임워크 (App Router) |
| React | 19.1.2 | UI 라이브러리 |
| React DOM | 19.1.2 | React 렌더링 엔진 |
| TypeScript | 5.x | 타입 시스템 |

### 0.3 UI/UX 라이브러리

#### 스타일링

| 라이브러리 | 버전 | 용도 |
|-----------|------|------|
| Tailwind CSS | 4.x | 유틸리티 CSS 프레임워크 |
| shadcn/ui | - | Radix UI + Tailwind 기반 디자인 시스템 |
| tw-animate-css | 1.3.7 | Tailwind 애니메이션 확장 |
| class-variance-authority | 0.7.1 | 컴포넌트 변형 관리 |
| clsx | 2.1.1 | 조건부 클래스명 유틸 |
| tailwind-merge | 3.3.1 | Tailwind 클래스 병합 |

#### UI 컴포넌트 (Radix UI 기반 shadcn/ui)

| 라이브러리 | 버전 | 설명 |
|-----------|------|------|
| @radix-ui/react-alert-dialog | 1.1.15 | 알림 대화상자 |
| @radix-ui/react-avatar | 1.1.10 | 아바타 컴포넌트 |
| @radix-ui/react-checkbox | 1.3.3 | 체크박스 |
| @radix-ui/react-collapsible | 1.1.12 | 접기/펼치기 |
| @radix-ui/react-dialog | 1.1.15 | 모달 다이얼로그 |
| @radix-ui/react-dropdown-menu | 2.1.16 | 드롭다운 메뉴 |
| @radix-ui/react-label | 2.1.7 | 폼 레이블 |
| @radix-ui/react-popover | 1.1.15 | 팝오버 |
| @radix-ui/react-progress | 1.1.7 | 진행 표시 바 |
| @radix-ui/react-scroll-area | 1.2.10 | 커스텀 스크롤 영역 |
| @radix-ui/react-select | 2.2.6 | 셀렉트 박스 |
| @radix-ui/react-separator | 1.1.7 | 구분선 |
| @radix-ui/react-slot | 1.2.3 | 슬롯 패턴 유틸 |
| @radix-ui/react-tabs | 1.1.13 | 탭 컴포넌트 |
| @radix-ui/react-toast | 1.2.15 | 토스트 알림 |
| @radix-ui/react-toggle | 1.1.10 | 토글 스위치 |
| @radix-ui/react-toggle-group | 1.1.11 | 토글 그룹 |
| @radix-ui/react-tooltip | 1.2.8 | 툴팁 |

### 0.4 데이터 시각화

| 라이브러리 | 버전 | 용도 |
|-----------|------|------|
| chart.js | 4.5.0 | 차트 라이브러리 (Canvas 기반) |
| react-chartjs-2 | 5.3.1 | React용 Chart.js 래퍼 |
| recharts | 3.5.0 | React 선언적 차트 라이브러리 |
| @tanstack/react-table | 8.21.3 | 고급 테이블/데이터그리드 |

### 0.5 에디터 & 텍스트 처리

#### 리치 텍스트 에디터

| 라이브러리 | 버전 | 용도 |
|-----------|------|------|
| @blocknote/core | 0.42.0 | BlockNote 에디터 코어 |
| @blocknote/react | 0.42.0 | React 통합 |
| @blocknote/mantine | 0.42.0 | Mantine UI 스타일 |
| @blocknote/code-block | 0.42.0 | 코드 블록 지원 |

#### 마크다운

| 라이브러리 | 버전 | 용도 |
|-----------|------|------|
| react-markdown | 10.1.0 | 마크다운 렌더러 |
| remark-gfm | 4.0.1 | GitHub Flavored Markdown |
| rehype-raw | 7.0.0 | HTML in Markdown 지원 |

#### 텍스트 비교

| 라이브러리 | 버전 | 용도 |
|-----------|------|------|
| diff-match-patch | 1.0.5 | 텍스트 Diff 알고리즘 |
| react-diff-viewer-continued | 3.4.0 | React Diff 뷰어 컴포넌트 |

---

## 1. 리포트 공통 설계 원칙 📋

### 1.1 디자인 원칙

| 원칙 | 설명 |
|------|------|
| **컴포넌트 캡슐화** | 숫자로 구분되는 리포트 목차별로 컴포넌트 구성 후, 전체를 캡슐화하는 디자인 생성 |
| **웹/다운로드 구분** | 웹 리포트와 다운로드용 리포트를 별도 디자인으로 분리 |
| **미리보기 기능** | 다운로드 전 확인 가능한 `미리보기 (Preview)` 버튼 제공 |
| **테마 색상** | 블루(Blue) 및 네이비(Navy) 계열 |

### 1.2 담당자 조치 필드 규칙

| 항목 | 설명 |
|------|------|
| **필드 용도** | XDR 자동 차단 외 보안 담당자의 실제 조치 내용 기록 |
| **기본 상태** | 공란 (리포트 생성 시) |
| **편집 권한** | 리포트 생성자, 관리자 |
| **필수 요소** | 가이드 문구 포함 (직접 수정 안내) |

---

## 2. 리포트 유형별 비교 표 📊

| 항목 | 월간 | 주간 | 일간 |
|------|------|------|------|
| **섹션 수** | 9개 | 6개 | 5개 |
| **보고 주기** | 매월 1일 | 매주 월요일 | 매일 |
| **리포트 목적** | 경영진 보고, 보안 전략 수립, 감사 대응 | 보안 운영 흐름 파악 및 대응 전략 점검 | 실시간 위협 대응 및 일일 보안 상황 공유 |
| **리포트 대상** | CISO, CTO, 경영진, 감사팀 | 보안팀 리더, IT 운영 책임자 | 실무 보안 담당자, 운영 관리자 |
| **Incident 분석 대상** | Critical, High | Critical, High, Medium | Critical, High, Medium, Low (전체) |
| **호스트 위협 집계** | 최대 10개 | 최대 10개 | - |
| **CVE 위협 집계** | CVSS 9.0+ (최대 10개) | - | - |
| **규정 준수 여부** | ISMS-P, ISO27001, GDPR | - | - |

---

## 3. 월간 리포트 (Monthly Report) - 9개 섹션 

**보고 주기**: 매월 1일 자동 생성  
**보고 기간**: 전월 1일 ~ 말일  
**주요 목적**: 경영진 보고, 보안 전략 수립, 감사 대응  
**리포트 대상**: CISO, CTO, 경영진, 감사팀

| No | 섹션 제목 | 포함 내용 | 시각화 유형 | 비고 |
|----|----------|----------|------------|------|
| 1 | **월간 Incident Summary** | - Severity별 개수 (Critical/High/Medium/Low)<br>- 탐지 건 줄글 요약 | 요약 카드 + 텍스트 | JSON 기반 |
| 2 | **월간 탐지 이벤트 요약** | - Severity별 탐지 건수 (파이차트 + 표)<br>- Status별 비율 (파이차트 + 표) | 파이차트 (2개) + 표 | defenderxs |
| 3 | **고위험 탐지 유형** | - MITRE ATT&CK 기준 탐지 유형<br>- Alert별 탐지 설명 및 모듈<br>- 최대 10개 | 표 | JSON 기반 | 
| 4 | **이벤트 분포** | - Critical, High 건만 해당<br>- Detection time, Incident ID, Severity, Status, Description | 표 | JSON 기반 |
| 5 | **주요 Incident 분석** | - 탐지 명 (영문)<br>- Date, Host, Internal IP, User<br>- File/Network Artifacts (표)<br>- Incident Summary<br>- 공격 기법 (MITRE ATT&CK)<br>- 권장 조치 (AI 분석)<br>- 담당자 조치 (공란) | 카드 + 표 + 텍스트 | JSON 기반 + 생성 |
| 6 | **호스트별 위협 집계** | - 가장 많은 Incident 포함 Host<br>- 최대 10개 | 표 | 권장 | defenderxs |
| 7 | **CVEs 위협 집계** | - CVSS 점수 9.0+ 기준<br>- 가장 많은 호스트 포함 CVE<br>- 최대 10개 | 표 | 권장 | defenderxs |
| 8 | **규정 준수 여부** | - ISMS-P 준수 여부<br>- ISO27001 준수 여부<br>- GDPR 준수 여부<br>- AI 인시던트 분석 내역 참조 | 카드 (상태 표시) | AI 분석 통계 |
| 9 | **최종 권고** | - 보안 유지 상황 요약<br>- 우선 조치 사항 (긴급도별) | 텍스트 블록 | JSON 기반 분석 |

---

## 4. 주간 리포트 (Weekly Report) - 6개 섹션 

**보고 주기**: 매주 월요일 자동 생성  
**보고 기간**: 지난 7일 (월~일)  
**주요 목적**: 보안 운영 흐름 파악 및 대응 전략 점검  
**리포트 대상**: 보안팀 리더, IT 운영 책임자

| No | 섹션 제목 | 포함 내용 | 시각화 유형 | 비고 |
|----|----------|----------|------------|------|
| 1 | **주간 Incident Summary** | - Severity별 개수 (Critical/High/Medium/Low)<br>- 탐지 건 줄글 요약 | 요약 카드 + 텍스트 | JSON 기반 |
| 2 | **주간 탐지 이벤트 요약** | - **A.** 주간 이벤트 통계 (MITRE ATT&CK 탐지 유형)<br>- **B.** 요일별 Alert 개수 (막대 그래프 + 줄글 설명)<br>- **C.** Status별 비율 (파이차트)<br>- **D.** Severity별 주간 인시던트 통계 (표) | 막대 그래프 + 파이차트 + 표 | 인시던트 통계 기반 생성 |
| 3 | **주요 Incident 분석** | - Critical, High, Medium 해당<br>- 탐지 명 (영문)<br>- Date, Host, Internal IP, User<br>- File/Network Artifacts (표)<br>- Incident Summary<br>- 공격 기법 (MITRE ATT&CK)<br>- 권장 조치 (AI 분석)<br>- 담당자 조치 (공란) | 카드 + 표 + 텍스트 | JSON 기반 + 생성 |
| 4 | **호스트별 위협 집계** | - 한 주간 가장 많은 Incident 포함 Host<br>- 최대 10개 | 표 | 권장 | defenderxs |
| 5 | **주간 Incident 대응 완료율** | - 전체 대응 완료율 (%)<br>- Resolved / Under Investigation / Pending 건수 | 프로그레스 바 + 요약 카드 | AI 분석 통계 |
| 6 | **주간 최종 권고** | - 보안 유지 상황 요약<br>- 우선 조치 사항 (긴급도별) | 텍스트 블록 | JSON 기반 분석 |

---

## 5. 일간 리포트 (Daily Report) - 5개 섹션 

**보고 주기**: 매일 자동 생성  
**보고 기간**: 당일 (00:00 ~ 23:59)  
**주요 목적**: 실시간 위협 대응 및 일일 보안 상황 공유  
**리포트 대상**: 실무 보안 담당자, 운영 관리자

| No | 섹션 제목 | 포함 내용 | 시각화 유형 | 비고 |
|----|----------|----------|------------|------|
| 1 | **일간 Incident Summary** | - Severity별 개수 (Critical/High/Medium/Low)<br>- 탐지 건 줄글 요약 | 요약 카드 + 텍스트 | JSON  |
| 2 | **일간 탐지 이벤트 요약** | - **A.** 일간 이벤트 통계 (MITRE ATT&CK 탐지 유형)<br>- **B.** Status별 비율 (파이차트)<br>- **C.** Severity별 일간 인시던트 통계 (표) | 파이차트 + 표 | 인시던트 통계 기반 생성 |
| 3 | **주요 Incident 분석** | - Critical, High, Medium, Low 전체 해당<br>- 탐지 명 (영문)<br>- Date, Host, Internal IP, User<br>- File/Network Artifacts (표)<br>- Incident Summary<br>- 공격 기법 (MITRE ATT&CK)<br>- 권장 조치 (AI 분석)<br>- 담당자 조치 (공란) | 카드 + 표 + 텍스트 | 인시던트 통계 기반 생성 |
| 4 | **일간 Incident 대응 완료율** | - 전체 대응 완료율 (%)<br>- Resolved / Under Investigation / Pending 건수 | 프로그레스 바 + 요약 카드 | AI 분석  |
| 5 | **일간 최종 권고** | - 보안 유지 상황 요약<br>- 우선 조치 사항 (긴급도별) | 텍스트 블록 | JSON 기반 분석 |

---

## 6. 주요 Incident 분석 필드 상세 

모든 리포트에 공통으로 포함되는 **주요 Incident 분석** 섹션의 필드 정의입니다.

| 필드명 | 설명 | 데이터 소스 | 표시 형식 |
|--------|------|------------|----------|
| **A. 탐지 명** | Incident 탐지 명칭 (영문 그대로 표시) | Incident JSON | 텍스트 (영문) |
| **B. Date** | 탐지 일시 | Incident JSON → Detection time | YYYY-MM-DD HH:mm:ss |
| **C. Host** | 영향받은 호스트 명 | Incident JSON | 텍스트 |
| **D. Internal IP** | 내부 IP 주소 | Incident JSON | IPv4 형식 |
| **E. User** | 관련 사용자 계정 | Incident JSON | 이메일 또는 계정명 |
| **F. File/Network Artifacts** | 파일 및 네트워크 아티팩트 정보 | Incident JSON | 표 형식 |
| **G. Incident Summary** | 인시던트 요약 설명 | Incident JSON / AI 생성 | 텍스트 블록 |
| **H. 공격 기법** | MITRE ATT&CK 기법 및 전술 | Incident JSON | 태그 (Badge) |
| **I. 권장 조치** | AI 기반 권장 조치 사항 | AI 인시던트 분석 | 텍스트 블록 |
| **J. 담당자 조치** | 보안 담당자 실제 조치 내용 | 수동 입력 (편집 가능) | 편집 가능 필드 |

### 6.1 File/Network Artifacts 표 구조

| Type | Name / Value | Hash / IP | XDR Action |
|------|--------------|-----------|------------|
| File | 파일명 | SHA256 해시값 | 파일 실행 차단 여부 |
| Domain | 도메인명 | IP 주소 | 통신 차단 여부 |
| Network | 연결 정보 | IP 주소 | 차단 여부 |

---

## 7. 시각화 컴포넌트 정의 

### 7.1 차트 유형

| 차트 유형 | 사용 섹션 | 라이브러리 | 설명 |
|----------|----------|----------|------|
| **파이/도넛 차트** | Severity 분포, Status 분포 | Chart.js / Recharts | 비율 시각화 |
| **막대 그래프** | 요일별 Alert 통계 | Chart.js / Recharts | 기간별 비교 |
| **라인 차트** | 시간대별 추이 | Chart.js / Recharts | 트렌드 시각화 |
| **프로그레스 바** | 대응 완료율 | 커스텀 CSS | 달성률 표시 |

### 7.2 UI 컴포넌트

| 컴포넌트 | 용도 | 설명 |
|----------|------|------|
| **요약 카드** | Severity별 건수 표시 | Critical/High/Medium/Low 색상 구분 |
| **데이터 테이블** | 상세 목록 표시 | 정렬, 필터링 지원 |
| **인시던트 카드** | 개별 인시던트 상세 | 접기/펼치기 지원 |
| **Badge** | Severity, Status, MITRE 표시 | 색상 코드 적용 |
| **편집 필드** | 담당자 조치 입력 | 점선 박스 + 가이드 문구 |

### 7.3 색상 코드 정의

| 요소 | 색상 | HEX 코드 | 용도 |
|------|------|----------|------|
| Critical | 빨강 | `#EF4444` | Critical Severity |
| High | 주황 | `#F97316` | High Severity |
| Medium | 노랑 | `#EAB308` | Medium Severity |
| Low | 초록 | `#22C55E` | Low Severity |
| Resolved | 민트 | `#10B981` | 해결 완료 상태 |
| Investigating | 황색 | `#F59E0B` | 조사 중 상태 |
| Primary | 블루 | `#2563EB` | 주요 UI 요소 |
| Navy | 네이비 | `#0F2744` | 배경, 헤더 |

---

## 8. 출력 형식 및 기능 

### 8.1 출력 형식

| 형식 | 용도 | 구현 방식 |
|------|------|----------|
| **웹 리포트** | 실시간 조회 | React 컴포넌트 렌더링 |
| **DOCX 다운로드** | 오프라인 보관, 보고서 제출 | DOCX 라이브러리 변환 |

### 8.2 주요 기능

| 기능 | 설명 | 우선순위 |
|------|------|----------|
| **미리보기 (Preview)** | 다운로드 전 리포트 확인 |
| **다운로드 (Download)** | 워드 형식 저장 |
| **편집 모드** | 담당자 조치 필드 수정 |
| **인쇄 최적화** | 프린트 스타일 적용 |

---

## 9. 역할별 리포트 활용 가이드 

### 9.1 실무 보안 담당자
- **주로 보는 리포트**: 일간
- **중점 섹션**: 주요 Incident 분석, 일간 최종 권고
- **활용 목적**: 실시간 위협 대응 및 긴급 조치 실행

### 9.2 보안팀 리더 / IT 운영 책임자
- **주로 보는 리포트**: 주간
- **중점 섹션**: 주간 탐지 이벤트 요약, 호스트별 위협 집계, 대응 완료율
- **활용 목적**: 주간 운영 현황 파악 및 대응 전략 점검

### 9.3 CISO / CTO / 경영진
- **주로 보는 리포트**: 월간
- **중점 섹션**: 월간 Incident Summary, 규정 준수 여부, 최종 권고
- **활용 목적**: 경영진 보고, 보안 전략 수립, 감사 대응

### 9.4 감사팀
- **주로 보는 리포트**: 월간
- **중점 섹션**: 규정 준수 여부 (ISMS-P, ISO27001, GDPR), CVEs 위협 집계
- **활용 목적**: 내부 감사, 컴플라이언스 확인

---

## 10. 개발 체크리스트 ✅

### 10.1 공통 컴포넌트

- [ ] 리포트 헤더 컴포넌트 (제목, 기간, 대상, 목적)
- [ ] Severity 요약 카드 컴포넌트
- [ ] 파이/도넛 차트 컴포넌트
- [ ] 막대 그래프 컴포넌트
- [ ] 데이터 테이블 컴포넌트
- [ ] 인시던트 상세 카드 컴포넌트
- [ ] Artifacts 테이블 컴포넌트
- [ ] MITRE ATT&CK 태그 컴포넌트
- [ ] 편집 가능 필드 컴포넌트 (담당자 조치)
- [ ] 프로그레스 바 컴포넌트
- [ ] 최종 권고 텍스트 블록 컴포넌트
- [ ] 미리보기 버튼
- [ ] 다운로드 버튼
- [ ] PDF 변환 기능

### 10.2 월간 리포트

- [ ] 섹션 1: 월간 Incident Summary
- [ ] 섹션 2: 월간 탐지 이벤트 요약 (파이차트 2개 + 표)
- [ ] 섹션 3: 고위험 탐지 유형 (최대 10개)
- [ ] 섹션 4: 이벤트 분포 (Critical, High)
- [ ] 섹션 5: 주요 Incident 분석 (Critical, High)
- [ ] 섹션 6: 호스트별 위협 집계 (최대 10개)
- [ ] 섹션 7: CVEs 위협 집계 (CVSS 9.0+, 최대 10개)
- [ ] 섹션 8: 규정 준수 여부 (ISMS-P, ISO27001, GDPR)
- [ ] 섹션 9: 최종 권고

### 10.3 주간 리포트

- [ ] 섹션 1: 주간 Incident Summary
- [ ] 섹션 2-A: 주간 이벤트 통계 (MITRE ATT&CK)
- [ ] 섹션 2-B: 요일별 Alert 통계 (막대 그래프)
- [ ] 섹션 2-C: Status별 비율 (파이차트)
- [ ] 섹션 2-D: Severity별 통계 (표)
- [ ] 섹션 3: 주요 Incident 분석 (Critical, High, Medium)
- [ ] 섹션 4: 호스트별 위협 집계 (최대 10개)
- [ ] 섹션 5: 주간 Incident 대응 완료율
- [ ] 섹션 6: 주간 최종 권고

### 10.4 일간 리포트

- [ ] 섹션 1: 일간 Incident Summary
- [ ] 섹션 2-A: 일간 이벤트 통계 (MITRE ATT&CK)
- [ ] 섹션 2-B: Status별 비율 (파이차트)
- [ ] 섹션 2-C: Severity별 통계 (표)
- [ ] 섹션 3: 주요 Incident 분석 (전체 Severity)
- [ ] 섹션 4: 일간 Incident 대응 완료율
- [ ] 섹션 5: 일간 최종 권고

---

## 📎 부록

### A. 용어 정의

| 용어 | 정의 |
|------|------|
| **Incident** | 보안 위협 이벤트 |
| **Severity** | 위협 심각도 (Critical/High/Medium/Low) |
| **Status** | 처리 상태 (Resolved/Under Investigation/Pending) |
| **MITRE ATT&CK** | 사이버 공격 전술 및 기법 프레임워크 |
| **CVE** | Common Vulnerabilities and Exposures (공통 취약점 및 노출) |
| **CVSS** | Common Vulnerability Scoring System (공통 취약점 점수 시스템) |
| **XDR** | Extended Detection and Response (확장 탐지 및 대응) |
| **Artifact** | 탐지된 파일, 네트워크 등의 증거 데이터 |

### B. 참고 규정

| 규정 | 설명 |
|------|------|
| **ISMS-P** | 정보보호 및 개인정보보호 관리체계 인증 |
| **ISO 27001** | 국제 정보보안 관리체계 표준 |
| **GDPR** | 유럽 일반 개인정보보호법 |

---

**문서 버전**: 1.2  
**최종 업데이트**: 2024-12-10  
**작성자**: DeFender X 클라이언트 팀 박진주 연구원   
**문서 용도**: 기간별 리포트 기능 기획 및 개발 참고 자료
