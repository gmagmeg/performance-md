http://localhost:3000/d/ReuNR5Aik/k6-dashboard?orgId=1&from=2025-07-11T12:15:44.614Z&to=2025-07-11T12:16:32.397Z&timezone=browser&var-URL=$__all&var-interval_value=3&var-data_source=deoi7eicapo1sb&refresh=10s

k6 run -e ENV=apache-php --out influxdb=http://localhost:8086/k6 /home/mamam/dev/web-performance/k6-script/spike-script/spike-script.js

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
    ✓ 'p(95)<2000' p(95)=1.68s

    http_req_failed
    ✓ 'rate<0.01' rate=0.00%


  █ TOTAL RESULTS

    checks_total.......................: 4611   107.689867/s
    checks_succeeded...................: 98.91% 4561 out of 4611
    checks_failed......................: 1.08%  50 out of 4611

    ✓ GET status is 200
    ✓ GET response has data
    ✗ GET response time < 5000ms
      ↳  96% — ✓ 1487 / ✗ 50

    HTTP
    http_req_duration.......................................................: avg=436.89ms min=13.87ms med=26.23ms max=11.3s  p(90)=68.92ms p(95)=1.68s
      { expected_response:true }............................................: avg=436.89ms min=13.87ms med=26.23ms max=11.3s  p(90)=68.92ms p(95)=1.68s
    http_req_failed.........................................................: 0.00%  0 out of 1537
    http_reqs...............................................................: 1537   35.896622/s

    EXECUTION
    iteration_duration......................................................: avg=2.42s    min=1.01s   med=2.03s   max=14.31s p(90)=3.03s   p(95)=3.7s
    iterations..............................................................: 1537   35.896622/s
    vus.....................................................................: 2      min=0         max=200
    vus_max.................................................................: 200    min=200       max=200

    NETWORK
    data_received...........................................................: 75 MB  1.8 MB/s
    data_sent...............................................................: 173 kB 4.0 kB/s