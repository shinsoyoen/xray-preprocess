# Pediatric Abdominal X-ray Dataset Preprocessing

## 📖 프로젝트 개요
이 저장소는 소아 복부 X-ray 합성 데이터셋을 **딥러닝 학습용**으로 변환하는 전처리 파이프라인을 제공합니다.  
원본 데이터셋은 `JSON` 라벨과 `PNG` 이미지를 포함하며, 이를 **Train / Val / Test** 로 분할하고 **마스크 이미지**를 생성합니다.  

최종적으로는 `Processed/` 디렉토리에 다음과 같은 구조로 저장됩니다:

Processed/
├─ train/
│ ├─ images/ (7,200개)
│ └─ masks/ (7,200개)
├─ val/
│ ├─ images/ (800개)
│ └─ masks/ (800개)
└─ test/
├─ images/ (1,000개)
└─ masks/ (1,000개)

---

## ⚙️ 환경 설정
```bash
# 가상환경 권장 (Python 3.10 이상)
python -m venv venv
source venv/bin/activate   # (Linux/Mac)
venv\Scripts\activate      # (Windows)

# 필수 패키지 설치
pip install pillow tqdm

# 전처리
python preprocess.py

# 검증
import os
base = "Processed"
for split in ["train", "val", "test"]:
    img_dir = os.path.join(base, split, "images")
    mask_dir = os.path.join(base, split, "masks")
    print(f"{split.upper()} - images: {len(os.listdir(img_dir))}, masks: {len(os.listdir(mask_dir))}")

# 예상 출력
TRAIN - images: 7200, masks: 7200
VAL   - images: 800, masks: 800
TEST  - images: 1000, masks: 1000

# 사용한 데이터셋
https://www.aihub.or.kr/aihubdata/data/view.do?currMenu=115&topMenu=100&aihubDataSe=data&dataSetSn=71862
