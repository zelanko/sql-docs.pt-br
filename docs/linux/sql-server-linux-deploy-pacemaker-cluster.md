---
title: Implantar um cluster Pacemaker para o SQL Server no Linux | Microsoft Docs
description: Este tutorial mostra como implantar um cluster Pacemaker para o SQL Server no Linux.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 12/11/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.openlocfilehash: 49f5e3fd6250d3a9bb20ff68927bc66fa1e5d426
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53211535"
---
# <a name="deploy-a-pacemaker-cluster-for-sql-server-on-linux"></a>Implantar um cluster Pacemaker para o SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este tutorial documenta as tarefas necessárias para implantar um cluster Linux Pacemaker para um [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] sempre no grupo de disponibilidade (AG) ou instância de cluster de failover (FCI). Ao contrário do Windows Server firmemente acoplado / [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] pilha, a criação do cluster Pacemaker, bem como configuração de AG (grupo) de disponibilidade no Linux pode ser feita antes ou após a instalação do [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. A integração e a configuração de recursos por uma parte de uma implantação do grupo de disponibilidade ou FCI Pacemaker é feito depois que o cluster é configurado.
> [!IMPORTANT]
> Um grupo de disponibilidade com um tipo de cluster nenhum faz *não* requer um cluster Pacemaker e não podem ser gerenciado por Pacemaker. 

> [!div class="checklist"]
> * Instalar o complemento de alta disponibilidade e Pacemaker.
> * Prepare os nós para Pacemaker (RHEL e somente Ubuntu).
> * Crie o cluster do Pacemaker.
> * Instale os pacotes de HA do SQL Server e SQL Server Agent.
 
## <a name="prerequisite"></a>Pré-requisito
[Instalar o SQL Server 2017](sql-server-linux-setup.md).

## <a name="install-the-high-availability-add-on"></a>Instalar o suplemento de alta disponibilidade
Use a sintaxe a seguir para instalar os pacotes que compõem o complemento de alta disponibilidade (HA) para cada distribuição do Linux. 

**Red Hat Enterprise Linux (RHEL)**
1.  Registre o servidor usando a sintaxe a seguir. Você será solicitado um nome de usuário válido e senha.
    
    ```bash
    sudo subscription-manager register
    ```
    
2.  Liste os pools disponíveis para o registro.
    
    ```bash
    sudo subscription-manager list --available
    ```

3.  Execute o seguinte comando para associar a alta disponibilidade do RHEL com a assinatura
    
    ```bash
    sudo subscription-manager attach --pool=<PoolID>
    ```
    
    em que *PoolId* é a ID do pool para a assinatura de alta disponibilidade da etapa anterior.
    
4.  Habilite o repositório poder usar o complemento de alta disponibilidade.
    
    ```bash
    sudo subscription-manager repos --enable=rhel-ha-for-rhel-7-server-rpms
    ```
    
5.  Instale o Pacemaker.
    
    ```bash
    sudo yum install pacemaker pcs fence-agents-all resource-agents
    ```

**Ubuntu**

```bash
sudo apt-get install pacemaker pcs fence-agents resource-agents
```

**SUSE Linux Enterprise Server (SLES)**

Instalar o padrão de alta disponibilidade no YaST ou fazê-lo como parte da instalação do servidor principal. A instalação pode ser feita com um ISO/DVD, como uma fonte ou obtendo-on-line.
> [!NOTE]
> Em SLES, o complemento de alta disponibilidade é inicializado quando o cluster é criado.

## <a name="prepare-the-nodes-for-pacemaker-rhel-and-ubuntu-only"></a>Preparar os nós para Pacemaker (RHEL e somente Ubuntu)
Pacemaker em si usa um usuário criado na distribuição denominada *hacluster*. O usuário é criado quando o complemento de alta disponibilidade está instalado no RHEL e Ubuntu.
1. Em cada servidor que servirá como um nó do cluster do Pacemaker, crie a senha para um usuário a ser usado pelo cluster. É o nome usado nos exemplos *hacluster*, mas qualquer nome pode ser usado. O nome e a senha devem ser a mesma em todos os nós que participam do cluster do Pacemaker.
   
    ```bash
    sudo passwd hacluster
    ```
    
