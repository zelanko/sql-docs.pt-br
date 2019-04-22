---
title: Escolher um método de upgrade do mecanismo de banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 07/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 5e57a427-2e88-4ef6-b142-4ccad97bcecc
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
manager: craigg
ms.openlocfilehash: f8a71f5e91fec924a73186211f3296bfc52add8a
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2019
ms.locfileid: "58872256"
---
# <a name="choose-a-database-engine-upgrade-method"></a>Escolher um método de upgrade do mecanismo de banco de dados
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Há várias abordagens a serem consideradas quando você está planejando fazer upgrade do [!INCLUDE[ssDE](../../includes/ssde-md.md)] de uma versão anterior do SQL Server, a fim de minimizar o tempo de inatividade e o risco. Você pode executar uma atualização in-loco, migrar para uma nova instalação ou executar uma atualização sem interrupção. O diagrama a seguir ajudará você a escolher entre essas abordagens. Cada uma das abordagens no diagrama também são discutidas abaixo. Para ajudá-lo com os pontos de decisão no diagrama, veja também [planejar e testar o Database Engine Upgrade Plan](../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md).  
  
 ![Árvore de decisão do método de upgrade do Mecanismo de Banco de Dados](../../database-engine/install-windows/media/database-engine-upgrade-method-decision-tree.png "Árvore de decisão do método de upgrade do Mecanismo de Banco de Dados")  
  
 **Download**  
  
