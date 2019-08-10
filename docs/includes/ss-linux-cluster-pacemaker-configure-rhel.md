---
ms.openlocfilehash: 6cf3dd279f33ea0c157743d4b4c11248267a0a62
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68215622"
---
3. Em todos os nós de cluster, abra as portas do firewall do Pacemaker. Para abrir essas portas com o `firewalld`, execute o seguinte comando:

   ```bash
   sudo firewall-cmd --permanent --add-service=high-availability
   sudo firewall-cmd --reload
   ```

   > Se o firewall não tiver uma configuração de alta disponibilidade interna, abra as portas do Pacemaker a seguir.
   >
   > * TCP: Portas 2224, 3121 e 21064
   > * UDP: Porta 5405

1. Instale os pacotes do Pacemaker em todos os nós.

   ```bash
   sudo yum install pacemaker pcs fence-agents-all resource-agents
   ```

2. Defina a senha do usuário padrão criado ao instalar pacotes do Pacemaker e do Corosync. Use a mesma senha em todos os nós. 

   ```bash
   sudo passwd hacluster
   ```

3. Para que os nós reingressem no cluster após a reinicialização, habilite e inicie o serviço `pcsd` e o Pacemaker. Execute o seguinte comando em todos os nós.

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
   sudo pcs cluster enable --all
   ```
   
   >[!NOTE]
   >Se você tiver configurado um cluster anteriormente nos mesmos nós, será necessário usar a opção `--force` ao executar `pcs cluster setup`. Essa opção é equivalente a executar o `pcs cluster destroy`. Para reabilitar o Pacemaker, execute o `sudo systemctl enable pacemaker`.

5. Instalar o agente do recurso SQL Server para o SQL Server. Execute os seguintes comandos em todos os nós. 

   ```bash
   sudo yum install mssql-server-ha
   ```
