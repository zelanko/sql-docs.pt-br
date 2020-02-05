---
title: Implantar um cluster do Pacemaker para o SQL Server em Linux
description: Este tutorial mostra como implantar um cluster do Pacemaker para SQL Server em Linux.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 12/11/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: ee3b4aac2e1bcdcc37de17a569f080d3b9bc87cc
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68077471"
---
# <a name="deploy-a-pacemaker-cluster-for-sql-server-on-linux"></a>Implantar um cluster do Pacemaker para o SQL Server em Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este tutorial documenta as tarefas necessárias para implantar um cluster do Linux Pacemaker para um [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] AG (grupo de disponibilidade) Always On ou uma FCI (instância de cluster de failover). Ao contrário da pilha [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] do Windows Server/ firmemente acoplada, a criação de cluster do Pacemaker e a configuração do AG (grupo de disponibilidade) no Linux podem ser feitas antes ou após a instalação do [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. A integração e a configuração de recursos para a parte do Pacemaker de uma implantação de AG ou FCI são feitas após a configuração do cluster.
> [!IMPORTANT]
> Um AG com um tipo de cluster None *não* requer um cluster do Pacemaker, nem pode ser gerenciado pelo Pacemaker. 

> [!div class="checklist"]
> * Instale o complemento de alta disponibilidade e instale o Pacemaker.
> * Prepare os nós para o Pacemaker (somente RHEL e Ubuntu).
> * Crie o cluster do Pacemaker.
> * Instale os pacotes SQL Server HA e SQL Server Agent.
 
## <a name="prerequisite"></a>Pré-requisito
[Instalar o SQL Server 2017](sql-server-linux-setup.md).

## <a name="install-the-high-availability-add-on"></a>Instalar o complemento de alta disponibilidade
Use a sintaxe a seguir para instalar os pacotes que compõem o complemento de HA (alta disponibilidade) para cada distribuição do Linux. 

**Red Hat Enterprise Linux (RHEL)**
1.  Registre o servidor usando a sintaxe a seguir. Você é solicitado a informar um nome de usuário e uma senha válidos.
    
    ```bash
    sudo subscription-manager register
    ```
    
2.  Liste os pools disponíveis para registro.
    
    ```bash
    sudo subscription-manager list --available
    ```

3.  Execute o comando a seguir para associar a alta disponibilidade do RHEL à assinatura
    
    ```bash
    sudo subscription-manager attach --pool=<PoolID>
    ```
    
    em que *PoolId* é a ID do pool para a assinatura de alta disponibilidade da etapa anterior.
    
4.  Habilite o repositório para poder usar o complemento de alta disponibilidade.
    
    ```bash
    sudo subscription-manager repos --enable=rhel-ha-for-rhel-7-server-rpms
    ```
    
5.  Instale o pacemaker.
    
    ```bash
    sudo yum install pacemaker pcs fence-agents-all resource-agents
    ```

**Ubuntu**

```bash
sudo apt-get install pacemaker pcs fence-agents resource-agents
```

**SUSE Linux Enterprise Server (SLES)**

Instale o padrão de Alta Disponibilidade no YaST ou faça isso como parte da instalação principal do servidor. A instalação pode ser feita com um ISO/DVD como uma origem ou colocando-o online.
> [!NOTE]
> No SLES, o complemento de HA é inicializado quando o cluster é criado.

## <a name="prepare-the-nodes-for-pacemaker-rhel-and-ubuntu-only"></a>Prepare os nós para o Pacemaker (somente RHEL e Ubuntu)
O próprio Pacemaker usa um usuário criado na distribuição chamada *hacluster*. O usuário é criado quando o complemento de HA é instalado no RHEL e no Ubuntu.
1. Em cada servidor que atuará como um nó do cluster do Pacemaker, crie a senha para um usuário a ser usado pelo cluster. O nome usado nos exemplos é *hacluster*, mas qualquer nome pode ser usado. O nome e a senha devem ser os mesmos em todos os nós que participam do cluster do Pacemaker.
   
    ```bash
    sudo passwd hacluster
    ```
    
