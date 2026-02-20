---
tags: [redis, concurrency]
created: 2026-02-20
---
# Redis 분산 락으로 동시성 제어

## 한 줄 요약
> Redisson의 RLock으로 분산 환경에서 동시 예약 문제를 해결

## 내용
OTORIDE 차량 공유 서비스에서 동일 차량에 대한 동시 예약 요청 시 중복 예약이 발생하는 문제가 있었다.

### 문제 상황
- 여러 사용자가 동시에 같은 차량을 예약 시도
- MySQL의 트랜잭션만으로는 분산 환경에서 동시성 제어 불가

### 해결
```java
RLock lock = redissonClient.getLock("vehicle:lock:" + vehicleId);
try {
    if (lock.tryLock(5, 10, TimeUnit.SECONDS)) {
        // 예약 로직 수행
    }
} finally {
    lock.unlock();
}
```

### 핵심 포인트
- `tryLock(waitTime, leaseTime, unit)`: 대기 시간과 자동 해제 시간 설정
- 데드락 방지를 위해 leaseTime 필수 설정
- 차량 단위로 락 키를 분리하여 불필요한 경합 최소화

## 연결
- MOC: [[Redis]] [[Spring]]
- 관련: [[MySQL 비관적 락 vs 낙관적 락]]