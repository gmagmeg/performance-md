http://localhost:3000/d/ReuNR5Aik/k6-dashboard?orgId=1&from=2025-07-11T23:09:10.462Z&to=2025-07-11T23:13:38.001Z&timezone=browser&var-URL=$__all&var-interval_value=3&var-data_source=deoi7eicapo1sb&refresh=10s

k6 run -e ENV=frankenphp --out influxdb=http://localhost:8086/k6 /home/mamam/dev/web-performance/k6-script/scripts/post-weight-flow-script.js

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
    ✓ 'p(90)<3000' p(90)=45.86ms

    http_req_duration{name:post_weight_get}
    ✓ 'p(90)<1000' p(90)=15.48ms

    http_req_failed
    ✓ 'rate<0.001' rate=0.00%


  █ TOTAL RESULTS

    checks_total.......................: 7492    31.048766/s
    checks_succeeded...................: 100.00% 7492 out of 7492
    checks_failed......................: 0.00%   0 out of 7492

    ✓ GET status is 200
    ✓ POST status is 200
    ✓ GET post has correct ID

    HTTP
    http_req_duration.........................................................: avg=12.74ms min=5.22ms  med=10.41ms max=95.05ms p(90)=19.51ms p(95)=32.39ms
      { expected_response:true }..............................................: avg=12.74ms min=5.22ms  med=10.41ms max=95.05ms p(90)=19.51ms p(95)=32.39ms
      { name:post_weight_create }.............................................: avg=35.06ms min=18.53ms med=33.92ms max=95.05ms p(90)=45.86ms p(95)=49.37ms
      { name:post_weight_get }................................................: avg=10.7ms  min=5.22ms  med=9.79ms  max=72.11ms p(90)=15.48ms p(95)=16.8ms
    http_req_failed...........................................................: 0.00%  0 out of 6913
    http_reqs.................................................................: 6913   28.649242/s

    EXECUTION
    iteration_duration........................................................: avg=2.28s   min=2s      med=2.01s   max=5.3s    p(90)=2.02s   p(95)=5.04s
    iterations................................................................: 6334   26.249718/s
    vus.......................................................................: 1      min=1         max=80
    vus_max...................................................................: 80     min=80        max=80

    NETWORK
    data_received.............................................................: 57 MB  234 kB/s
    data_sent.................................................................: 1.2 MB 4.9 kB/s