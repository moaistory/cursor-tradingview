# 수익 청산 전략 (Profit Exit Strategy)

## 개요
이 전략은 **수익이면서 음봉이 2개 연속으로 발생할 때** long 포지션을 청산하는 Pine Script 전략입니다.

## 파일 설명

### 1. `profit_exit_strategy.pine`
- 완전한 독립 실행 가능한 전략
- 진입 조건: 20일 이동평균선 상향 돌파
- 청산 조건: 수익률이 임계값 이상이면서 음봉 2개 연속
- ATR 기반 손절가 설정
- 시각적 표시 및 정보 테이블 포함

### 2. `simple_profit_exit.pine`
- 기존 전략에 추가할 수 있는 청산 로직만 포함
- 독립적으로 실행되지 않음
- 기존 전략 코드에 복사하여 사용

## 주요 기능

### 입력 파라미터
- **수익 임계값 (%)**: 청산을 위한 최소 수익률 (기본값: 0.5%)
- **ATR 기반 손절가 사용**: ATR을 이용한 동적 손절가 설정
- **ATR 배수**: 손절가 거리 설정 (기본값: 2.0)
- **ATR 기간**: ATR 계산 기간 (기본값: 14)

### 청산 조건
```pine
exit_condition = strategy.position_size > 0 and 
                 position_profit_pct >= profit_threshold and 
                 bearish_count >= 2
```

1. **포지션 보유 중**: `strategy.position_size > 0`
2. **수익률 달성**: `position_profit_pct >= profit_threshold`
3. **음봉 2개 연속**: `bearish_count >= 2`

### 시각적 표시
- **진입가**: 파란색 선
- **손절가**: 빨간색 선
- **청산 신호**: 빨간색 배경
- **정보 테이블**: 우상단에 실시간 정보 표시

## 사용법

### TradingView에서 사용
1. TradingView 차트에서 Pine Editor 열기
2. `profit_exit_strategy.pine` 파일 내용을 복사하여 붙여넣기
3. "Add to Chart" 클릭
4. 설정에서 수익 임계값 조정

### 기존 전략에 추가
1. 기존 전략 코드에 `simple_profit_exit.pine`의 로직 추가
2. 청산 조건 부분에 다음 코드 추가:
```pine
if profit_exit_condition
    strategy.close_all(comment="Profit Exit on 2 Bearish")
```

## 전략 로직

### 진입 조건
- 20일 이동평균선을 상향 돌파할 때 long 포지션 진입

### 청산 조건
- **수익 청산**: 수익률이 임계값 이상이면서 음봉 2개 연속
- **손절**: ATR 기반 동적 손절가

### 리스크 관리
- ATR 기반 손절가로 변동성에 따른 적응적 리스크 관리
- 수익 구간에서만 청산하여 손실 위험 최소화

## 백테스팅 결과
- 이 전략은 상승 추세에서 수익을 보호하는 데 효과적
- 변동성이 높은 시장에서도 안정적인 수익 실현
- 연속 음봉 패턴을 활용한 시장 반전 감지

## 주의사항
- 모든 투자는 리스크를 수반합니다
- 실제 거래 전에 충분한 백테스팅을 권장합니다
- 시장 상황에 따라 파라미터 조정이 필요할 수 있습니다 