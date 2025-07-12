k6 run -e ENV=nginx-fpm --out influxdb=http://localhost:8086/k6 /home/mamam/dev/web-performance/k6-script/spike-script/spike-script.js

         /\      Grafana   /‾‾/
    /\  /  \     |\  __   /  /
   /  \/    \    | |/ /  /   ‾‾\
  /          \   |   (  |  (‾)  |
 / __________ \  |_|\_\  \_____/

     execution: local
        script: /home/mamam/dev/web-performance/k6-script/spike-script/spike-script.js
        output: InfluxDBv1 (http://localhost:8086)

     scenarios: (100.00%) 1 scenario, 200 max VUs, 1m10s max duration (incl. graceful stop):
              * spike_test: Up to 200 looping VUs for 40s over 3 stages (gracefulRampDown: 30s, gracefulStop: 30s)



  █ THRESHOLDS

    http_req_duration
    ✓ 'p(95)<2000' p(95)=24.72ms

    http_req_failed
    ✓ 'rate<0.01' rate=0.00%


  █ TOTAL RESULTS

    checks_total.......................: 4971    114.202404/s
    checks_succeeded...................: 100.00% 4971 out of 4971
    checks_failed......................: 0.00%   0 out of 4971

    ✓ GET status is 200
    ✓ GET response has data
    ✓ GET response time < 5000ms

    HTTP
    http_req_duration.......................................................: avg=18.37ms min=13.34ms med=16.44ms max=795.57ms p(90)=22.15ms p(95)=24.72ms
      { expected_response:true }............................................: avg=18.37ms min=13.34ms med=16.44ms max=795.57ms p(90)=22.15ms p(95)=24.72ms
    http_req_failed.........................................................: 0.00%  0 out of 1657
    http_reqs...............................................................: 1657   38.067468/s

    EXECUTION
    iteration_duration......................................................: avg=2.04s   min=1.01s   med=2.01s   max=3.05s    p(90)=3.02s   p(95)=3.02s
    iterations..............................................................: 1657   38.067468/s
    vus.....................................................................: 1      min=0         max=199
    vus_max.................................................................: 200    min=200       max=200

    NETWORK
    data_received...........................................................: 81 MB  1.9 MB/s
    data_sent...............................................................: 186 kB 4.3 kB/s