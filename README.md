# *KISTI-MCP*

한국과학기술정보연구원(KISTI)이 서비스하는 다양한 플랫폼의 OpenAPI를 LLM이 활용할 수 있게 하는 MCP서버입니다.
## 사용 가능한 도구(10개)

| 도구명                                           | 기능             |
| --------------------------------------------- | -------------- |
| `search_scienceon_papers`                     | - 논문 목록 검색     |
| `search_scienceon_paper_details`              | - 논문 상세 정보     |
| `search_scienceon_patents`                    | - 특허 목록 검색     |
| `search_scienceon_patent_details`             | - 특허 상세 정보     |
| `search_scienceon_patent_citations`           | - 특허 인용/피인용 관계 |
| `search_scienceon_reports`                    | - 보고서 목록 검색    |
| `search_scienceon_report_details`             | - 보고서 상세 정보    |
| `search_ntis_rnd_project`                     | - 과제 검색        |
| `search_ntis_science_tect_classifications`    | - 과학기술분류 추천    |
| `search_ntis_related_content_recommendations` | - 과제 연관콘텐츠 추천  |

## 📜History

| 버전     | 날짜         | 주요 사항                                                                             |
| ------ | ---------- | --------------------------------------------------------------------------------- |
| 0.2.10 | 2025-08-13 | - NTIS 과제 검색 도구 기능 지원<br>- NTIS 과학기술분류 추천 도구 기능 지원<br>- NTIS 과제 연관콘텐츠 추천 도구 기능 지원 |
| 0.1.7  | 2025-07-22 | - 첫 번째 릴리즈<br>- ScienceON 의 논문, 특허, 보고서 등 총 7종의 API 사용 지원                         |

## 설치

### 요구사항
---
- [uv](https://github.com/astral-sh/uv) (권장) 또는 pip 사용
    - Python 3.10 이상
- KISTI 플랫폼 별 API 키 필요
	- ScienceON - API Key, Client ID, MAC Address
		- https://scienceon.kisti.re.kr/por/oapi/openApi.do 사이트 방문
		- 회원가입 및 로그인
		- API Key 및 Client ID 발급 신청
	- NTIS - API Key
		- https://www.ntis.go.kr/rndopen/api/mng/apiMain.do 사이트 방문
		- 회원가입 및 로그인
		- 데이터활용 > OpenAPI > API 별 활용신청
			- 1) 국가R&D 과제검색 서비스(대국민용) 2021-02-09
			- 2) 과학기술표준분류 추천 서비스(기관용) 2019-12-31
			- 3) 연관콘텐츠 추천 서비스(전체용) 2023-11-27
- MCP 지원 LLM 클라이언트 설정
	- Claude Desktop 

### 설치 방법
---
#### uv 사용 (권장)

1. 저장소 클론(작업폴더(예 C:\MCP)에서 )

```bash
git clone https://github.com/ansua79/kisti-mcp.git
cd kisti-mcp
```

2. uv로 의존성 설치

```bash
uv sync
```

#### 전통적인 pip 방법

1. 가상환경 생성 및 활성화(작업폴더(예 C:\MCP)에서 )

```bash
python -m venv venv
source venv/bin/activate  # Linux/Mac
# 또는
venv\Scripts\activate     # Windows
```

2. 의존성 설치

```bash
pip install -e .
# 또는 직접 설치
pip install fastmcp httpx pycryptodome
```

#### 환경변수 설정

1. `.env.example` 파일을 `.env`로 복사

```bash
cp .env.example .env
```

2. `.env` 파일을 편집하여 실제 값으로 변경:

```
# .env 파일 내용
SCIENCEON_API_KEY=your_actual_api_key
SCIENCEON_CLIENT_ID=your_actual_client_id
SCIENCEON_MAC_ADDRESS=your_actual_mac_address

NTIS_RND_PROJECT_API_KEY=your_ntis_api_key
NTIS_CLASSIFICATION_API_KEY=your_ntis_api_key
NTIS_RECOMMENDATION_API_KEY=your_ntis_api_key
```

### 동작확인
---
- 실행(uv사용:권장)
```bash
uv run kisti-mcp-server.py
```

