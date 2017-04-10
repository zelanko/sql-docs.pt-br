---
title: "Escolher um M&#233;todo de Atualiza&#231;&#227;o do Mecanismo de Banco de Dados | Microsoft Docs"
ms.custom: ""
ms.date: "06/02/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "server-general"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5e57a427-2e88-4ef6-b142-4ccad97bcecc
caps.latest.revision: 23
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 23
---
# Escolher um M&#233;todo de Atualiza&#231;&#227;o do Mecanismo de Banco de Dados
  Há várias abordagens a serem consideradas quando você está planejando atualizar o [!INCLUDE[ssDE](../../includes/ssde-md.md)] de uma versão anterior do SQL Server para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para minimizar o tempo de inatividade e o risco. Você pode executar uma atualização in-loco, migrar para uma nova instalação ou executar uma atualização sem interrupção. O diagrama a seguir ajudará você a escolher entre essas abordagens. Cada uma das abordagens no diagrama também são discutidas abaixo. Para ajudá-lo com os pontos de decisão no diagrama, veja também [Plan and Test the Database Engine Upgrade Plan](../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md).  
  
 ![Database Engine Upgrade Method Decision Tree](../../database-engine/install-windows/media/database-engine-upgrade-method-decision-tree.png "Database Engine Upgrade Method Decision Tree")  
  
 **Download**  
  
-   Para baixar o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], acesse o  **[Centro de Avaliação](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)**.  
  