2. Em cada nó que fará parte do cluster do Pacemaker, habilitar e iniciar o `pcsd` serviço com os seguintes comandos (RHEL e Ubuntu):

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   ```
   
   Em seguida, execute
   
   ```bash
   sudo systemctl status pcsd
   ```
   
   para garantir que `pcsd` é iniciado.
3. Habilite o serviço Pacemaker em cada possível nó do cluster do Pacemaker.
   
   ```bash
   sudo systemctl start pacemaker
   ```

   No Ubuntu, você verá um erro:
   
   *Inicialização padrão do pacemaker não contém nenhum runlevels, anulando.*
   
   Esse erro é um problema conhecido. Apesar do erro, habilitar o serviço Pacemaker for bem-sucedida, e esse bug será corrigido em algum momento no futuro.
   
4. Em seguida, crie e inicie o cluster do Pacemaker. Há uma diferença entre o RHEL e Ubuntu nesta etapa. Embora em ambas as distribuições, instalando `pcs` configura um arquivo de configuração padrão para o cluster do Pacemaker, no RHEL, a execução desse comando destrói qualquer configuração existente e cria um novo cluster.

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
   
   em que *PMClusterName* é o nome atribuído ao cluster do Pacemaker e *Nodelist* é a lista de nomes de nós separados por um espaço.

**Ubuntu**

Configurar o Ubuntu é semelhante ao RHEL. No entanto, há uma grande diferença: instalando pacotes do Pacemaker cria uma configuração de base para o cluster e permite e inicia `pcsd`. Se você tentar configurar o cluster do Pacemaker, seguindo as instruções RHEL exatamente, você obterá um erro. Para corrigir esse problema, execute as seguintes etapas: 
1. Remova a configuração padrão do Pacemaker em cada nó.
   
   ```bash
   sudo pcs cluster destroy
   ```
   
2. Siga as etapas na seção RHEL para criar o cluster do Pacemaker.

**SLES**

O processo para criar um cluster Pacemaker é completamente diferente em SLES no RHEL e Ubuntu. As etapas a seguir mostram como criar um cluster com SLES.
1. Inicie o processo de configuração de cluster executando 
   ```bash
   sudo ha-cluster-init
   ``` 
   
   em um de nós. Você será solicitado que o NTP não está configurado e que não há nenhum dispositivo de watchdog for encontrado. Isso é ótimo para colocar as coisas em funcionamento. Watchdog está relacionado ao STONITH, se você usar o isolamento de internas do SLES que é baseado no armazenamento. NTP e o watchdog podem ser configurados mais tarde.
   
2. Você precisará configurar Corosync. Você precisará fornecer o endereço de rede para associação, bem como a porta e endereço de multicast. O endereço de rede é a sub-rede que você está usando; Por exemplo, 192.191.190.0. Você pode aceitar os padrões em cada prompt ou altere se necessário.
   
3. Em seguida, será perguntado se você deseja configurar SBD, que é o isolamento com base em disco. Essa configuração pode ser feita mais tarde, se desejado. Se SBD não estiver configurado, ao contrário em RHEL e Ubuntu, `stonith-enabled` será por padrão definido como false.
   
4. Por fim, será perguntado se você deseja configurar um endereço IP para a administração. Esse endereço IP é opcional, mas funciona de modo semelhante ao endereço IP de um cluster de failover do Windows Server (WSFC) no sentido de que ele cria um endereço IP do cluster a ser usado para se conectar a ele por meio de alta disponibilidade da Web Konsole (HAWK). Essa configuração, também, é opcional.
   
5. Certifique-se de que o cluster está em execução emitindo 
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
Use os seguintes comandos para instalar o pacote de HA do SQL Server e [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Agent, se eles não estão instalados. Instalando o pacote de alta disponibilidade depois de instalar [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] requer uma reinicialização da [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] para que ele seja usado. Essas instruções pressupõem que os repositórios para os pacotes da Microsoft já foram configurados, desde então [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] deve ser instalado no momento.
> [!NOTE]
> - Se você não usará [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] agente de envio de logs ou qualquer outro uso, ele não tem a ser instalado, então, empacotar *mssql-server-agent* pode ser ignorada.
> - Os pacotes opcionais para [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] no Linux, [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] pesquisa de texto completo (*mssql-server-fts*) e [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Integration Services (*mssql-server-está*), não são necessária para alta disponibilidade, para uma FCI ou um grupo de disponibilidade.

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

Neste tutorial, você aprendeu como implantar um cluster Pacemaker para o SQL Server no Linux. Você aprendeu como para:
> [!div class="checklist"]
> * Instalar o complemento de alta disponibilidade e Pacemaker.
> * Prepare os nós para Pacemaker (RHEL e somente Ubuntu).
> * Crie o cluster do Pacemaker.
> * Instale os pacotes de HA do SQL Server e SQL Server Agent.

Para criar e configurar um grupo de disponibilidade para o SQL Server no Linux, consulte:

> [!div class="nextstepaction"]
> [Criar e configurar um grupo de disponibilidade para o SQL Server no Linux](sql-server-linux-create-availability-group.md).

