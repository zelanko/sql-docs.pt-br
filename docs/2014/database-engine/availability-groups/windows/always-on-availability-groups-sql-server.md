---
title: Grupos de Disponibilidade AlwaysOn (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], about
- secondary replicas, see Availability Groups [SQL Server]
- availability [SQL Server]
- AlwaysOn [SQL Server], see Availability Groups [SQL Server]
- Availability Groups [SQL Server]
ms.assetid: aa427606-8422-4656-b205-c9e665ddc8c1
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 2c05dc72e99d5b897412bdcf8afdd85370dd06b7
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84937213"
---
# <a name="always-on-availability-groups-sql-server"></a>Grupos de Disponibilidade AlwaysOn (SQL Server)
  O recurso [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] é uma solução de alta disponibilidade e de recuperação de desastres que fornece uma alternativa em nível corporativo para espelhamento de banco de dados. Apresentados no [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], os [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] maximizam a disponibilidade de um conjunto de bancos de dados de usuário para uma empresa. Um *grupo de disponibilidade* dá suporte a um ambiente de failover para um conjunto discreto de bancos de dados de usuário, conhecidos como *bancos de dados de disponibilidade*, que fazem failover juntos. Um grupo de disponibilidade dá suporte a um conjunto de bancos de dados primários de leitura/gravação e a um dos oito conjuntos de bancos de dados secundários correspondentes. Opcionalmente, é possível tornar disponíveis os bancos de dados secundários para acesso somente leitura e/ou algumas operações de backup.  
  
 Um grupo de disponibilidade faz failover no nível de uma réplica de disponibilidade. Os failovers não são provocados por problemas de banco de dados, como um banco de dados que se torna suspeito devido à perda de um arquivo de dados, à exclusão de um banco de dados ou à corrupção de um log de transações.  
  
  
##  <a name="benefits"></a><a name="Benefits"></a> Benefícios  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] fornecem um conjunto diversificado de opções que melhoram a disponibilidade do banco de dados e habilitam o uso aprimorado de recursos. Os principais componentes são os seguintes:  
  
-   Permite até nove réplicas de disponibilidade. Uma *réplica de disponibilidade* é uma instanciação de um grupo de disponibilidade que é hospedado por uma instância específica do SQL Server e que mantém uma cópia local de cada banco de dados de disponibilidade pertencente ao grupo de disponibilidade. Cada grupo de disponibilidade suporta uma réplica primária e até oito réplicas secundárias. Para obter mais informações, consulte [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md).  
  
    > [!IMPORTANT]  
    >  Cada réplica de disponibilidade deve residir em um nó diferente de um único cluster do WSFC (Windows Server Failover Clustering). Para obter mais informações sobre pré-requisitos, restrições e recomendações para grupos de disponibilidade, consulte [pré-requisitos, restrições e recomendações para grupos de disponibilidade de Always on; SQL Server;](prereqs-restrictions-recommendations-always-on-availability.md).  
  
-   Dá suporte para modos de disponibilidade alternativos, como:  
  
    -   *Modo de confirmação assíncrona*. Este modo de disponibilidade é uma solução de recuperação de desastre que funciona bem quando as réplicas de disponibilidade estão distribuídas em distâncias consideráveis.  
  
    -   *Modo de confirmação síncrona*. Este modo de disponibilidade enfatiza a alta disponibilidade e a proteção dos dados sobre o desempenho, às custas do aumento da latência de transação. Um determinado grupo de disponibilidade pode dar suporte a até três réplicas de disponibilidade de confirmação síncrona, incluindo a réplica primária atual.  
  
     Para obter mais informações, consulte [modos de disponibilidade; Always On grupos de disponibilidade;](availability-modes-always-on-availability-groups.md).  
  
-   Dá suporte a várias formas de failover de disponibilidade-grupo: failover automático, failover manual planejado (geralmente referenciado como um "failover manual" simples) e failover manual forçado (geralmente referenciado como "failover forçado" simples). Para obter mais informações, consulte [failover e modos de failover; Always On grupos de disponibilidade;](failover-and-failover-modes-always-on-availability-groups.md).  
  
