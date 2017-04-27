1. **Em ambos os nós de cluster, crie um arquivo para armazenar o nome de usuário do SQL Server e a senha para o logon do Pacemaker**. O comando a seguir cria e popula este arquivo:

    ```bash
    sudo touch /var/opt/mssql/secrets/passwd
    sudo echo '<loginName>' >> /var/opt/mssql/secrets/passwd
    sudo echo '<loginPassword>' >> /var/opt/mssql/secrets/passwd
    sudo chown root:root /var/opt/mssql/secrets/passwd 
    sudo chmod 600 /var/opt/mssql/secrets/passwd
    ```
2. **Todos os nós de cluster devem ser capazes de acessar um ao outro via SSH**. Ferramentas como hb_report ou crm_report (para solução de problemas) e Gerenciador de histórico do Hawk exigem acesso SSH sem senha entre os nós, caso contrário, eles podem apenas coletar dados do nó atual. No caso de você usar uma porta SSH não padrão, use a opção -X (consulte a página do manual). Por exemplo, se a porta SSH é 3479, invoque um hb_report com:

    ```bash
    crm_report -X "-p 3479" [...]
    ```

    Para obter mais informações, consulte [Requisitos de sistema e as recomendações na documentação do SUSE](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_requirements_other.html).

3. **Instalar a extensão de Alta Disponibilidade**. Para instalar a extensão, siga as etapas no tópico SUSE a seguir:
    
    [Início rápido de instalação e configuração](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html)

4. **Instalar o agente do recurso FCI para SQL Server**. Execute os seguintes comandos em ambos os nós:

    ```bash
    sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server.repo
    sudo zypper --gpg-auto-import-keys refresh
    sudo zypper install mssql-server-ha
    ```

5. **Configure automaticamente o primeiro nó**. A próxima etapa é configurar um cluster de um nó em execução por meio da configuração do primeiro nó, SLES1. Siga as instruções no tópico SUSE, [Configurando o primeiro nó](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.setup.1st-node).

    Quando terminar, verifique o status do cluster com `crm status`:
    ```bash
    crm status
    ```

    Ele deve mostrar que esse único nó, SLES1, está configurado.

6. **Adicionar nós a um cluster existente**. Em seguida, adicione o nó SLES2 ao cluster. Siga as instruções no tópico SUSE, [Adicionar o segundo nó](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.setup.2nd-node).
    
    Quando terminar, verifique o status do cluster com **crm status**. Se você tiver adicionado um segundo nó, a saída será semelhante ao seguinte:
        
    ```
    2 nodes configured
    1 resource configured
    Online: [ SLES1 SLES2 ]
    Full list of resources:
    admin_addr     (ocf::heartbeat:IPaddr2):       Started SLES1
    ```

    > [!NOTE]
    > **admin_addr** é o recurso de cluster de IP virtual que é configurado durante a configuração do cluster inicial de um nó.

7.    **Procedimentos de remoção**. Se você precisar remover um nó do cluster, use o script de inicialização **ha-cluster-remove**. Para obter mais informações, consulte [visão geral dos Scripts de inicialização](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.bootstrap).  

