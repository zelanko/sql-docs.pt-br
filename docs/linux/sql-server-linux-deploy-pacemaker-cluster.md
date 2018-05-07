---
title: Implantar um cluster de Pacemaker para o SQL Server no Linux | Microsoft Docs
description: Este tutorial mostra como implantar um cluster Pacemaker para SQL Server no Linux.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 12/11/2017
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.openlocfilehash: b97c727573e85c58ffea33656e3829b17455a12f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="deploy-a-pacemaker-cluster-for-sql-server-on-linux"></a>Implantar um cluster de Pacemaker para o SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este tutorial documenta as tarefas necessárias para implantar um cluster Linux Pacemaker para um [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] sempre no grupo de disponibilidade (AG) ou instância de cluster de failover (FCI). Ao contrário do Windows Server firmemente acoplado /[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] pilha, criação de cluster Pacemaker, bem como configuração de grupo (AG) de disponibilidade no Linux pode ser feita antes ou após a instalação do [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. A integração e a configuração de recursos para a parte Pacemaker de uma implantação de grupo de disponibilidade ou FCI é feito depois que o cluster é configurado.
> [!IMPORTANT]
> Um grupo de disponibilidade com um tipo de cluster de None *não* requer que um cluster Pacemaker e não podem ser gerenciado por Pacemaker. 

> [!div class="checklist"]
> * Instalar o complemento de alta disponibilidade e Pacemaker.
> * Prepare os nós de Pacemaker (RHEL e Ubuntu somente).
> * Crie o cluster Pacemaker.
> * Instale os pacotes de HA do SQL Server e SQL Server Agent.
 
## <a name="prerequisite"></a>Pré-requisito
[Instalar o SQL Server de 2017](sql-server-linux-setup.md).

## <a name="install-the-high-availability-add-on"></a>Instalar o suplemento de alta disponibilidade
Use a sintaxe a seguir para instalar os pacotes que compõem o complemento de alta disponibilidade (HA) para cada distribuição de Linux. 

**Red Hat Enterprise Linux (RHEL)**
1.  Registre o servidor usando a sintaxe a seguir. Você será solicitado um nome de usuário válido e senha.
    
    ```bash
    sudo subscription-manager register
    ```
    
2.  Lista os pools disponíveis para registro.
    
    ```bash
    sudo subscription-manager list --available
3.  Run the following command to associate RHEL high availability with the subscription
    
    ```bash
    sudo subscription-manager attach --pool=<PoolID>
    ```
    
    onde *PoolId* é a ID do pool para a assinatura de alta disponibilidade da etapa anterior.
    
4.  Habilite o repositório poder usar o complemento de alta disponibilidade.
    
    ```bash
    sudo subscription-manager repos --enable=rhel-ha-for-rhel-7-server-rpms
    ```
    
5.  Instale Pacemaker.
    
    ```bash
    sudo yum install pacemaker pcs fence-agents-all resource-agents
    ```

**Ubuntu**

```bash
sudo apt-get install pacemaker pcs fence-agents resource-agents
```

**SUSE Linux Enterprise Server (SLES)**

Instale o padrão de alta disponibilidade YaST ou fazê-lo como parte da instalação do servidor principal. A instalação pode ser feita com um ISO/DVD como uma fonte ou obtendo-on-line.
> [!NOTE]
> Em SLES, o complemento de alta disponibilidade é inicializado quando o cluster é criado.

## <a name="prepare-the-nodes-for-pacemaker-rhel-and-ubuntu-only"></a>Preparar os nós de Pacemaker (RHEL e Ubuntu apenas)
Pacemaker próprio usa um usuário criado na distribuição chamada *hacluster*. O usuário é criado quando o complemento de alta disponibilidade é instalado em RHEL e Ubuntu.
1. Em cada servidor que servirá como um nó do cluster Pacemaker, crie a senha para um usuário a ser usado pelo cluster. O nome usado nos exemplos é *hacluster*, mas qualquer nome pode ser usado. O nome e a senha devem ser a mesma em todos os nós que participam no cluster Pacemaker.
   
    ```bash
    sudo passwd hacluster
    ```
    
2. Em cada nó que fará parte do cluster Pacemaker, habilitar e iniciar o `pcsd` serviço com os seguintes comandos (RHEL e Ubuntu):

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   ```
   
   Em seguida, execute
   
   ```bash
   sudo systemctl status pcsd
   ```
   
   para garantir que `pcsd` é iniciado.
3. Habilite o serviço Pacemaker em cada nó do cluster Pacemaker de possíveis.
   
   ```bash
   sudo systemctl start pacemaker
   ```

   No Ubuntu, você vir um erro:
   
   *pacemaker início padrão não contém nenhum runlevels, anulando.*
   
   Esse erro é um problema conhecido. Apesar do erro, habilitando o serviço Pacemaker for bem-sucedida, e esse bug será corrigido em algum momento no futuro.
   
4. Em seguida, crie e inicie o cluster Pacemaker. Há uma diferença entre RHEL e Ubuntu nesta etapa. Em ambas as distribuições, instalando `pcs` configura um arquivo de configuração padrão para o cluster Pacemaker, RHEL, a execução desse comando destrói qualquer configuração existente e cria um novo cluster.

<a id="create"></a>
## <a name="create-the-pacemaker-cluster"></a>Criar o cluster Pacemaker 
Esta seção documenta como criar e configurar o cluster para cada distribuição de Linux.

**RHEL**

1. Autorizar os nós
   
   ```bash
   sudo pcs cluster auth <Node1 Node2 … NodeN> -u hacluster
   ```
   
   onde *NodeX* é o nome do nó.
2. Criar o cluster
   
   ```bash
   sudo pcs cluster setup --name <PMClusterName Nodelist> --start --all --enable
   ```
   
   onde *PMClusterName* é o nome atribuído ao cluster Pacemaker e *Nodelist* é a lista de nomes de nós separados por um espaço.

**Ubuntu**

Configurar Ubuntu é semelhante ao RHEL. No entanto, há uma grande diferença: instalar os pacotes Pacemaker cria uma configuração de base para o cluster e habilita e inicia `pcsd`. Se você tentar configurar o cluster Pacemaker seguindo as instruções do RHEL exatamente, você receberá um erro. Para corrigir esse problema, execute as seguintes etapas: 
1. Remova a configuração de Pacemaker padrão de cada nó.
   
   ```bash
   sudo pcs cluster destroy
   ```
   
2. Siga as etapas na seção RHEL para criar o cluster Pacemaker.

**SLES**

O processo para criar um cluster Pacemaker é completamente diferente em SLES em RHEL e Ubuntu. As etapas a seguir documentam como criar um cluster com SLES.
1. Inicie o processo de configuração de cluster, executando 
   ```bash
   sudo ha-cluster-init
   ``` 
   
   em um de nós. Você pode ser solicitado que o NTP não está configurado e que não há nenhum dispositivo de watchdog foi encontrado. Isso é bom para colocar as coisas em execução. Watchdog está relacionado a STONITH se você usar o isolamento de internos do SLES baseado em armazenamento. NTP e watchdog podem ser configuradas mais tarde.
   
2. Você precisará configurar Corosync. Você será solicitado para o endereço de rede associar, bem como o endereço de multicast e a porta. O endereço de rede é a sub-rede que você está usando; Por exemplo, 192.191.190.0. Você pode aceitar os padrões em cada prompt ou altere se necessário.
   
3. Em seguida, você será solicitado se deseja configurar SBD, que é o isolamento com base em disco. Essa configuração pode ser feita posteriormente, se desejado. Se SBD não estiver configurado, diferentemente em RHEL e Ubuntu, `stonith-enabled` será por padrão definido como false.
   
4. Por fim, você será solicitado se deseja configurar um endereço IP para administração. Esse endereço IP é opcional, mas funções semelhante para o endereço IP de um cluster de failover do Windows Server (WSFC) no sentido de que ele cria um endereço IP do cluster a ser usado para se conectar a ele por meio de HA Web Konsole (HAWK). Essa configuração também é opcional.
   
5. Certifique-se de que o cluster está em execução, emitindo 
   ```bash
   sudo crm status
   ```
   
6. Alterar o *hacluster* senha com 
   ```bash
   sudo passwd hacluster
   ```
   
7. Se você tiver configurado um endereço IP para a administração, você pode testá-lo em um navegador, que também testa a alteração da senha *hacluster*.
   ![](./media/sql-server-linux-deploy-pacemaker-cluster/image2.png)
   
8. Em outro servidor SLES será um nó do cluster, execute 
   ```bash
   sudo ha-cluster-join
   ```
   
9. Quando solicitado, insira o nome ou endereço IP do servidor que foi configurado como o primeiro nó do cluster nas etapas anteriores. O servidor é adicionado como um nó ao cluster existente.
   
10. Verifique se que o nó foi adicionado ao emitir 
   ```bash
   sudo crm status
   ```
   
11. Alterar o *hacluster* senha com 
   ```bash
   sudo passwd hacluster
   ```
   
12. Repita as etapas 8 a 11 para todos os outros servidores a serem adicionados ao cluster.

## <a name="install-the-sql-server-ha-and-sql-server-agent-packages"></a>Instalar os pacotes de HA do SQL Server e SQL Server Agent
Use os seguintes comandos para instalar o pacote de HA do SQL Server e [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] agente, se eles não estiverem instalados. Instalando o pacote de alta disponibilidade depois de instalar [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] requer a reinicialização do [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] para ser usado. Essas instruções pressupõem que os repositórios para os pacotes da Microsoft já foram configurados, desde [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] deve ser instalado neste ponto.
> [!NOTE]
> - Se você não usar [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] agente de envio de logs ou qualquer outro uso, ele não tem que ser instalado, portanto pacote *mssql-server-agente* pode ser ignorada.
> - Os pacotes opcionais para [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] no Linux, [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] pesquisa de texto completo (*fts do mssql server*) e [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Integration Services (*mssql servidor é*), não são necessário para alta disponibilidade, para uma FCI ou um grupo de disponibilidade.

**RHEL**

```bash
sudo yum install mssql-server-ha mssql-server-agent
sudo systemctl restart mssql-server
```

**Ubuntu**

```bash
sudo apt-get install mssql-server-ha mssql-server-agent
sudo systemctl restart mssql-server
```

**SLES**

```bash
sudo zypper install mssql-server-ha mssql-server-agent
sudo systemctl restart mssql-server
```

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu como implantar um cluster Pacemaker para SQL Server no Linux. Você aprendeu como para:
> [!div class="checklist"]
> * Instalar o complemento de alta disponibilidade e Pacemaker.
> * Prepare os nós de Pacemaker (RHEL e Ubuntu somente).
> * Crie o cluster Pacemaker.
> * Instale os pacotes de HA do SQL Server e SQL Server Agent.

Para criar e configurar um grupo de disponibilidade para o SQL Server no Linux, consulte:

> [!div class="nextstepaction"]
> [Criar e configurar um grupo de disponibilidade para o SQL Server no Linux](sql-server-linux-create-availability-group.md).

