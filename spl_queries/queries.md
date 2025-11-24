# SIMPLE SPL CHEAT SHEET (copy & paste)

# 1) Top client IPs (who connects most)
source="access.log" | top clientip

# 2) Add-to-cart events as a clean table (time, IP, product)
source="access.log" "action=addtocart" | table req_time, clientip, productId

# 3) Count events per client IP for host nginx
host=nginx | stats count by clientip

# 4) Count occurrences of each source IP in secure logs
source="secure.log" | stats count by src

# 5) Same top client IPs again (quick reminder)
source="access.log" | top clientip

# 6) Geo count of secure.log source IPs (needs iplocation enabled)
source="secure.log" | iplocation src | stats count by Country

# 7) Top productId (which product appears most)
source="access.log" | top productId

# 8) Error count (status >= 400)
source="access.log" | rex "(?<status>\d{3})" | where status >= 400 | stats count by status

# 9) Requests over time (small time buckets)
source="access.log" | timechart span=30m count AS requests

# 10) Show full raw events (quick look)
source="access.log" | head 20
