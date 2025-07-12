http://localhost:3000/d/ReuNR5Aik/k6-dashboard?orgId=1&from=2025-07-11T11:27:46.650Z&to=2025-07-11T11:32:00.000Z&timezone=browser&var-URL=$__all&var-interval_value=3&var-data_source=deoi7eicapo1sb&refresh=10s


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
    ✓ 'p(90)<3000' p(90)=49.61ms

    http_req_duration{name:post_weight_get}
    ✓ 'p(90)<1000' p(90)=22.45ms

    http_req_failed
    ✓ 'rate<0.001' rate=0.00%


  █ TOTAL RESULTS

    checks_total.......................: 7465    30.854148/s
    checks_succeeded...................: 100.00% 7465 out of 7465
    checks_failed......................: 0.00%   0 out of 7465

    ✓ GET status is 200
    ✓ POST status is 200
    ✓ GET post has correct ID

    HTTP
    http_req_duration.........................................................: avg=18.46ms min=9.7ms   med=16.29ms max=154.88ms p(90)=27.99ms p(95)=36.91ms
      { expected_response:true }..............................................: avg=18.46ms min=9.7ms   med=16.29ms max=154.88ms p(90)=27.99ms p(95)=36.91ms
      { name:post_weight_create }.............................................: avg=39.96ms min=22.61ms med=38.71ms max=154.88ms p(90)=49.61ms p(95)=53.78ms
      { name:post_weight_get }................................................: avg=16.51ms min=9.7ms   med=15.59ms max=101ms    p(90)=22.45ms p(95)=25.14ms
    http_req_failed...........................................................: 0.00%  0 out of 6892
    http_reqs.................................................................: 6892   28.485839/s

    EXECUTION
    iteration_duration........................................................: avg=2.29s   min=2.01s   med=2.01s   max=5.18s    p(90)=2.03s   p(95)=5.05s
    iterations................................................................: 6319   26.11753/s
    vus.......................................................................: 1      min=1         max=80
    vus_max...................................................................: 80     min=80        max=80

    NETWORK
    data_received.............................................................: 56 MB  231 kB/s
    data_sent.................................................................: 1.2 MB 4.9 kB/s