-   Para baixar o [!INCLUDE[SSnoversion](../../includes/ssnoversion-md.md)], acesse o  **[Centro de Avaliação](https://www.microsoft.com/evalcenter/evaluate-sql-server)**.  
  
-   Tem uma conta do Azure?  Em seguida, acesse **[aqui](https://azuremarketplace.microsoft.com/marketplace/apps/microsoftsqlserver.sql2019-ws2016?tab=Overview)** para criar uma Máquina Virtual com o [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] Developer Edition já instalado.  
  
> [!NOTE]  
>  Você também pode atualizar o banco de dados do SQL Azure ou virtualizar seu ambiente SQL Server como parte de seu plano de atualização. Estes artigos estão fora do escopo deste artigo, mas veja abaixo alguns links:
>   - [Visão geral do SQL Server nas Máquinas Virtuais do Azure](https://azure.microsoft.com/documentation/articles/virtual-machines-sql-server-infrastructure-services/)
>   - [Banco de Dados SQL do Azure](https://azure.microsoft.com/services/sql-database/) 
>   - [Selecionando uma opção do SQL Server no Azure](https://azure.microsoft.com/documentation/articles/data-management-azure-sql-database-and-sql-server-iaas/).  
  
## <a name="upgrade-in-place"></a>Atualização in-loco  
 Com essa abordagem, o programa de instalação do SQL Server faz upgrade da instalação existente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], substituindo os bits do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] existentes pelos novos bits do [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] e, depois, faz upgrade de cada um dos bancos de dados do sistema e do usuário.  O método de atualização in-loco é o mais fácil, requer algum tempo de inatividade, leva mais tempo para executar um fallback se um fallback for necessário e não é permitido em todos os cenários. Para obter mais informações sobre os cenários de atualização in-loco com e sem suporte, veja [Atualizações de versão e edição com suporte](../../database-engine/install-windows/supported-version-and-edition-upgrades-2017.md).  
  
 Essa abordagem é frequentemente usada nos seguintes cenários:  
  
-   Um ambiente de desenvolvimento sem uma configuração de alta disponibilidade (HA).  
  
-   Um ambiente de produção de missão não crítica que pode tolerar tempo de inatividade e que é executado em hardware e software recentes. O tempo de inatividade depende do tamanho do banco de dados e da velocidade de seu subsistema de E/S. Atualizar o SQL Server 2014 quando as tabelas com otimização de memória estiverem em uso levará um pouco mais de tempo. Para saber mais, confira [Planejar e testar o plano de atualização do mecanismo de banco de dados](../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md).  
  
> [!WARNING]  
>  Ao executar o programa de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é interrompida e reiniciada como parte da execução das verificações pré-atualização.  
  
> [!CAUTION]  
>  Quando você atualizar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a instância anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será substituída e não mais existirá no computador. Antes de atualizar, faça backup dos bancos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e de outros objetos associados à instância anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 O diagrama a seguir fornece uma visão geral de alto nível das etapas necessárias para uma atualização in-loco do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 ![Upgrade do Mecanismo de Banco de Dados Atualização in-loco não HA](../../database-engine/install-windows/media/database-engine-upgrade-non-ha-in-place-upgrade.png "Upgrade do Mecanismo de Banco de Dados Atualização in-loco não HA")  
  
 Para obter etapas detalhadas, consulte [Fazer upgrade do SQL Server usando o Assistente de Instalação &#40;Instalação&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md).  
  
## <a name="migrate-to-a-new-installation"></a>Migrar para uma nova instalação  
 Com essa abordagem, você mantém o ambiente atual enquanto cria um novo ambiente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , frequentemente em um novo hardware e com uma nova versão do sistema operacional. Depois de instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no novo ambiente, você deve realizar algumas etapas para preparar o novo ambiente para migrar os bancos de dados do usuário do ambiente existente para o novo ambiente e minimizar o tempo de inatividade. Essas etapas incluem a migração dos seguintes itens:  
  
-   **Objetos do sistema:** Alguns aplicativos dependem de informações, entidades e/ou objetos que estão fora do escopo de um único banco de dados de usuário. Normalmente, um aplicativo tem dependências no banco de dados mestre e msdb e também no banco de dados do usuário. Qualquer coisa armazenada fora de um banco de dados de usuário que seja necessária para o funcionamento correto daquele banco de dados deve estar disponível na instância do servidor de destino. Por exemplo, os logons de um aplicativo são armazenados como metadados no banco de dados mestre e devem ser recriados no servidor de destino. Se um plano de manutenção de um banco de dados ou aplicativo depender de trabalhos do SQL Server Agent, cujos metadados estão armazenados no banco de dados msdb, é necessário recriar esses trabalhos na instância do servidor de destino. De maneira semelhante, os metadados para um gatilho em nível de servidor são armazenados no mestre.  
 
   Ao mover o banco de dados de um aplicativo para outra instância de servidor, é necessário recriar todos os metadados dos objetos e entidades dependentes do mestre e do msdb na instância do servidor de destino. Por exemplo, se um aplicativo de banco de dados usar gatilhos em nível de servidor, apenas a anexação ou a restauração do banco de dados no novo sistema não será suficiente. O banco de dados não funcionará conforme esperado a não ser que os metadados desses gatilhos sejam recriados manualmente no banco de dados mestre. Para obter informações detalhadas, veja [Gerenciar metadados ao disponibilizar um banco de dados em outra instância do servidor &#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md).  
  
-   **Pacotes do Integration Services armazenados no MSDB:** se você estiver armazenando pacotes no MSDB, precisará escrever script para esses pacotes usando o [dtutil Utility](../../integration-services/dtutil-utility.md) ou reimplantá-los no novo servidor. Antes de usar os pacotes no novo servidor, você precisará atualizar os pacotes para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para saber mais, confira [Upgrade Integration Services Packages](../../integration-services/install-windows/upgrade-integration-services-packages.md).  
  
-   **Chaves de criptografia do Reporting Services:** Um parte importante da configuração do servidor de relatório é a criação de uma cópia de backup da chave simétrica usada para criptografar informações confidenciais. Uma cópia de backup da chave é necessária para várias operações rotineiras, possibilitando que você reutilize um banco de dados de servidor de relatório existente em uma nova instalação. Para obter mais informações, veja [Fazer backup e restaurar as chaves de criptografia do Reporting Services](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md) e [Atualizar e migrar o Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)  
  
 Quando o novo ambiente do   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tiver os mesmos objetos de sistema do ambiente existente, migre os bancos de dados do usuário do sistema existente para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de maneira que minimize o tempo de inatividade do sistema existente. Realize a migração do banco de dados usando backup e restauração ou redirecionando LUNs se você estiver em um ambiente de SAN. As etapas para ambos os métodos são delineadas nos diagramas a seguir.  
  
> [!CAUTION]  
>  O tempo de inatividade depende do tamanho do banco de dados e da velocidade de seu subsistema de E/S. Atualizar o SQL Server 2014 quando as tabelas com otimização de memória estiverem em uso levará um pouco mais de tempo. Para saber mais, confira [Planejar e testar o plano de atualização do mecanismo de banco de dados](../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md).  
  
 Depois de migrar os bancos de dados do usuário, direcione novos usuários para a nova instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando um entre vários métodos possíveis (por exemplo, renomear o servidor, usar uma entrada de DNS, modificar cadeias de conexão).  A nova abordagem de instalação reduz o risco e o tempo de inatividade em comparação com uma atualização in-loco e facilita as atualizações de hardware e sistema operacional em conjunto com a atualização para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Se você já tiver uma solução de HA (alta disponibilidade) em vigor ou outro ambiente com várias instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vá para [Atualização sem interrupção](#rolling-upgrade). Se você não tiver uma solução de alta disponibilidade, considere configurar o [Espelhamento de Banco de Dados](../database-mirroring/setting-up-database-mirroring-sql-server.md) temporariamente para minimizar o tempo de inatividade e facilitar a atualização ou aproveitar essa oportunidade para configurar um [Grupo de Disponibilidade AlwaysOn](https://msdn.microsoft.com/library/hh510260.aspx) como uma solução de HA permanente.  
  
 Por exemplo, você pode usar essa abordagem para atualizar:  
  
-   Uma instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um sistema operacional sem suporte.    
-   Uma instalação x86 do SQL Server, pois o [!INCLUDE[ss2016](../../includes/sssql15-md.md)] e posterior não dá suporte a instalações x86.   
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o novo hardware e/ou uma nova versão do sistema operacional.    
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em conjunto com a consolidação de servidores.   
-   O SQL Server 2005, pois o [!INCLUDE[ss2016](../../includes/sssql15-md.md)] e posterior não dá suporte à atualização in-loco do SQL Server 2005. Para obter mais informações, consulte [Você está fazendo upgrade do SQL Server 2005?](../../database-engine/install-windows/are-you-upgrading-from-sql-server-2005.md).

  
As etapas necessárias para a atualização de uma nova instalação variam um pouco, dependendo se você estiver usando armazenamento NAS ou SAN.  
  
-   **Ambiente de armazenamento anexado:** se você tiver um ambiente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que usa o armazenamento anexado, o diagrama a seguir e os links do diagrama orientarão você pelas etapas necessárias para a atualização de uma nova instalação do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
     ![Método de upgrade de nova instalação usando backup e restauração para o armazenamento anexado](../../database-engine/install-windows/media/new-installation-upgrade-method-using-backup-and-restore-for-attached-storage.png "Método de upgrade de nova instalação usando backup e restauração para o armazenamento anexado")  
  
-   **Ambiente de armazenamento SAN:**  se você tiver um ambiente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que usa o armazenamento SAN, o diagrama a seguir e os links do diagrama orientarão você pelas etapas necessárias para a atualização de uma nova instalação do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
     ![Método de upgrade de nova instalação usando desanexar e anexar para o armazenamento da rede SAN](../../database-engine/install-windows/media/new-installation-upgrade-method-using-detach-and-attach-for-san-storage.png "Método de upgrade de nova instalação usando desanexar e anexar para o armazenamento da rede SAN")  
  
## <a name="rolling-upgrade"></a>Atualização sem interrupção  
 É necessária uma atualização sem interrupção em ambientes de solução do SQL Server que envolvem várias instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que devam ser atualizadas em uma determinada ordem para maximizar o tempo de atividade, minimizar os riscos e preservar a funcionalidade. Uma atualização sem interrupção é, em essência, a atualização de várias instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em uma ordem específica, com a atualização in-loco de cada instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ou com a atualização de uma nova instalação para facilitar a atualização de hardware e/ou do sistema operacional como parte do projeto de atualização. Há várias situações em que a abordagem de atualização sem interrupção é necessária. Essas situações são documentadas nos seguintes artigos:  
  
-   Grupos de Disponibilidade Always On: para obter etapas detalhadas para executar uma atualização sem interrupção nesse ambiente, confira [Atualizar instâncias de réplica do Grupo de Disponibilidade Always On](../../database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances.md).    
-   Instâncias de cluster de failover: para obter etapas detalhadas para executar uma atualização sem interrupção nesse ambiente, confira [Atualizar uma instância de cluster de failover do SQL Server](../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance.md)    
-   Instâncias espelhadas: para obter etapas detalhadas para executar uma atualização sem interrupção nesse ambiente, confira [Atualizando instâncias espelhadas](../../database-engine/database-mirroring/upgrading-mirrored-instances.md).    
-   Instâncias de envio de logs: para obter etapas detalhadas para executar uma atualização sem interrupção nesse ambiente, confira [Fazendo upgrade do envio de logs para o SQL Server &#40;Transact-SQL&#41;](../../database-engine/log-shipping/upgrading-log-shipping-to-sql-server-2016-transact-sql.md).    
-   Um ambiente de replicação: para obter etapas detalhadas para executar uma atualização sem interrupção nesse ambiente, confira [Atualizar bancos de dados replicados](../../database-engine/install-windows/upgrade-replicated-databases.md).  
-   Um ambiente de expansão do SQL Server Reporting Services: Para obter etapas detalhadas para executar uma atualização sem interrupção nesse ambiente, confira [Atualizar e migrar o Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md).  
  
## <a name="next-steps"></a>Próximas etapas
 [Planejar e testar o plano de atualização do mecanismo de banco de dados](../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md)   
 [Concluir a atualização do mecanismo de banco de dados](../../database-engine/install-windows/complete-the-database-engine-upgrade.md)  