2. Em cada nó que fará parte do cluster do Pacemaker, habilite e inicie o serviço `pcsd` com os seguintes comandos (RHEL e Ubuntu):

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   ```
   
   Em seguida, execute
   
   ```bash
   sudo systemctl status pcsd
   ```
   
   para garantir que o `pcsd` seja iniciado.
3. Habilite o serviço do Pacemaker em cada nó possível do cluster do Pacemaker.
   
   ```bash
   sudo systemctl start pacemaker
   ```

   No Ubuntu, você verá um erro:
   
   *o Pacemaker Default-Start não contém níveis de execução, anulando.*
   
   Esse erro é um problema conhecido. Apesar do erro, a habilitação do serviço Pacemaker é bem-sucedida e esse bug será corrigido em algum momento no futuro.
   
4. Em seguida, crie e inicie o cluster do Pacemaker. Há uma diferença entre o RHEL e o Ubuntu nesta etapa. Enquanto estiver em ambas as distribuições, instalar o `pcs` configura um arquivo de configuração padrão para o cluster do Pacemaker, no RHEL, a execução desse comando destrói qualquer configuração existente e cria um novo cluster.

<a id="create"></a>
## <a name="create-the-pacemaker-cluster"></a>Criar o cluster do Pacemaker 
Esta seção documenta como criar e configurar o cluster para cada distribuição do Linux.

**RHEL**

1. Autorizar os nós
   
   ```bash
   sudo pcs cluster auth <Node1 Node2 ... NodeN> -u hacluster
   ```
   
   em que *NodeX* é o nome do nó.
2. Criar o cluster
   
   ```bash
   sudo pcs cluster setup --name <PMClusterName Nodelist> --start --all --enable
   ```
   
   em que *PMClusterName* é o nome atribuído ao cluster do Pacemaker e *NodeList* é a lista de nomes dos nós separados por um espaço.

**Ubuntu**

Configurar o Ubuntu é semelhante ao RHEL. No entanto, há uma grande diferença: instalar os pacotes do Pacemaker cria uma configuração de base para o cluster e habilita e inicia o `pcsd`. Se você tentar configurar o cluster do Pacemaker seguindo exatamente as instruções do RHEL, receberá um erro. Para corrigir esse problema, execute as seguintes etapas: 
1. Remova a configuração padrão do Pacemaker de cada nó.
   
   ```bash
   sudo pcs cluster destroy
   ```
   
2. Siga as etapas na seção do RHEL para criar o cluster do Pacemaker.

**SLES**

O processo para criar um cluster do Pacemaker é completamente diferente no SLES do que no RHEL e no Ubuntu. As etapas a seguir documentam como criar um cluster com o SLES.
1. Inicie o processo de configuração de cluster executando 
   ```bash
   sudo ha-cluster-init
   ``` 
   
   em um dos nós. Talvez você seja avisado de que o NTP não está configurado e que nenhum dispositivo watchdog foi encontrado. Isso está bem para colocar tudo em funcionamento. O watchdog está relacionado a STONITH se você usa o isolamento interno do SLES que é baseado em armazenamento. O NTP e o watchdog podem ser configurados posteriormente.
   
2. Você será solicitado a configurar o Corosync. Você será solicitado a fornecer o endereço de rede a ser associado, bem como o endereço e a porta de multicast. O endereço de rede é a sub-rede que você está usando; por exemplo, 192.191.190.0. Você pode aceitar os padrões em todos os prompts ou alterar, se necessário.
   
3. Em seguida, será perguntado se você deseja configurar o SBD, que é o isolamento baseado em disco. Essa configuração pode ser feita mais tarde, se desejado. Se o SBD não estiver configurado, ao contrário do RHEL e do Ubuntu, o `stonith-enabled` será definido como false por padrão.
   
4. Por fim, será perguntado se você deseja configurar um endereço IP para administração. Esse endereço IP é opcional, mas funciona de forma semelhante ao endereço IP para um WSFC (cluster de failover do Windows Server), no sentido de que cria um endereço IP no cluster a ser usado para se conectar a ele por meio do HAWK (Konsole da Web de HA). Essa configuração também é opcional.
   
5. Verifique se o cluster está em funcionamento emitindo 
   ```bash
   sudo crm status
   ```
   
6. Altere a senha *hacluster* por 
   ```bash
   sudo passwd hacluster
   ```
   
7. Se você configurou um endereço IP para administração, pode testá-lo em um navegador, que também testa a alteração de senha para *hacluster*.
   ![](./media/sql-server-linux-deploy-pacemaker-cluster/image2.png)
   
8. Em outro servidor SLES que será um nó do cluster, execute 
   ```bash
   sudo ha-cluster-join
   ```
   
9. Quando solicitado, insira o nome ou o endereço IP do servidor que foi configurado como o primeiro nó do cluster nas etapas anteriores. O servidor é adicionado como um nó ao cluster existente.
   
10. Verifique se o nó foi adicionado emitindo 
   ```bash
   sudo crm status
   ```
   
11. Altere a senha *hacluster* por 
   ```bash
   sudo passwd hacluster
   ```
   
12. Repita as Etapas 8-11 para todos os outros servidores serem adicionados ao cluster.

## <a name="install-the-sql-server-ha-and-sql-server-agent-packages"></a>Instale os pacotes SQL Server HA e SQL Server Agent
Use os comandos a seguir para instalar o pacote de HA do SQL Server e o Agente do [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], se ainda não estiverem instalados. Instalar o pacote de HA depois de instalar o [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] requer reiniciar o [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] para que ele seja usado. Estas instruções pressupõem que os repositórios dos pacotes da Microsoft já foram configurados, pois [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] deve estar instalado neste ponto.
> [!NOTE]
> - Se você não usar o [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Agent para envio de logs ou qualquer outro uso, ele não precisará ser instalado, portanto, o pacote *mssql-server-agent* poderá ser ignorado.
> - Os outros pacotes opcionais para o [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] no Linux, Pesquisa de Texto Completo do [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] (*mssql-server-fts*) e [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Integration Services (*mssql-server-is*), não são necessários para alta disponibilidade, seja para uma FCI ou um AG.

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

Neste tutorial, você aprendeu a implantar um cluster do Pacemaker para SQL Server em Linux. Você aprendeu a:
> [!div class="checklist"]
> * Instale o complemento de alta disponibilidade e instale o Pacemaker.
> * Prepare os nós para o Pacemaker (somente RHEL e Ubuntu).
> * Crie o cluster do Pacemaker.
> * Instale os pacotes SQL Server HA e SQL Server Agent.

Para criar e configurar um grupo de disponibilidade para SQL Server em Linux, confira:

> [!div class="nextstepaction"]
> [Criar e configurar um grupo de disponibilidade para SQL Server em Linux](sql-server-linux-create-availability-group.md).

