---
title: Atualizar uma instância do cluster de failover do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 10/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- upgrading failover clusters
- clusters [SQL Server], upgrading
- failover clustering [SQL Server], upgrading
ms.assetid: daac41fe-7d0b-4f14-84c2-62952ad8cbfa
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 54863db300d7a63404161e438bede2ecc2ec8928
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47783724"
---
# <a name="upgrade-a-sql-server-failover-cluster-instance"></a>Atualizar uma instância de cluster de failover do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] dá suporte ao upgrade de um cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para uma nova versão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], para um novo service pack ou atualização cumulativa do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ou ao instalar um novo service pack ou atualização cumulativa do serviço Windows separadamente em todos os nós de cluster de failover, com tempo de inatividade limitado a um único failover manual (ou dois failovers manuais, em caso de failback para a primária original).  
  
 Não há suporte para upgrade do sistema operacional Windows de um cluster de failover em sistemas operacionais anteriores ao [!INCLUDE[winblue-server-2-md](../../../includes/winblue-server-2-md.md)]. Para fazer upgrade de um nó de cluster em execução no [!INCLUDE[winblue-server-2-md](../../../includes/winblue-server-2-md.md)] ou posterior, consulte [Executar uma atualização ou atualização sem interrupção](#perform-a-rolling-upgrade-or-update).  
  
 Os detalhes do suporte são os seguintes:  
  
-   Há suporte para a atualização do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] por meio da interface do usuário e do prompt de comando. Você pode executar a atualização do prompt de comando em cada nó de cluster de failover ou usando a interface do usuário de instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para atualizar cada nó de cluster.  Para obter mais informações, consulte [Atualizar uma instância do cluster de failover do SQL Server &#40;instalação&#41;](../../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance-setup.md) e [Instalar o SQL Server por meio do prompt de comando](../../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md).  
  
-   Os cenários a seguir não têm suporte como parte de uma atualização do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] :  
  
    -   Não é possível atualizar de uma instância autônoma do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para um cluster de failover.  
  
    -   Você não pode adicionar recursos a um cluster de failover. Por exemplo, você não pode adicionar o [!INCLUDE[ssDE](../../../includes/ssde-md.md)] a um cluster de failover somente do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
    -   Você não pode fazer downgrade do nó de cluster de failover para uma instância autônoma.  
  
    -   A alteração da edição do cluster de failover é limitada a determinados cenários. Para obter mais informações, consulte [Atualizações de versão e edição com suporte](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md).  
  
-   Durante a atualização do cluster de failover, o tempo de inatividade está limitado ao tempo necessário à atualização de scripts para execução. Se você seguir o processo de atualização sem interrupção do cluster de failover abaixo e atender a todos os pré-requisitos em todos os nós antes de começar o processo de atualização, o tempo de inatividade é mínimo. O upgrade do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] quando as tabelas com otimização de memória estiverem em uso levará um pouco mais de tempo. Para saber mais, confira [Planejar e testar o plano de atualização do mecanismo de banco de dados](../../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md).  
  
## <a name="prerequisites"></a>Prerequisites  
 Antes de começar, examine as seguintes informações importantes:  
  
-   [Upgrades de versão e edição com suporte](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md): verifique se você pode atualizar para o [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] de sua versão do sistema operacional Windows e da versão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Por exemplo, não é possível atualizar diretamente de um instância de clustering de failover do SQL Server 2005 para o [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] atualizar um cluster de failover em execução no [!INCLUDE[winxpsvr-md](../../../includes/winxpsvr-md.md)].  
  
-   [Escolha um método de atualização do mecanismo de banco de dados](../../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md): selecione o método de atualização apropriado e as etapas com base em sua análise de atualizações de versão e edição com suporte e também com base em outros componentes instalados em seu ambiente para atualizar os componentes no ordem correta.  
  
-   [Planejar e testar o plano de atualização do mecanismo de banco de dados](../../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md): examine as notas de versão e os problemas conhecidos da atualização, a lista de verificação pré-atualização, e desenvolva e teste o plano de atualização.  
  
-   [Requisitos de hardware e software para a instalação do SQL Server](../../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md): examine os requisitos de software para a instalação do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Se for necessário um software adicional, instale-o em cada nó antes de começar o processo de atualização para minimizar qualquer tempo de inatividade.  
  
## <a name="perform-a-rolling-upgrade-or-update"></a>Realizar uma atualização ou atualização sem interrupção  
 Para atualizar um cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para o [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], use a instalação de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para atualizar cada nó de cluster de failover por vez, começando com os nós passivos. Conforme você atualiza cada nó, ele é omitido dos possíveis proprietários do cluster de failover. Se houver um failover inesperado, os nós atualizados não participarão do failover até que a propriedade do grupo de recursos de cluster seja movida para um nó atualizado pela instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 Por padrão, a instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] determina quando executar failover em um nó atualizado. Isso depende do número total de nós na instância de cluster de failover e do número de nós que já foram atualizados. Quando a metade ou mais da metade dos nós já tiver sido atualizada, a instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provocará um failover em um nó atualizado quando você executar a atualização no próximo nó. Durante o failover em um nó atualizado, o grupo de clusters é movido para um nó atualizado. Todos os nós atualizados são colocados na lista de possíveis proprietários e todos os nós que ainda não foram atualizados são removidos da lista de possíveis proprietários. À medida que você atualiza cada nó restante, ele é omitido dos possíveis proprietários do cluster de failover.  
  
 Esse processo resulta em tempo de inatividade limitado a um tempo de failover e ao tempo de execução do script de atualização do banco de dados durante toda a atualização de cluster de failover.  
  
 Para controlar o comportamento de failover de nós de cluster durante o processo de atualização, execute a operação de atualização no prompt de comando e use o parâmetro /FAILOVERCLUSTERROLLOWNERSHIP. Para obter mais informações, consulte [Instalar o SQL Server por meio do prompt de comando](../../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md).  
  
## <a name="next-steps"></a>Próximas etapas  
 [Fazer upgrade do SQL Server usando o Assistente de Instalação &#40;Instalação&#41;](../../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)   
 [Instalar o SQL Server do prompt de comando](../../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)   
 [Atualizar uma instância de cluster de failover do SQL Server &#40;instalação&#41;](../../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance-setup.md)  
  
  