-   Tem uma conta do Azure?  Então, acesse **[aqui](https://azure.microsoft.com/en-us/marketplace/partners/microsoft/sqlserver2016ctp2evaluationwindowsserver2012r2/?wt.mc_id=sqL16_vm)** para executar uma máquina virtual com o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] já instalado.  
  
> [!NOTE]  
>  Você também pode atualizar o banco de dados do SQL Azure ou virtualizar seu ambiente SQL Server como parte de seu plano de atualização. Esses assuntos estão fora do escopo deste tópico, mas você pode consultar estes links: [Introdução à nuvem híbrida do SQL Server 2016](../Topic/Introduction%20to%20SQL%20Server%202016%20Hybrid%20Cloud.md), [Visão geral do SQL Server em Máquinas Virtuais do Azure](https://azure.microsoft.com/documentation/articles/virtual-machines-sql-server-infrastructure-services/), [Banco de Dados SQL](https://azure.microsoft.com/en-us/services/sql-database/) e [Selecionando uma opção do SQL Server no Azure](https://azure.microsoft.com/documentation/articles/data-management-azure-sql-database-and-sql-server-iaas/).  
  
##  <a name="UpgradeInPlace"></a> Atualização in-loco  
 Com essa abordagem, o programa de instalação do SQL Server atualiza a instalação existente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , substituindo os bits do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] existentes por bits do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e atualiza cada um dos bancos de dados do sistema e do usuário.  O método de atualização in-loco é o mais fácil, requer algum tempo de inatividade, leva mais tempo para executar um fallback se um fallback for necessário e não é permitido em todos os cenários. Para obter mais informações sobre os cenários de atualização in-loco com e sem suporte, veja [Atualizações de versão e edição com suporte](../../database-engine/install-windows/supported-version-and-edition-upgrades.md).  
  
 Essa abordagem é frequentemente usada nos seguintes cenários:  
  
-   Um ambiente de desenvolvimento sem uma configuração de alta disponibilidade (HA).  
  
-   Um ambiente de produção de missão não crítica que pode tolerar tempo de inatividade e que é executado em hardware e software recentes. O tempo de inatividade depende do tamanho do banco de dados e da velocidade de seu subsistema de E/S. Atualizar o SQL Server 2014 quando as tabelas com otimização de memória estiverem em uso levará um pouco mais de tempo. Para saber mais, confira [Plan and Test the Database Engine Upgrade Plan](../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md).  
  
> [!WARNING]  
>  Ao executar o programa de instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é interrompida e reiniciada como parte da execução das verificações pré-atualização.  
  
> [!CAUTION]  
>  Quando você atualizar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a instância anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será substituída e não mais existirá no computador. Antes de atualizar, faça backup dos bancos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e de outros objetos associados à instância anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 O diagrama a seguir fornece uma visão geral de alto nível das etapas necessárias para uma atualização in-loco do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 ![Database Engine Upgrade Non-HA In-Place Upgrade](../../database-engine/install-windows/media/database-engine-upgrade-non-ha-in-place-upgrade.png "Database Engine Upgrade Non-HA In-Place Upgrade")  
  
 Para obter etapas detalhadas, veja [Atualizar para o SQL Server 2016 usando o Assistente de Instalação &#40;Instalação&#41;](../../database-engine/install-windows/upgrade-to-sql-server-2016-using-the-installation-wizard-setup.md).  
  
##  <a name="NewInstallationUpgrade"></a> Migrar para uma nova instalação  
 Com essa abordagem, você mantém o ambiente atual enquanto cria um novo ambiente do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , frequentemente em um novo hardware e com uma nova versão do sistema operacional. Depois de instalar o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] no novo ambiente, você deve realizar algumas etapas para preparar o novo ambiente para migrar os bancos de dados do usuário do ambiente existente para o novo ambiente e minimizar o tempo de inatividade. Essas etapas incluem a migração dos seguintes itens:  
  
-   **Objetos do sistema: **alguns aplicativos dependem de informações, entidades e/ou objetos que estão fora do escopo de um único banco de dados de usuário. Normalmente, um aplicativo tem dependências no banco de dados mestre e msdb e também no banco de dados do usuário. Qualquer coisa armazenada fora de um banco de dados de usuário que seja necessária para o funcionamento correto daquele banco de dados deve estar disponível na instância do servidor de destino. Por exemplo, os logons de um aplicativo são armazenados como metadados no banco de dados mestre e devem ser recriados no servidor de destino. Se um plano de manutenção de um banco de dados ou aplicativo depender de trabalhos do SQL Server Agent, cujos metadados estão armazenados no banco de dados msdb, é necessário recriar esses trabalhos na instância do servidor de destino. De maneira semelhante, os metadados para um gatilho em nível de servidor são armazenados no mestre.  
    Ao mover o banco de dados de um aplicativo para outra instância de servidor, é necessário recriar todos os metadados dos objetos e entidades dependentes do mestre e do msdb na instância do servidor de destino. Por exemplo, se um aplicativo de banco de dados usar gatilhos em nível de servidor, apenas a anexação ou a restauração do banco de dados no novo sistema não será suficiente. O banco de dados não funcionará conforme esperado a não ser que os metadados desses gatilhos sejam recriados manualmente no banco de dados mestre. Para obter informações detalhadas, veja [Gerenciar metadados ao disponibilizar um banco de dados em outra instância do servidor &#40;SQL Server&#41;](../../relational-databases/databases/manage metadata when making a database available on another server.md).  
  
-   **Pacotes do Integration Services armazenados no MSDB:** se você estiver armazenando pacotes no MSDB, precisará escrever script para esses pacotes usando o [dtutil Utility](../../integration-services/dtutil-utility.md) ou reimplantá-los no novo servidor. Antes de usar os pacotes no novo servidor, você precisará atualizar os pacotes para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para saber mais, confira [Upgrade Integration Services Packages](../../integration-services/install-windows/upgrade-integration-services-packages.md).  
  
-   **Chaves de criptografia do Reporting Services:** uma parte importante da configuração do servidor de relatório é a criação de uma cópia de backup da chave simétrica usada para criptografar informações confidenciais. Uma cópia de backup da chave é necessária para várias operações rotineiras, possibilitando que você reutilize um banco de dados de servidor de relatório existente em uma nova instalação. Para obter mais informações, veja [Fazer backup e restaurar as chaves de criptografia do Reporting Services](../../reporting-services/install-windows/back-up-and-restore-reporting-services-encryption-keys.md) e [Atualizar e migrar o Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)  
  
 Quando o novo ambiente do   [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tiver os mesmos objetos de sistema do ambiente existente, migre os bancos de dados do usuário do sistema existente para a instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] de maneira que minimize o tempo de inatividade do sistema existente. Realize a migração do banco de dados usando backup e restauração ou redirecionando LUNs se você estiver em um ambiente de SAN. As etapas para ambos os métodos são delineadas nos diagramas a seguir.  
  
> [!CAUTION]  
>  O tempo de inatividade depende do tamanho do banco de dados e da velocidade de seu subsistema de E/S. Atualizar o SQL Server 2014 quando as tabelas com otimização de memória estiverem em uso levará um pouco mais de tempo. Para saber mais, confira [Plan and Test the Database Engine Upgrade Plan](../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md).  
  
 Depois de migrar os bancos de dados do usuário, direcione novos usuários para a nova instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando um entre vários métodos possíveis (por exemplo, renomear o servidor, usar uma entrada de DNS, modificar cadeias de conexão).  A nova abordagem de instalação reduz o risco e o tempo de inatividade em comparação com uma atualização in-loco e facilita as atualizações de hardware e sistema operacional em conjunto com a atualização para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
> [!NOTE]  
>  Se você já tiver uma solução de HA (alta disponibilidade) em vigor ou outro ambiente com várias instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vá para [Atualização sem interrupção](#RollingUpgrade). Se você não tiver uma solução de alta disponibilidade, considere configurar o [Espelhamento de Banco de Dados](http://msdn.microsoft.com/library/ms190941.aspx) temporariamente para minimizar o tempo de inatividade e facilitar a atualização ou aproveitar essa oportunidade para configurar um [Grupo de Disponibilidade AlwaysOn](http://msdn.microsoft.com/library/hh510260.aspx) como uma solução de HA permanente.  
  
 Por exemplo, você pode usar essa abordagem para atualizar:  
  
-   Uma instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um sistema operacional sem suporte.  
  
-   Um instalação x86 do SQL Server, já que o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] não oferece suporte a instalações x86.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o novo hardware e/ou uma nova versão do sistema operacional.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em conjunto com a consolidação de servidores.  
  
-   O SQL Server 2005, já que o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] não dá suporte à atualização in-loco do SQL Server 2005 para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para saber mais, confira [Are you upgrading from SQL Server 2005?](../../database-engine/install-windows/are-you-upgrading-from-sql-server-2005.md).  
  
 As etapas necessárias para a atualização de uma nova instalação variam um pouco, dependendo se você estiver usando armazenamento NAS ou SAN.  
  
-   **Ambiente NAS:** se você tiver um ambiente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que use NAS, o diagrama a seguir e os links do diagrama orientam você pelas etapas necessárias para a atualização de uma nova instalação do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
     ![New installation upgrade method using backup and restore for attached storage](../../database-engine/install-windows/media/new-installation-upgrade-method-using-backup-and-restore-for-attached-storage.png "New installation upgrade method using backup and restore for attached storage")  
  
-   **Ambiente SAN:**  se você tiver um ambiente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que use SAN, o diagrama a seguir e os links do diagrama orientam você pelas etapas necessárias para a atualização de uma nova instalação do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
     ![New installation upgrade method using detach and attach for SAN storage](../../database-engine/install-windows/media/new-installation-upgrade-method-using-detach-and-attach-for-san-storage.png "New installation upgrade method using detach and attach for SAN storage")  
  
##  <a name="RollingUpgrade"></a> Atualização sem interrupção  
 É necessária uma atualização sem interrupção em ambientes de solução do SQL Server que envolvem várias instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que devam ser atualizadas em uma determinada ordem para maximizar o tempo de atividade, minimizar os riscos e preservar a funcionalidade. Uma atualização sem interrupção é, em essência, a atualização de várias instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em uma ordem específica, com a atualização in-loco de cada instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou com a atualização de uma nova instalação para facilitar a atualização de hardware e/ou do sistema operacional como parte do projeto de atualização. Há várias situações em que a abordagem de atualização sem interrupção é necessária. Essas situações são documentadas nos seguintes tópicos:  
  
-   Grupos de Disponibilidade AlwaysOn: para obter etapas detalhadas para executar uma atualização sem interrupção nesse ambiente, veja [Atualizar instâncias de réplica do Grupo de Disponibilidade AlwaysOn](../../database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances.md).  
  
-   Instâncias de clustering de failover: para obter etapas detalhadas para executar uma atualização sem interrupção nesse ambiente, veja [Atualizar uma instância de cluster de failover do SQL Server](../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance.md)  
  
-   Instâncias espelhadas: para obter etapas detalhadas para executar uma atualização sem interrupção nesse ambiente, veja [Atualizando instâncias espelhadas](../../database-engine/database-mirroring/upgrading-mirrored-instances.md).  
  
-   Instâncias de envio de log: para obter etapas detalhadas para executar uma atualização sem interrupção nesse ambiente, veja [Atualizando o envio de log para o SQL Server 2016 &#40;Transact-SQL&#41;](../../database-engine/log-shipping/upgrading-log-shipping-to-sql-server-2016-transact-sql.md)  
  
-   Um ambiente de replicação: para obter etapas detalhadas para executar uma atualização sem interrupção nesse ambiente, veja [Upgrade Replicated Databases](../../database-engine/install-windows/upgrade-replicated-databases.md)  
  
-   Um ambiente expandido do SQL Server Reporting Services: para obter etapas detalhadas para executar uma atualização sem interrupção nesse ambiente, veja [Atualizar e migrar o Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md).  
  
## Este artigo foi útil para você? Estamos atentos  
 Quais são as informações que você está procurando? Você as localizou? Estamos atentos aos seus comentários para aprimorar o conteúdo. Envie seus comentários para [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Choose%20a%20Database%20Engine%20Upgrade%20Method%20page)  
  
## Consulte também  
 [Planejar e testar o plano de atualização do mecanismo de banco de dados](../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md)   
 [Concluir a atualização do mecanismo de banco de dados](../../database-engine/install-windows/complete-the-database-engine-upgrade.md)  
  
  