- 예시
```
PS D:\mcp\kisti-mcp-0.2.10> uv run .\kisti-mcp-server.py
Using CPython 3.10.17
Creating virtual environment at: .venv
      Built kisti-mcp-server @ file:///D:/mcp/kisti-mcp-0.2.10
░░░░░░░░░░░░░░░░░░░░ [0/48] Installing wheels...                                   
Installed 48 packages in 1.29s
INFO:__main__:.env 파일에서 6개의 환경변수를 로드했습니다.
INFO:__main__:KISTI API 인증 정보가 성공적으로 로드되었습니다.
INFO:__main__:.env 파일에서 6개의 환경변수를 로드했습니다.
INFO:__main__:NTIS API 인증 정보가 성공적으로 로드되었습니다.


╭─ FastMCP 2.0 ──────────────────────────────────────────────────────────────╮
│                                                                            │
│        _ __ ___ ______           __  __  _____________    ____    ____     │
│       _ __ ___ / ____/___ ______/ /_/  |/  / ____/ __ \  |___ \  / __ \    │
│      _ __ ___ / /_  / __ `/ ___/ __/ /|_/ / /   / /_/ /  ___/ / / / / /    │
│     _ __ ___ / __/ / /_/ (__  ) /_/ /  / / /___/ ____/  /  __/_/ /_/ /     │
│    _ __ ___ /_/    \__,_/____/\__/_/  /_/\____/_/      /_____(_)____/      │
│                                                                            │
│                                                                            │
│                                                                            │
│    🖥️  Server name:     KISTI-MCP Server                                    │
│    📦 Transport:       STDIO                                               │
│                                                                            │
│    📚 Docs:            https://gofastmcp.com                               │
│    🚀 Deploy:          https://fastmcp.cloud                               │
│                                                                            │
│    🏎️  FastMCP version: 2.10.6                                              │
│    🤝 MCP version:     1.12.2                                              │
│                                                                            │
╰────────────────────────────────────────────────────────────────────────────╯


[08/13/25 14:58:11] INFO     Starting MCP server 'KISTI-MCP Server' with transport 'stdio'                server.py:1371

```

### 사용 방법
---
#### 도구 등록(Claude Desktop 기준)
```
%APPDATA%\Claude\claude_desktop_config.json 파일 수정

{
  "mcpServers": {
    "kisti": {
      "command": "uv", 
      "args": [
        "--directory",
        "설치디렉토리명", 
        "run",
        "kisti-mcp-server.py"
      ]
    }
  }
}
```
* 설치디렉토리명은 D:\mcp\kisti-mcp 등으로 설치환경에 따라 수정

#### 클라이언트(Claude Desktop) 재시작
- 작업관리자에서도 완전 종료 후 재시작
- 검색 및 도구 : kisti ⑩ 확인


## 프로젝트 구조

```
kisti-mcp/
├── kisti-mcp-server.py    # 메인 서버 파일
├── pyproject.toml         # 프로젝트 설정
├── .env.example          # 환경변수 예시 파일
├── .env                  # 환경변수 파일 (사용자가 생성)
├── README.md             # 이 파일
├── LICENSE               # 라이선스
└── .gitignore           # Git 무시 파일
```

## 데이터 소스

- **KISTI ScienceON** : 한국과학기술정보연구원 과학기술 지식인프라
- **KISTI NTIS** : 한국과학기술정보연구원 국가과학기술지식정보서비스 

## 라이선스

이 프로젝트는 **Creative Commons Attribution-NonCommercial 4.0 International License (CC BY-NC 4.0)** 하에 배포됩니다.

- ✅ 개인적/학술/연구/교육 목적 사용, 비상업적 사용 허용
- ❌ 상업적 사용 금지
- 💼 상업적 사용을 원하시는 경우 별도 라이선스가 필요합니다. 문의: [raezero@kisti.re.kr]

자세한 내용은 [LICENSE](https://github.com/ansua79/kisti-mcp/LICENSE) 파일을 참조하세요.

## 문제 해결

### 일반적인 문제
---
1. **토큰 발급 실패**
    - API 키와 클라이언트 ID가 올바른지 확인
    - MAC 주소가 정확한지 확인
    - 네트워크 연결 상태 확인
2. **검색 결과 없음**
    - 검색 키워드를 다양하게 시도
    - 한글 키워드 사용 권장
3. **환경변수 확인**
    - `.env` 파일이 올바르게 설정되었는지 확인
    - 환경변수 값에 따옴표나 공백이 없는지 확인

## KISTI 초거대AI연구센터 AI플랫폼팀

KISTI의 초거대AI연구센터는 2023년 12월 KISTI는 생성형 거대 언어 모델 'KONI(KISTI Open Natural Intelligence)'의 첫선을 토대로 2024년 3월 정식 출범한 부서이며, **AI플랫폼팀은 AI모델 및 Agent 서비스 기술 개발**을 담당하고 있습니다.

## 지원

문제가 있거나 질문이 있으시면 [Issues](https://github.com/ansua79/kisti-mcp/issues)에서 문의해주세요.

## 관련 링크
- [KISTI-AI-Platform-Team](https://github.com/KISTI-AI-Platform-Team/BlueSkyNova)
- [KONI:KISTI Open Neural Intelligence](https://huggingface.co/KISTI-KONI) - KISTI 과학기술정보 특화 거대언어생성모델
- [SpectraBench](https://github.com/gwleee/SpectraBench) - Intelligent Scheduling System for Large Language Model Benchmarking
- [DOREA(Document-Oriented Reasoning and Explanation Assistant)](https://github.com/Byun11/Dorea-pdf-ai)
- [KISTI ScienceON](https://scienceon.kisti.re.kr/)
- [KISTI NTIS](https://www.ntis.go.kr)
