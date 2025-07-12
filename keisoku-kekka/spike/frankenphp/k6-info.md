http://localhost:3000/d/ReuNR5Aik/k6-dashboard?orgId=1&from=2025-07-11T23:23:42.806Z&to=2025-07-11T23:24:28.907Z&timezone=browser&var-URL=$__all&var-interval_value=3&var-data_source=deoi7eicapo1sb&refresh=10s

k6 run -e ENV=frankenphp --out influxdb=http://localhost:8086/k6 /home/mamam/dev/web-performance/k6-script/spike-script/spike-script.js

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
    ✓ 'p(95)<2000' p(95)=21.44ms

    http_req_failed
    ✓ 'rate<0.01' rate=0.00%


  █ TOTAL RESULTS

    checks_total.......................: 5013    118.384365/s
    checks_succeeded...................: 100.00% 5013 out of 5013
    checks_failed......................: 0.00%   0 out of 5013

    ✓ GET status is 200
    ✓ GET response has data
    ✓ GET response time < 5000ms

    HTTP
    http_req_duration.......................................................: avg=14.56ms min=10.25ms med=13.44ms max=36.87ms p(90)=18.9ms p(95)=21.44m
      { expected_response:true }............................................: avg=14.56ms min=10.25ms med=13.44ms max=36.87ms p(90)=18.9ms p(95)=21.44m
    http_req_failed.........................................................: 0.00%  0 out of 1671
    http_reqs...............................................................: 1671   39.461455/s

    EXECUTION
    iteration_duration......................................................: avg=2.02s   min=1.01s   med=2.01s   max=3.04s   p(90)=3.01s  p(95)=3.01s
    iterations..............................................................: 1671   39.461455/s
    vus.....................................................................: 4      min=0         max=199
    vus_max.................................................................: 200    min=200       max=200

    NETWORK
    data_received...........................................................: 82 MB  1.9 MB/s
    data_sent...............................................................: 187 kB 4.4 kB/s