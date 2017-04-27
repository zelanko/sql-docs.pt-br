---
title: "Atualizar uma instância do cluster de failover do SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 02/01/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- upgrading failover clusters
- clusters [SQL Server], upgrading
- failover clustering [SQL Server], upgrading
ms.assetid: daac41fe-7d0b-4f14-84c2-62952ad8cbfa
caps.latest.revision: 47
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 060f7bbbcd12d1b41f4c527fb1c1dff34b666134
ms.lasthandoff: 04/11/2017

---
# <a name="upgrade-a-sql-server-failover-cluster-instance"></a>Atualizar uma instância de cluster de failover do SQL Server
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] dá suporte à atualização de um cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para uma nova versão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], para um novo service pack ou atualização cumulativa do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], ou ao instalar um novo service pack ou atualização cumulativa do serviço Windows separadamente em todos os nós de cluster de failover com tempo de inatividade limitado a um único failover manual (ou dois failovers manuais em caso de failback para a primária original).  
  
 Em sistemas operacionais anteriores ao Windows Server 2012 R2, não há suporte para atualização do sistema operacional do Windows de um cluster de failover. Para atualizar um nó de cluster executado no Windows Server 2012 R2, veja [Atualização sem interrupção do sistema operacional do cluster](https://technet.microsoft.com/en-us/library/dn850430.aspx)  
  
 Os detalhes do suporte são os seguintes:  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]a atualização tem suporte pela interface do usuário e por meio do prompt de comando. Você pode executar a atualização do prompt de comando em cada nó de cluster de failover ou usando a interface do usuário de instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para atualizar cada nó de cluster.  Para obter mais informações, consulte [Atualizar uma instância de cluster de failover do SQL Server &#40;instalação&#41;](../../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance-setup.md) e [Instalar o SQL Server 2016 do prompt de comando](../../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md).  
  
-   Os cenários a seguir não têm suporte como parte de uma atualização do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] :  
  
    -   Não é possível atualizar de uma instância autônoma do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para um cluster de failover.  
  
    -   Você não pode adicionar recursos a um cluster de failover. Por exemplo, você não pode adicionar o [!INCLUDE[ssDE](../../../includes/ssde-md.md)] a um cluster de failover somente do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
    -   Você não pode fazer downgrade do nó de cluster de failover para uma instância autônoma.  
  
    -   A alteração da edição do cluster de failover é limitada a determinados cenários. Para obter mais informações, consulte [Atualizações de versão e edição com suporte](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md).  
  
-   Durante a atualização do cluster de failover, o tempo de inatividade está limitado ao tempo necessário à atualização de scripts para execução. Se você seguir o processo de atualização sem interrupção do cluster de failover abaixo e atender a todos os pré-requisitos em todos os nós antes de começar o processo de atualização, o tempo de inatividade é mínimo. Atualizar o SQL Server 2014 quando as tabelas com otimização de memória estiverem em uso levará um pouco mais de tempo. Para saber mais, confira [Plan and Test the Database Engine Upgrade Plan](../../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md).  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Antes de começar, examine as seguintes informações importantes:  
  
-   [Supported Version and Edition Upgrades](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md): verifique se você pode atualizar para o SQL Server 2016 de sua versão do sistema operacional Windows e da versão do SQL Server. Por exemplo, não é possível atualizar diretamente de um instância de clustering de failover do SQL Server 2005 para [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] ou atualizar um cluster de failover em execução no Windows Server 2003.  
  
-   [Choose a Database Engine Upgrade Method](../../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md): selecione o método e as etapas de atualização apropriados com base em sua análise de atualizações de versão e de edição com suporte e também com base em outros componentes instalados em seu ambiente a fim de atualizar os componentes na ordem correta.  
  
-   [Planejar e testar o plano de atualização do mecanismo de banco de dados](../../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md): examine as notas de versão e os problemas conhecidos da atualização, a lista de verificação pré-atualização, e desenvolva e teste o plano de atualização.  
  
-   [Requisitos de hardware e software para a instalação do SQL Server 2016](../../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md): examine os requisitos de software para a instalação do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Se for necessário um software adicional, instale-o em cada nó antes de começar o processo de atualização para minimizar qualquer tempo de inatividade.  
  
## <a name="performing-a-rolling-upgrade-or-update"></a>Realizando uma atualização ou atualização sem interrupção  
 Para atualizar um cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para o [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], use a instalação de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para atualizar cada nó de cluster de failover por vez, começando com os nós passivos. Conforme você atualiza cada nó, ele é omitido dos possíveis proprietários do cluster de failover. Se houver um failover inesperado, os nós atualizados não participarão do failover até que a propriedade do grupo de recursos de cluster seja movida para um nó atualizado pela instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 Por padrão, a instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] determina quando executar failover em um nó atualizado. Isso depende do número total de nós na instância de cluster de failover e do número de nós que já foram atualizados. Quando a metade ou mais da metade dos nós já tiver sido atualizada, a instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provocará um failover em um nó atualizado quando você executar a atualização no próximo nó. Durante o failover em um nó atualizado, o grupo de clusters é movido para um nó atualizado. Todos os nós atualizados são colocados na lista de possíveis proprietários e todos os nós que ainda não foram atualizados são removidos da lista de possíveis proprietários. À medida que você atualiza cada nó restante, ele é omitido dos possíveis proprietários do cluster de failover.  
  
 Esse processo resulta em tempo de inatividade limitado a um tempo de failover e ao tempo de execução do script de atualização do banco de dados durante toda a atualização de cluster de failover.  
  
 Para controlar o comportamento de failover de nós de cluster durante o processo de atualização, execute a operação de atualização no prompt de comando e use o parâmetro /FAILOVERCLUSTERROLLOWNERSHIP. Para obter mais informações, consulte [Instalar o SQL Server 2016 do prompt de comando](../../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md).  
  
## <a name="see-also"></a>Consulte também  
 [Atualizar para o SQL Server 2016 usando o Assistente de Instalação &#40;Instalação&#41;](../../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)   
 [Instalar o SQL Server 2016 do prompt de comando](../../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)   
 [Atualizar uma instância de cluster de failover do SQL Server &#40;instalação&#41;](../../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance-setup.md)  
  
  