-   Permite a você configurar uma determinada réplica de disponibilidade para dar suporte a um ou ambos os seguintes recursos ativos-secundários:  
  
    -   Acesso de conexão somente leitura, que permite que conexões somente leitura com a réplica acessem e leiam seus bancos de dados quando estiver em execução como uma réplica secundária. Para obter mais informações, consulte secundários [ativos: réplicas secundárias legíveis; Always On grupos de disponibilidade](https://msdn.microsoft.com/library/ff878253.aspx)).  
  
    -   Execução de operações de backup em seus bancos de dados quando estiver em execução como uma réplica secundária. Para obter mais informações, consulte secundários [ativos: backup em réplicas secundárias](https://msdn.microsoft.com/library/ff878253.aspx)).  
  
     O uso de recursos secundários ativos melhora a eficiência de TI e reduz o custo devido à melhor utilização de recurso de hardware secundário. Além disso, descarregar aplicativos de intenção de leitura e trabalhos de backup para réplicas secundárias ajuda a melhorar o desempenho na réplica primária.  
  
-   Dá suporte a um ouvinte de grupo de disponibilidade para cada grupo de disponibilidade. Um *ouvinte de grupo de disponibilidade* é um nome de servidor ao qual os clientes podem se conectar para acessar um banco de dados em uma réplica primária ou secundária de um grupo de disponibilidade AlwaysOn. Os ouvintes de grupo de disponibilidade direcionam conexões de entrada para a réplica primária ou para uma réplica secundária somente leitura. O ouvinte fornece o failover rápido de aplicativo depois de um failover de grupo de disponibilidade. Para obter mais informações, consulte [ouvintes do grupo de disponibilidade, conectividade de cliente e failover de aplicativo; SQL Server;](../../listeners-client-connectivity-application-failover.md).  
  
-   Dá suporte a uma política de failover flexível para proporcionar maior controle sobre o failover de disponibilidade-grupo. Para obter mais informações, consulte [failover e modos de failover; Always On grupos de disponibilidade;](failover-and-failover-modes-always-on-availability-groups.md).  
  
-   Dá suporte ao conserto de página automático para proteção contra dano de página. Para obter mais informações, consulte [reparo automático de página &#40;para grupos de disponibilidade e espelhamento de banco de dados;](../../../sql-server/failover-clusters/automatic-page-repair-availability-groups-database-mirroring.md).  
  
-   Dá suporte à criptografia e compactação, que fornecem um transporte seguro de alto desempenho.  
  
-   Fornece um conjunto integrado de ferramentas para simplificar a implantação e o gerenciamento de grupos de disponibilidade, incluindo:  
  
    -   [!INCLUDE[tsql](../../../includes/tsql-md.md)] para criar e gerenciar grupos de disponibilidade. Para obter mais informações, consulte [visão geral de instruções Transact-SQL para Always on grupo de disponibilidade; SQL Server;](transact-sql-statements-for-always-on-availability-groups.md).  
  
    -   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] , como a seguir:  
  
        -   O [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)] cria e configura um grupo de disponibilidade. Em alguns ambientes, este assistente também pode preparar automaticamente os bancos de dados secundários e iniciar a sincronização de dados para cada um deles. Para obter mais informações, consulte [usar a caixa de diálogo novo grupo de disponibilidade; SQL Server Management Studio;](use-the-new-availability-group-dialog-box-sql-server-management-studio.md).  
  
        -   O [!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)] adiciona um ou mais bancos de dados primários a um grupo de disponibilidade existente. Em alguns ambientes, este assistente também pode preparar automaticamente os bancos de dados secundários e iniciar a sincronização de dados para cada um deles. Para obter mais informações, veja [Usar o Assistente para Adicionar Banco de Dados a Grupo de Disponibilidade (SQL Server)](availability-group-add-database-to-group-wizard.md).  
  
        -   O [!INCLUDE[ssAoAddRepWiz](../../../includes/ssaoaddrepwiz-md.md)] adiciona uma ou mais réplicas secundárias a um grupo de disponibilidade existente. Em alguns ambientes, este assistente também pode preparar automaticamente os bancos de dados secundários e iniciar a sincronização de dados para cada um deles. Para obter mais informações, consulte [usar o assistente para adicionar réplica ao grupo de disponibilidade; SQL Server Management Studio;](use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md).  
  
        -   O [!INCLUDE[ssAoFoAgWiz](../../../includes/ssaofoagwiz-md.md)] inicia um failover manual em um grupo de disponibilidade. Dependendo da configuração e do estado da réplica secundária que você especificar como o destino de failover, o assistente pode executar um failover planejado ou manual forçado. Para obter mais informações, consulte [usar o assistente de grupo de disponibilidade de failover; SQL Server Management Studio;](use-the-fail-over-availability-group-wizard-sql-server-management-studio.md).  
  
    -   O [!INCLUDE[ssAoDash](../../../includes/ssaodash-md.md)] monitora grupos de disponibilidade AlwaysOn, réplicas de disponibilidade e bancos de dados de disponibilidade e avalia os resultados para políticas AlwaysOn. Para obter mais informações, consulte [usar o painel AlwaysOn; SQL Server Management Studio;](use-the-always-on-dashboard-sql-server-management-studio.md).  
  
    -   O painel Detalhes do Pesquisador de Objetos exibe informações básicas sobre grupos de disponibilidade existentes. Para obter mais informações, consulte [usar os detalhes do pesquisador de objetos para monitorar o grupo de disponibilidade; SQL Server Management Studio;](use-object-explorer-details-to-monitor-availability-groups.md).  
  
    -   Cmdlets do PowerShell. Para obter mais informações, consulte [visão geral dos cmdlets do PowerShell para grupos de disponibilidade Always on; SQL serve;](overview-of-powershell-cmdlets-for-always-on-availability-groups-sql-server.md).  
  
