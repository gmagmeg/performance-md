http://localhost:3000/d/ReuNR5Aik/k6-dashboard?orgId=1&from=2025-07-11T13:56:21.183Z&to=2025-07-11T14:00:52.442Z&timezone=browser&var-URL=$__all&var-interval_value=3&var-data_source=deoi7eicapo1sb&refresh=10s

k6 run -e ENV=nginx-fpm --out influxdb=http://localhost:8086/k6 /home/mamam/dev/web-performance/k6-script/scripts/post-weight-flow-scri
pt.js

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
    ✓ 'p(90)<3000' p(90)=50.53ms

    http_req_duration{name:post_weight_get}
    ✓ 'p(90)<1000' p(90)=20.69ms

    http_req_failed
    ✓ 'rate<0.001' rate=0.00%


  █ TOTAL RESULTS

    checks_total.......................: 7485    30.418329/s
    checks_succeeded...................: 100.00% 7485 out of 7485
    checks_failed......................: 0.00%   0 out of 7485

    ✓ POST status is 200
    ✓ GET status is 200
    ✓ GET post has correct ID

    HTTP
    http_req_duration.........................................................: avg=17.41ms min=9.2ms   med=14.96ms max=749.88ms p(90)=25.54ms p(95)=36.09ms
      { expected_response:true }..............................................: avg=17.41ms min=9.2ms   med=14.96ms max=749.88ms p(90)=25.54ms p(95)=36.09ms
      { name:post_weight_create }.............................................: avg=38.72ms min=22.12ms med=37.55ms max=118.06ms p(90)=50.53ms p(95)=54.15ms
      { name:post_weight_get }................................................: avg=15.45ms min=9.2ms   med=14.2ms  max=749.88ms p(90)=20.69ms p(95)=22.72ms
    http_req_failed...........................................................: 0.00%  0 out of 6904
    http_reqs.................................................................: 6904   28.0572/s

    EXECUTION
    iteration_duration........................................................: avg=2.29s   min=2s      med=2.01s   max=5.14s    p(90)=2.03s   p(95)=5.05s
    iterations................................................................: 6323   25.696072/s
    vus.......................................................................: 2      min=1         max=80
    vus_max...................................................................: 80     min=80        max=80

    NETWORK
    data_received.............................................................: 56 MB  228 kB/s
    data_sent.................................................................: 1.2 MB 4.8 kB/s