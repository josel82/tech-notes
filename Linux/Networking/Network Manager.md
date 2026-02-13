
Adding a route
```bash
# 1. Identify your connection name for ens19 
nmcli connection show 
# 2. Add the route (replace "Wired connection 2" with your actual name) 
sudo nmcli connection modify "Wired connection 2" +ipv4.routes "224.0.0.0/4" 
# 3. Apply the change 
sudo nmcli connection up "Wired connection 2"
```