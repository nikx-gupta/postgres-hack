# postgres-hack
1. Setting up Postgres DB Cluster using Kubegres
   - Refer [Url](https://www.kubegres.io/doc/getting-started.html)
2. As Db is running on ClusterIP we need to add below port forwarding in to local machine
   - Here "10.1.232.136" is the POD or service ClusterIP. Use "kubectl describe service postrgres-server"
   - Here "192.168.1.31" refers to local machine IP address
   - Use "-D" in place of "-A" to delete the route
   ```bash
   sudo iptables -t nat -A PREROUTING -j DNAT -d 192.168.1.31 -p tcp --dport 5432 --to 10.1.232.136
   ```
 3. Deploy ARM Template 
   ```bash
   az deployment group create -g rgdf -n nikxpgdeploy --template-file azure_app_with_db.json
   ```

References
1. [kubegres Github](https://github.com/reactive-tech/kubegres)
 
