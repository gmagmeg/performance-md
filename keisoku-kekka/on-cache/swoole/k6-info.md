http://localhost:3000/d/ReuNR5Aik/k6-dashboard?orgId=1&from=2025-07-11T23:57:35.887Z&to=2025-07-12T00:01:54.446Z&timezone=browser&var-URL=$__all&var-interval_value=3&var-data_source=deoi7eicapo1sb&refresh=10s

k6 run -e ENV=swoole-php --out influxdb=http://localhost:8086/k6 /home/mamam/dev/web-performance/k6-script/scripts/post-weight-flow-script.js

         /\      Grafana   /‾‾/
    /\  /  \     |\  __   /  /
   /  \/    \    | |/ /  /   ‾‾\
  /          \   |   (  |  (‾)  |
 / __________ \  |_|\_\  \_____/

     execution: local
        script: /home/mamam/dev/web-performance/k6-script/scripts/post-weight-flow-script.js
        output: InfluxDBv1 (http://localhost:8086)

     scenarios: (100.00%) 1 scenario, 80 max VUs, 4m30s max duration (incl. graceful stop):
              * btoc_scenario: Up to 80 looping VUs for 4m0s over 3 stages (gracefulRampDown: 30s, gracefulStop: 30s)



  █ THRESHOLDS

    http_req_duration{name:post_weight_create}
    ✓ 'p(90)<3000' p(90)=45.64ms

    http_req_duration{name:post_weight_get}
    ✓ 'p(90)<1000' p(90)=16.38ms

    http_req_failed
    ✓ 'rate<0.001' rate=0.00%


  █ TOTAL RESULTS

    checks_total.......................: 7489    31.000836/s
    checks_succeeded...................: 100.00% 7489 out of 7489
    checks_failed......................: 0.00%   0 out of 7489

    ✓ GET status is 200
    ✓ POST status is 200
    ✓ GET post has correct ID

    HTTP
    http_req_duration.........................................................: avg=13.26ms min=5.22ms  med=11.1ms  max=159.58ms p(90)=20.51ms p(95)=31.93ms
      { expected_response:true }..............................................: avg=13.26ms min=5.22ms  med=11.1ms  max=159.58ms p(90)=20.51ms p(95)=31.93ms
      { name:post_weight_create }.............................................: avg=35.37ms min=17.28ms med=33.53ms max=159.58ms p(90)=45.64ms p(95)=49.23ms
      { name:post_weight_get }................................................: avg=11.21ms min=5.22ms  med=10.43ms max=115.71ms p(90)=16.38ms p(95)=18.18ms
    http_req_failed...........................................................: 0.00%  0 out of 6904
    http_reqs.................................................................: 6904   28.579219/s

    EXECUTION
    iteration_duration........................................................: avg=2.29s   min=2s      med=2.01s   max=5.18s    p(90)=2.02s   p(95)=5.04s
    iterations................................................................: 6319   26.157602/s
    vus.......................................................................: 2      min=1         max=80
    vus_max...................................................................: 80     min=80        max=80

    NETWORK
    data_received.............................................................: 56 MB  231 kB/s
    data_sent.................................................................: 1.2 MB 4.9 kB/s