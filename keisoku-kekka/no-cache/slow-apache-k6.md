http://localhost:3000/d/ReuNR5Aik/k6-dashboard?orgId=1&from=2025-07-11T05:09:11.369Z&to=2025-07-11T05:13:52.753Z&timezone=browser&var-URL=$__all&var-interval_value=3&var-data_source=deoi7eicapo1sb&refresh=10s


    k6 run -e ENV=apache-php --out influxdb=http://localhost:8086/k6 /home/mamam/dev/web-performance/k6-script/scripts/post-weight-flow-script.js

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
    ✓ 'p(90)<3000' p(90)=146.59ms

    http_req_duration{name:post_weight_get}
    ✓ 'p(90)<1000' p(90)=115.28ms

    http_req_failed
    ✓ 'rate<0.001' rate=0.00%


  █ TOTAL RESULTS

    checks_total.......................: 7219    29.420532/s
    checks_succeeded...................: 100.00% 7219 out of 7219
    checks_failed......................: 0.00%   0 out of 7219

    ✓ GET status is 200
    ✓ POST status is 200
    ✓ GET post has correct ID

    HTTP
    http_req_duration.........................................................: avg=90.31ms  min=62.79ms med=84.35ms  max=676.33ms p(90)=119.35ms p(95)=130.59ms
      { expected_response:true }..............................................: avg=90.31ms  min=62.79ms med=84.35ms  max=676.33ms p(90)=119.35ms p(95)=130.59ms
      { name:post_weight_create }.............................................: avg=117.03ms min=80.27ms med=110.04ms max=676.33ms p(90)=146.59ms p(95)=157.85ms
      { name:post_weight_get }................................................: avg=87.86ms  min=62.79ms med=81.94ms  max=653.09ms p(90)=115.28ms p(95)=125.56ms
    http_req_failed...........................................................: 0.00%  0 out of 6660
    http_reqs.................................................................: 6660   27.142367/s

    EXECUTION
    iteration_duration........................................................: avg=2.37s    min=2.06s   med=2.08s    max=5.36s    p(90)=2.14s    p(95)=5.19s
    iterations................................................................: 6101   24.864201/s
    vus.......................................................................: 1      min=1         max=80
    vus_max...................................................................: 80     min=80        max=80

    NETWORK
    data_received.............................................................: 54 MB  220 kB/s
    data_sent.................................................................: 1.1 MB 4.7 kB/s