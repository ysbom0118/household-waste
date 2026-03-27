# 🗑️ 생활 폐기물 분리 Object Detection 프로젝트

> AI Hub 생활 폐기물 데이터를 활용한 폐기물 분류(Object Detection) 프로젝트

---

# 📃 Contents

- [1. 프로젝트 소개](#1-프로젝트-소개)
  - [목표](#목표)
  - [수행 환경](#수행-환경)
  - [Project Workflow](#project-workflow)
- [2. 데이터](#2-데이터)
  - [데이터 출처](#데이터-출처)
  - [사용 데이터](#사용-데이터)
  - [데이터 전처리](#데이터-전처리)
- [3. 실험](#3-실험)
  - [baseline](#baseline)
  - [실험 1](#실험-1)
  - [실험 2](#실험-2)
- [4. 결과](#4-결과)
- [5. 프로젝트 회고](#5-프로젝트-회고)
  - [어려웠던 점](#어려웠던-점)
  - [개선 방향](#개선-방향)

---

# 1. 프로젝트 소개

## 목표

- 생활 폐기물 이미지 데이터를 활용하여 **Object Detection 기반 분류 모델 개발**
- YOLO 모델을 활용하여 폐기물 종류 자동 인식

### 분류 대상 클래스
- 종이
- 플라스틱
- 페트병
- 캔

### 성능 평가 지표
- mAP50-95
- Precision / Recall

---

## 수행 환경

- 개발 환경: Google Colab
- GPU: T4
- Framework: Ultralytics YOLO

---

## Project Workflow

- 데이터 수집 → 데이터 전처리 → 라벨 변환 → 모델 학습 → 성능 평가 → 개선 실험


---

# 2. 데이터

## 데이터 출처

- AI Hub 생활 폐기물 데이터셋  
https://aihub.or.kr/aihubdata/data/view.do?srchOptnCnd=OPTNCND001&currMenu=115&topMenu=100&searchKeyword=%EC%83%9D%ED%99%9C%ED%8F%90%EA%B8%B0%EB%AC%BC&aihubDataSe=data&dataSetSn=140

---

## 사용 데이터

- 총 4개 클래스 사용
  - 종이
  - 플라스틱
  - 페트병
  - 캔

- 원본 데이터셋 중 일부만 사용

---

## 데이터 전처리

### 이미지 전처리
- Resize: **640 × 640**

### 라벨 변환
- 기존: JSON 형식
- 변환: YOLO format (txt)


### 데이터 구조

dataset
├── train
│ ├── images
│ └── labels
├── valid
│ ├── images
│ └── labels
└── data.yaml


---

# 3. 실험

## baseline

| name | model | epoch | batch | imgsz | patience |
|------|------|------|------|------|----------|
| baseline | yolo26n | 100 | 32 | 640 | 10 |

👉 결과 이미지 삽입

---

## 실험 1

- batch size 증가

| name | model | epoch | batch | imgsz | patience |
|------|------|------|------|------|----------|
| exp1 | yolo26n | 100 | 64 | 640 | 10 |

👉 결과 이미지 삽입

### 실험 결과 분석

- batch size 증가에 따른 성능 변화 분석 작성

---

## 실험 2

### 적용 기법
- epoch 증가 (200)
- mixup = 0.1
- optimizer = AdamW
- label smoothing = 0.1
- cosine learning rate 적용

| name | model | epoch | batch | patience | 기타 |
|------|------|------|------|----------|------|
| exp2 | yolo26n | 200 | 32 | 30 | mixup, AdamW, cos_lr |

👉 결과 이미지 삽입

### 실험 결과 분석

- 데이터 augmentation 및 optimizer 변경 효과 분석
- 과적합 여부 확인
- 성능 향상 여부 기술

---

# 4. 결과

## 모델 비교

| 모델 | mAP50-95 | Precision | Recall |
|------|----------|-----------|--------|
| baseline |  |  |  |
| exp1 |  |  |  |
| exp2 |  |  |  |

👉 confusion matrix / PR curve / 예측 결과 이미지 삽입

---

## 결과 해석

- 최고 성능 모델 분석
- 클래스별 성능 차이 분석
- 오탐 / 미탐 사례 분석

---

# 5. 프로젝트 회고

## 어려웠던 점

- JSON → YOLO 라벨 변환 과정
- 클래스 불균형 문제
- Colab 환경에서 학습 시간 제한

---

## 개선 방향

- 데이터 증강 추가
- 더 큰 모델 실험 (yolo26s, m 등)
- 클래스 균형 조정
- 실시간 적용을 위한 경량화 고려
