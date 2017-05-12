# Jmeter

## plugin
### PerfMon Metrics Collector
`cpu, memory, network i/o 등을 모니터링할 수 있게 한다`
graph를 보여줄 `listener plugin`과 로컬의 데이터를 수집할 `agent`를 설치해야한다. 플러그인만 설치해서는 동작하지 않고, 에러를 뿌릴 것이다.

#### 리스너 설치
Plugins Manager를 사용해서 설치

#### Agent 설치
아래에서 다운 받아 적당한 위치에 설치/실행
[PerfMon Server Agent download](https://jmeter-plugins.org/wiki/PerfMonAgent/?utm_source=Blog&utm_medium=BM_blog&utm_campaign=PerfMon)
```
$ startAgent.sh
```
