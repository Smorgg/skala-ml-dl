# SKALA ML/DL 실습 환경

이 저장소는 Python 3.11.11 기반의 머신러닝·딥러닝 Jupyter Notebook 실습 환경입니다.
필수 라이브러리는 루트의 `requirements.txt`에서 한 번에 관리합니다.

## 프로젝트 구조

```text
.
├── 04-DeepLearning/   # 딥러닝 실습 Notebook
├── requirements.txt  # 실습에 필요한 Python 라이브러리
├── .gitignore        # 가상환경과 학습 결과 제외 규칙
└── README.md
```

## 사전 준비

- Python 버전 관리를 위한 `pyenv`
- VS Code의 Python 확장
- VS Code의 Jupyter 확장

Python 3.11.11이 없다면 터미널에서 설치합니다.

```bash
brew install pyenv
pyenv install 3.11.11
```

이미 설치되어 있는지는 다음 명령으로 확인할 수 있습니다.

```bash
"$HOME/.pyenv/versions/3.11.11/bin/python" --version
```

## 가상환경 생성

프로젝트 루트에서 Python 3.11.11을 명시하여 `.venv`를 생성합니다.
이 방식은 기존 Homebrew Python이나 셸의 Python 별칭을 변경하지 않습니다.

```bash
cd /Users/han/skala-workspace/skala-ml-dl

"$HOME/.pyenv/versions/3.11.11/bin/python" -m venv .venv
```

## 필수 라이브러리 설치

`pip` 명령이 다른 Python을 가리키는 문제를 피하기 위해 가상환경의 Python 경로를
명시합니다.

```bash
.venv/bin/python -m pip install --upgrade pip
.venv/bin/python -m pip install -r requirements.txt
```

`requirements.txt`에는 다음 범주의 라이브러리가 포함되어 있습니다.

- Jupyter 커널: `ipykernel`
- 통계·머신러닝: NumPy, pandas, seaborn, Matplotlib, scikit-learn 등
- 딥러닝·자연어 처리: PyTorch, Transformers, Datasets 등

## Jupyter 커널 등록

새 가상환경을 VS Code Jupyter 커널 목록에 등록합니다.

```bash
.venv/bin/python -m ipykernel install --user \
  --name skala-ml-dl-31111 \
  --display-name "Python 3.11.11 (skala-ml-dl)"
```

VS Code에서 Notebook을 연 뒤 오른쪽 위의 **Select Kernel**에서
`Python 3.11.11 (skala-ml-dl)`을 선택합니다. 목록이 갱신되지 않으면
명령 팔레트에서 **Developer: Reload Window**를 실행합니다.

## 환경 확인

Notebook 셀에서 현재 커널의 Python 버전과 실행 경로를 확인합니다.

```python
# Notebook이 프로젝트 가상환경의 Python을 사용하는지 확인합니다.
import sys

print(sys.version)
print(sys.executable)
```

정상적으로 설정되었다면 Python 버전은 `3.11.11`, 실행 경로는 다음과 같이 표시됩니다.

```text
/Users/han/skala-workspace/skala-ml-dl/.venv/bin/python
```

가상환경인 `.venv/`는 로컬에서만 사용하며 Git에 커밋하지 않습니다.
