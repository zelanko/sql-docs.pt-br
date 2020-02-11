---
title: Instalação do cluster de failover do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: c0e75a7c-85c5-423c-a218-77247bf071aa
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 49fce70b4fc01f77fe7ca54e3951f0372ba18489
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63067642"
---
# <a name="sql-server-failover-cluster-installation"></a>Instalação do cluster de failover do SQL Server
  Para instalar um cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , você deve criar e configurar uma instância de cluster de failover por meio da execução da Instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="installing-a-failover-cluster"></a>Instalando um cluster de failover  
 Para instalar um cluster de failover, você deve usar uma conta de domínio com direitos de administrador local, permissão para fazer logon como um serviço e atuar como parte do sistema operacional em todos os nós do cluster de failover. Para instalar um cluster de failover por meio do programa de instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , siga estas etapas:  
  
1.  Para instalar, configurar e manter um cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , use a Instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
    -   Identifique as informações necessárias para criar sua instância de cluster de failover (por exemplo, o recurso de disco de cluster, endereços IP e nome de rede) e os nós disponíveis para failover. Para mais informações:  
  
        -   [Antes de instalar o cluster de failover](before-installing-failover-clustering.md)  
  
        -   [Considerações sobre segurança para uma instalação do SQL Server](../../install/security-considerations-for-a-sql-server-installation.md)  
  
    -   As etapas de configuração devem ocorrer antes de executar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] programa de instalação; Use o administrador de cluster do Windows para levá-los. Você deve ter um grupo WSFC para cada instância de cluster de failover que deseja configurar.  
  
    -   Você deve garantir que seu sistema atende aos requisitos mínimos. Para obter mais informações sobre requisitos específicos para um cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , veja [Antes de instalar o clustering de failover](before-installing-failover-clustering.md).  
  
2.  Adicionar ou remover nós de uma configuração de cluster de failover sem afetar os outros nós do cluster. Para obter mais informações, consulte [Adicionar ou remover nós em um cluster de Failover SQL Server &#40;instalação&#41;](add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md).  
  
    -   Todos os nós de um cluster de failover devem ser da mesma plataforma, de 32 ou de 64 bits, e devem executar a mesma edição e versão do sistema operacional. Além disso, as edições do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de 64 bits devem ser instaladas em hardware de 64 bits executando as versões de 64 bits de sistemas operacionais Windows. Não há suporte para WOW64 para clustering de failover nesta versão.  
  
3.  Especificar vários endereços IP para cada instância do cluster de failover. Você pode especificar vários endereços IP para cada sub-rede. Se os vários endereços IP estiverem na mesma sub-rede, a Instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] definirá a dependência como AND. Se você estiver clusterizando nós em várias sub-redes, a Instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] definirá a dependência como OR.  
  
## <a name="includessnoversionincludesssnoversion-mdmd-failover-cluster-installation-options"></a>
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Opções de instalações de cluster de failover  
  
##### <a name="option-1-integrated-installation-with-add-node"></a>Opção 1: Instalação integrada com Adicionar Nó  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] consiste em duas etapas:  
  
1.  Criar e configurar uma instância de cluster de failover de um único nó do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Ao concluir a configuração bem-sucedida de um nó, você tem uma instância de cluster de failover totalmente funcional. Neste momento ele não tem alta disponibilidade porque há apenas um nó no cluster de failover.  
  
2.  Em cada nó a ser adicionado ao cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , execute a Instalação com a funcionalidade Adicionar Nó para adicionar o nó.  
  
##### <a name="option-2-advancedenterprise-installation"></a>Opção 2: Instalação Avançada/Corporativa  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] A instalação Avançada/Corporativa do cluster de failover consiste em duas etapas:  
  
1.  Em cada nó que fará parte do cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , execute a Instalação com a funcionalidade de Preparação de Cluster de Failover. Essa etapa prepara os nós prontos para serem clusterizados, mas não há nenhuma instância operacional do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no final dessa etapa.  
  
2.  Depois que os nós estão preparados para clustering, execute a Instalação no nó que possui o disco compartilhado com a funcionalidade de Conclusão de Cluster de failover. Essa etapa configura e conclui a instância de cluster de failover. No final dessa etapa, você terá uma instância de cluster de failover operacional do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
    > [!NOTE]  
    >  Qualquer opção de instalação permite a instalação de cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] com vários nós. É possível usar o item Adicionar Nó para adicionar mais nós a qualquer opção após a criação de um cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
    > [!IMPORTANT]  
    >  A letra da unidade do sistema operacional para locais de instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] deve ser igual em todos os nós adicionados ao cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
#### <a name="ip-address-configuration-during-setup"></a>Configuração de endereço IP durante a instalação  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] permite definir ou alterar as configurações de dependência de recursos IP durante as ações a seguir:  
  
-   Instalação integrada – [Criar um novo cluster de failover do SQL Server &#40;Instalação&#41;](create-a-new-sql-server-failover-cluster-setup.md)  
  
-   CompleteFailoverCluster (Instalação avançada) – [Criar um novo cluster de failover do SQL Server &#40;Instalação&#41;](create-a-new-sql-server-failover-cluster-setup.md)  
  
-   Adicionar Nó – [Adicionar ou remover nós em um cluster de failover do SQL Server &#40;Instalação&#41;](add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)  
  
-   Remover nó – [Adicionar ou remover nós em um cluster de failover do SQL Server &#40;Instalação&#41;](add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)  
  
 **Observação** Há suporte para endereços IP IPV6.  Se você configurar IPV4 e IPV6, ambos serão tratados como sub-redes diferentes, e espera-se que o IPV6 entre online primeiro.  
  
##### <a name="includessnoversionincludesssnoversion-mdmd-multi-subnet-failover-cluster"></a>
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Cluster de failover de várias sub-redes  
 Você pode definir dependências OR quando os nós no cluster estiverem em sub-redes diferentes. No entanto, cada nó no cluster de failover de várias sub-redes do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] deve ser um possível proprietário de pelo menos um dos endereços IP especificados.  
  
## <a name="see-also"></a>Consulte Também  
 [Antes de instalar o cluster de failover](before-installing-failover-clustering.md)   
 [Crie um novo cluster de failover SQL Server &#40;a instalação&#41;](create-a-new-sql-server-failover-cluster-setup.md)   
 [Instalar o SQL Server 2014 no prompt de comando](../../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)   
 [Atualizar um cluster de failover SQL Server](../windows/upgrade-a-sql-server-failover-cluster-instance.md)  
  
  
