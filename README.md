# SKALA ML/DL 실습 환경

이 저장소는 Python 3.11.11 기반의 머신러닝 및 딥러닝 Jupyter Notebook 실습
프로젝트입니다. Python 버전, 가상환경과 라이브러리는 `uv`로 관리합니다.

## 프로젝트 구조

```text
.
├── 04-DeepLearning/  # 딥러닝 실습 Notebook
├── .python-version   # 프로젝트 Python 버전
├── pyproject.toml    # 직접 의존성과 프로젝트 설정
├── uv.lock           # 실제 설치 버전 잠금 파일
├── .gitignore        # 가상환경과 학습 결과 제외 규칙
└── README.md
```

`.venv/`는 로컬 가상환경이므로 Git에 커밋하지 않습니다. `pyproject.toml`과
`uv.lock`은 다른 환경에서도 같은 의존성을 재현할 수 있도록 Git에 포함합니다.

## 사전 준비

다음 도구가 필요합니다.

- `uv`
- `libomp` (`xgboost`, `lightgbm` 실행에 필요한 macOS OpenMP 런타임)
- VS Code의 Python 확장
- VS Code의 Jupyter 확장

macOS에서 `uv`가 없다면 설치합니다.

```bash
brew install uv
```

Apple Silicon Mac에서 `xgboost` 또는 `lightgbm` import 시 `libomp.dylib` 오류가
발생하면 OpenMP 런타임을 설치합니다.

```bash
brew install libomp
```

## 프로젝트 환경 준비

프로젝트 루트에서 다음 명령을 실행합니다.

```bash
cd /Users/han/skala-workspace/skala-ml-dl
uv sync
```

`uv sync`는 다음 작업을 처리합니다.

- `.python-version`에 지정된 Python 3.11.11 준비
- 프로젝트의 `.venv` 생성 또는 동기화
- `uv.lock`에 기록된 버전으로 필수 라이브러리 설치
- 잠금 파일에 없는 불필요한 패키지 제거

가상환경을 직접 활성화하지 않아도 `uv run`으로 프로젝트 환경의 명령을 실행할 수
있습니다.

```bash
uv run python --version
uv run python -c "import sys; print(sys.executable)"
uv tree
```

## 의존성 관리

새 라이브러리를 추가합니다.

```bash
uv add <패키지명>
```

개발 도구를 추가합니다.

```bash
uv add --dev <패키지명>
```

라이브러리를 제거합니다.

```bash
uv remove <패키지명>
```

이 명령들은 `pyproject.toml`, `uv.lock`, `.venv`를 함께 갱신합니다. Notebook
안에서 임시로 `%pip install`한 패키지는 프로젝트 의존성에 기록되지 않으므로,
계속 사용할 라이브러리는 `uv add`로 추가합니다.

일부 하위 패키지가 폐기된 `sklearn` 배포판을 참조하지만, 프로젝트에서는 올바른
패키지인 `scikit-learn`을 직접 사용하고 잘못된 배포판은 uv 설정으로 제외합니다.
또한 이 저장소의 잠금 대상은 현재 실습 환경과 같은 macOS로 제한합니다.

## VS Code Jupyter 커널

`uv sync`를 완료한 뒤 Notebook 오른쪽 위의 **Select Kernel**에서 다음 환경을
선택합니다.

```text
Python Environments
└── /Users/han/skala-workspace/skala-ml-dl/.venv/bin/python
```

기존 커널 목록이 남아 있으면 명령 팔레트에서 **Developer: Reload Window**를
실행한 뒤 다시 선택합니다.

Notebook 셀에서 실제 실행 환경을 확인합니다.

```python
# Notebook이 uv 프로젝트 가상환경을 사용하는지 확인합니다.
import sys

print(sys.version)
print(sys.executable)
```

정상적인 결과에는 Python `3.11.11`과 다음 실행 경로가 포함됩니다.

```text
/Users/han/skala-workspace/skala-ml-dl/.venv/bin/python
```
