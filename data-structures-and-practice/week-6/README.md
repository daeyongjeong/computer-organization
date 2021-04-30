# Week 6

## Problem 1: Linked_Queue 구현

- 문자들의 Linked Queue를 테스트하는 프로그램 구현
- 명령어
  - `+<c>` : AddQ
  - `-` : DeleteQ
  - S : Show
  - Q : Quit

### 출력 예시

```
*********** Command ***********
+<c>: AddQ c, -: DeleteQ,
S: Show, Q: Quit
*******************************

Command> +1
Command> +2
Command> +3
Command> +4
Command> -
 1
Command> -
 2
Command> +5
Command> +6
Command> +7
Command> +8
Command> +9
Command> +a
Command> +b
Command> +c
Command> +d
Command> s
 3 4 5 6 7 8 9 a b c d

Command> -
 3
Command> -
 4
Command> s
 5 6 7 8 9 a b c d
```

## Problem 2: Queue_simulation

- 프린터 작업에 대한 simulation
  - Linked Queue로 프린터 큐 구현
- 시뮬레이션 방식
  - `current_time`을 증가시키면서 매 시각 가상의 프린트 job을 처리

```
while(current_time < MAX_SIMUL_TIME) {
... ++current_time;
}
```

- job
  - `id` – job의 ID
  - `arrival_time` – job이 도착한 시간
  - `duration` – job의 프린트 시간
- 새로운 job의 도착 (`is_job_arrived()`)
  - `random()` 을 호출, 반환값이 정해진 값보다 작으면 도착한 것으로 간주
  - 새 job을 큐에 삽입 (`insert_job_into_queue (id, arrival_time, duration)`)
    - 새 job의 프린트 시간 `duration = random() \* MAX_PRINTING_TIME + 1`
- 프린트 완료 (`is_printer_idle()`)
  - 남은 프린트 시간이 0 이하면 완료된 것임
  - 큐에서 다음 job을 가져와 실행 (`process_next_job()`)
    - `current_job_id = job.id`
    - `remaining_time = job.duration`
- job 을 프린트 하기
  - 프린트 시간을 매 시각 하나씩 감소시키는 것을 프린트가 되는 것으로 간주
    - 매 시각: `--remaining_time`
- 난수 발생 함수
  - `rand()` 함수
    - 0 ~ `RAND_MAX` 까지의 정수를 무작위로 반환
  - `srand()`함수
    - 매번 새로운 난수를 발생시키기 위하여 사용
    - `srand(time(NULL))`
- 0.0 ~ 1.0 까지의 실수를 무작위로 반환
  - `return rand()/(double)RAND_MAX;`
- 1 ~ 5 까지의 정수를 무작위로 반환
  - `return (int)(5\*(rand()/(double)RAND_MAX)) + 1;`

### 출력 예시

```
===== time 0 =====
 새 Job <1>이 들어 왔습니다. 프린트 시간은 = 3 입니다.
 프린트를 시작합니다 - Job <1> ...
 현재 프린터 큐: [ ]

===== time 1 =====
 새 Job <2>이 들어 왔습니다. 프린트 시간은 = 5 입니다.
 아직 Job <1>을 프린트하고 있습니다 ...
 현재 프린터 큐: [ 2 ]

===== time 2 =====
 아직 Job <1>을 프린트하고 있습니다 ...
 현재 프린터 큐: [ 2 ]

===== time 3 =====
 새 Job <3>이 들어 왔습니다. 프린트 시간은 = 2 입니다.
 프린트를 시작합니다 - Job <2> ...
 현재 프린터 큐: [ 3 ]

===== time 4 =====
 아직 Job <2>을 프린트하고 있습니다 ...
 현재 프린터 큐: [ 3 ]

===== time 5 =====
 아직 Job <2>을 프린트하고 있습니다 ...
 현재 프린터 큐: [ 3 ]

===== time 6 =====
 아직 Job <2>을 프린트하고 있습니다 ...
 현재 프린터 큐: [ 3 ]

===== time 7 =====
 새 Job <4>이 들어 왔습니다. 프린트 시간은 = 5 입니다.
 아직 Job <2>을 프린트하고 있습니다 ...
 현재 프린터 큐: [ 3 4 ]

...

===== time 14 =====
 새 Job <8>이 들어 왔습니다. 프린트 시간은 = 1 입니다.
 아직 Job <4>을 프린트하고 있습니다 ...
 현재 프린터 큐: [ 5 6 7 8 ]

===== time 15 =====
 새 Job <9>이 들어 왔습니다. 프린트 시간은 = 1 입니다.
 프린트를 시작합니다 - Job <5> ...
 현재 프린터 큐: [ 6 7 8 9 ]

===== time 16 =====
 새 Job <10>이 들어 왔습니다. 프린트 시간은 = 3 입니다.
 프린트를 시작합니다 - Job <6> ...
 현재 프린터 큐: [ 7 8 9 10 ]

===== time 17 =====
 아직 Job <6>을 프린트하고 있습니다 ...
 현재 프린터 큐: [ 7 8 9 10 ]

===== time 18 =====
 프린트를 시작합니다 - Job <7> ...
 현재 프린터 큐: [ 8 9 10 ]

===== time 19 =====
 프린트를 시작합니다 - Job <8> ...
 현재 프린터 큐: [ 9 10 ]

완료된 프린트 Job = 8 개
평균 지연 시간    = 3.8750000 단위시간
```