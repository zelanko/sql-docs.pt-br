
3. Em ambos os nós de cluster, abra as portas de firewall do Pacemaker. Para abrir essas portas com o `firewalld`, execute o seguinte comando:

   ```bash
   sudo firewall-cmd --permanent --add-service=high-availability
   sudo firewall-cmd --reload
   ```

   > Se você estiver usando outro firewall que não tenha uma configuração de alta disponibilidade interna, as portas a seguir precisarão ser abertas para que o Pacemaker seja capaz de se comunicar com outros nós no cluster
   >
   > * TCP: portas 2224, 3121, 21064
   > * UDP: porta 5405

1. Instale os pacotes do Pacemaker em cada nó.

   ```bash
   sudo yum install pacemaker pcs fence-agents-all resource-agents
   ```

   

2. Defina a senha para o usuário padrão criado ao instalar pacotes do Pacemaker e do Corosync. Use a mesma senha em ambos os nós. 

   ```bash
   sudo passwd hacluster
   ```

   

3. Habilite e inicie o serviço `pcsd` e o Pacemaker. Isso permitirá que os nós reingressem no cluster após a reinicialização. Execute o comando a seguir em ambos os nós.

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   sudo systemctl enable pacemaker
   ```

4. Crie o cluster. Para criar o cluster, execute o seguinte comando:

   ```bash
   sudo pcs cluster auth <node1> <node2> <node3> -u hacluster -p <password for hacluster>
   sudo pcs cluster setup --name <clusterName> <node1> <node2> <node3> 
   sudo pcs cluster start --all
   ```
   
   >[!NOTE]
   >Se você tiver configurado um cluster anteriormente nos mesmos nós, você precisará usar a opção '-force' ao executar 'pcs cluster setup'. Observe que isso é equivalente à execução de 'pcs cluster destroy' e o serviço pacemaker precisa ser reabilitado usando 'sudo systemctl enable pacemaker'.

5. Instalar o agente do recurso SQL Server para o SQL Server. Execute os comandos a seguir em ambos os nós. 

   ```bash
   sudo yum install mssql-server-ha
   ```