##  <a name="terms-and-definitions"></a><a name="TermsAndDefinitions"></a>Termos e definições  
 grupo de disponibilidade  
 Um contêiner para um conjunto de bancos de dados, *bancos de dados de disponibilidade*, que executam failover juntos.  
  
 banco de dados de disponibilidade  
 Um banco de dados que pertence a um grupo de disponibilidade. Para cada banco de dados de disponibilidade, o grupo de disponibilidade mantém uma única cópia de leitura/gravação (o *banco de dados primário*) e de uma a oito cópias somente leitura (*bancos de dados secundários*).  
  
 banco de dados primário  
 A cópia de leitura-gravação de um banco de dados de disponibilidade.  
  
 banco de dados secundário  
 Uma cópia somente leitura de um banco de dados de disponibilidade.  
  
 réplica de disponibilidade  
 Uma instanciação de um grupo de disponibilidade que é hospedado por uma instância específica do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e que mantém uma cópia local de cada banco de dados de disponibilidade pertencente ao grupo de disponibilidade. Existem dois tipos de réplica de disponibilidade: uma única *réplica primária* e uma a oito *réplicas secundárias*.  
  
 réplica primária  
 A réplica de disponibilidade que torna disponíveis os bancos de dados primários para conexões de leitura/gravação de clientes e, também, envia registros do log de transações para cada banco de dados primário a toda réplica secundária.  
  
 réplica secundária  
 Uma réplica de disponibilidade que mantém uma cópia secundária de cada banco de dados de disponibilidade e serve como destinos potenciais de failover para o grupo de disponibilidade. Opcionalmente, uma réplica secundária pode incluir o suporte ao acesso somente leitura para que bancos de dados secundários possam oferecer suporte à criação de backups em bancos de dados secundários.  
  
 ouvinte do grupo de disponibilidade  
 Um nome do servidor ao qual os clientes podem se conectar para acessar um banco de dados em uma réplica primária ou secundária de um grupo de disponibilidade AlwaysOn. Os ouvintes de grupo de disponibilidade direcionam conexões de entrada para a réplica primária ou para uma réplica secundária somente leitura.  
  
> [!NOTE]  
>  Para obter mais informações, consulte [visão geral do grupos de disponibilidade AlwaysOn; SQL serve;](overview-of-always-on-availability-groups-sql-server.md).  
  
##  <a name="interoperability-and-coexistence-with-other-database-engine-features"></a><a name="Interoperability"></a>Interoperabilidade e coexistência com outros recursos de Mecanismo de Banco de Dados  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] podem ser usados com os seguintes recursos ou componentes do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:  
  
-   [Sobre a captura de dados de alterações; SQL Server;](../../../relational-databases/track-changes/about-change-data-capture-sql-server.md)  
  
-   [Sobre Controle de Alterações; SQL serve;](../../../relational-databases/track-changes/about-change-tracking-sql-server.md)  
  
-   [Bancos de dados independentes](../../../relational-databases/databases/contained-databases.md)  
  
-   [Criptografia de banco de dados](../../../relational-databases/security/encryption/transparent-data-encryption.md)  
  
-   [Instantâneos do banco de dados](database-snapshots-with-always-on-availability-groups-sql-server.md)  
  
-   [FILESTREAM](../../../relational-databases/blob/filestream-sql-server.md)  
  
-   [FileTable](../../../relational-databases/blob/filetables-sql-server.md)  
  
-   [Envio de logs](../../log-shipping/about-log-shipping-sql-server.md)  
  
-   [RBS (Armazenamento de Blob Remoto)](../../../relational-databases/blob/remote-blob-store-rbs-sql-server.md)  
  
-   [Replicação](../../install-windows/install-sql-server-replication.md)  
  
-   [Service Broker](../../configure-windows/sql-server-service-broker.md)  
  
-   [SQL Server Agent](../../../ssms/agent/sql-server-agent.md)  
  
-   [Reporting Services](reporting-services-with-always-on-availability-groups-sql-server.md)  
  
> [!WARNING]  
>  Para obter informações sobre restrições e limitações para usar outros recursos com o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] , consulte [Always on grupos de disponibilidade: interoperabilidade; SQL Server;](always-on-availability-groups-interoperability-sql-server.md).  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Introdução com grupos de disponibilidade Always On; SQL Server;](getting-started-with-always-on-availability-groups-sql-server.md)  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> Conteúdo relacionado  
  
-   **Blogs:**  
  
     [SQL Server Blogs da equipe do Always On: o blog oficial da equipe do SQL Server AlwaysOn](https://blogs.msdn.com/b/sqlalwayson/)  
  
     [Blogs dos engenheiros do CSS SQL Server](https://blogs.msdn.com/b/psssql/)  
  
-   **Vídeos:**  
  
     [Microsoft SQL Server Code-Named "Denali" Always On Series, Part 1: Introducing the Next Generation High Availability Solution](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302) (Série do Always On, codinome "Denali" do Microsoft SQL Server, parte 1: apresentando a próxima geração de solução de alta disponibilidade)  
  
     [Microsoft SQL Server o codinome "Denali" Always On série, parte 2: criando uma solução de alta disponibilidade de missão crítica usando o AlwaysOn](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
-   **Whitepapers:**  
  
     [Guia de soluções AlwaysOn do Microsoft SQL Server para alta disponibilidade e recuperação de desastre](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral de grupos de disponibilidade de Always On; SQL Server;](overview-of-always-on-availability-groups-sql-server.md)   
 [Pré-requisitos, restrições e recomendações para Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)   
 [Configuração de uma instância de servidor para grupos de disponibilidade Always On; SQL Server;](always-on-availability-groups-sql-server.md)   
 [Criação e configuração de grupos de disponibilidade; SQL Server;](creation-and-configuration-of-availability-groups-sql-server.md)   
 [Administração de um grupo de disponibilidade; SQL Server;](administration-of-an-availability-group-sql-server.md)   
 [Monitoramento de grupos de disponibilidade &#40;SQL Server&#41;](monitoring-of-availability-groups-sql-server.md)   
 [Visão geral de instruções Transact-SQL para grupos de disponibilidade Always On; SQL Server;](transact-sql-statements-for-always-on-availability-groups.md)   
 [Visão geral dos cmdlets do PowerShell para Grupos de Disponibilidade AlwaysOn; SQL Server;](overview-of-powershell-cmdlets-for-always-on-availability-groups-sql-server.md)  
  
