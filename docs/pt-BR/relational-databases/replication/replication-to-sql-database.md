---
title: Replicação para Banco de Dados SQL | Microsoft Docs
ms.custom: ''
ms.date: 04/24/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQL Database replication
- replication, SQL Database
ms.assetid: e8484da7-495f-4dac-b38e-bcdc4691f9fa
caps.latest.revision: 15
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: On Demand
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 8de5356d33d2ea5805b4befded6e75c41d3997b5
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="replication-to-sql-database"></a>Replicação para banco de dados SQL
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  A replicação do[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode ser configurada para o [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)].  
 
 ### <a name="supported-configurations"></a>**Configurações com suporte:**  
 -  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode ser uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em execução local ou uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em execução em uma máquina virtual do Azure na nuvem. Para obter mais informações, consulte [Visão geral do SQL Server em máquinas virtuais do Azure](https://azure.microsoft.com/documentation/articles/virtual-machines-sql-server-infrastructure-services/).  
 - [!INCLUDE[ssSDS](../../includes/sssds-md.md)] deve ser um assinante de push de um publicador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
 -  O banco de dados de distribuição e os agentes de replicação não podem ser colocados no [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
 - Somente há suporte para a replicação transacional unidirecional. Não há suporte para a replicação transacional ponto a ponto e replicação de mesclagem.  
 
 ## <a name="versions"></a>Versões  
 - O editor e o distribuidor devem estar em pelo menos uma das seguintes versões:  
   
 -   [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)]  
 
 -   [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]  
   
 -   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP1 CU3  
   
 -   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] RTM CU10  
   
 -   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 CU8  
   
 -   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] previsto em SP3  
   
 - Tentar configurar a replicação usando uma versão mais antiga pode resultar no erro número MSSQL_REPL20084 (O processo não pôde conectar ao assinante.) e MSSQL_REPL40532 (Não é possível abrir o servidor \<name> solicitado pelo logon. Falha no logon.).  
 
 - O assinante do [!INCLUDE[ssSDS](../../includes/sssds-md.md)] deve ter pelo menos V12 e pode estar em qualquer região.  
   
 - Para usar todos os recursos de [!INCLUDE[ssSDS](../../includes/sssds-md.md)], você deve usar as versões mais recentes do [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) e [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx).  
   
 ## <a name="remarks"></a>Remarks  
 - A replicação pode ser configurada usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou executando instruções do [!INCLUDE[tsql](../../includes/tsql-md.md)] no editor. Não é possível configurar a replicação usando o portal do [!INCLUDE[ssSDS](../../includes/sssds-md.md)] .  
   
 - A replicação só pode usar logons de autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para se conectar ao [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
   
 - A tabela replicada deve ter uma chave primária.  
   
 - Você deve ter uma assinatura existente do Azure e uma existente do [!INCLUDE[ssSDS](../../includes/sssds-md.md)] V12.  
   
 - Uma única publicação no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode oferecer suporte a ambos os assinantes, [!INCLUDE[ssSDS](../../includes/sssds-md.md)] e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (local e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em uma máquina virtual do Azure).  
   
 - Gerenciamento, monitoramento e solução de problemas de replicação devem ser executados por meio do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]local.  
   
 - Apenas assinaturas por push do [!INCLUDE[ssSDS](../../includes/sssds-md.md)] têm suporte.  
   
 - Somente `@subscriber_type = 0` tem suporte em **sp_addsubscription** para o banco de dados SQL.  
   
 - O[!INCLUDE[ssSDS](../../includes/sssds-md.md)] não oferece suporte a replicação bidirecional, imediata, atualizável ou ponto a ponto.      
   
 ## <a name="replication-architecture"></a>Arquitetura de replicação  
 ![replication-to-sql-database](../../relational-databases/replication/media/replication-to-sql-database.png "replication-to-sql-database")  
   
 ## <a name="scenarios"></a>Cenários  
   
 ### <a name="typical-replication-scenario"></a>Cenário típico de replicação  
   
 1.  Crie uma publicação de replicação transacional em um banco de dados local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
   
 2.  No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] local, use o **Assistente para nova assinatura** ou as instruções do [!INCLUDE[tsql](../../includes/tsql-md.md)] para criar um push de assinatura para o [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
   
 3.  O conjunto de dados inicial normalmente é um instantâneo criado pelo Snapshot Agent e distribuído e aplicado pelo Distribution Agent. O conjunto de dados inicial também pode ser fornecido por meio de um backup ou outros meios, como [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
   
 #### <a name="data-migration-scenario"></a>Cenário de migração de dados  
   
 1.  Use a replicação transacional para replicar dados de um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] local para [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
   
 2.  Redirecione os aplicativos cliente ou de camada intermediária para atualizar a cópia do [!INCLUDE[ssSDS](../../includes/sssds-md.md)] .  
   
 3.  Pare de atualizar a versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da tabela e remova a publicação.  
   
 ## <a name="limitations"></a>Limitações  
  Não há suporte para as seguintes opções para assinaturas do [!INCLUDE[ssSDS](../../includes/sssds-md.md)] :  
   
 -   Copiar associação de grupos de arquivos  
   
 -   Copiar esquemas de particionamento de tabela  
   
 -   Copiar esquemas de particionamento de índice  
   
 -   Copiar estatísticas definidas pelo usuário  
   
 -   Copiar associações padrão  
   
 -   Copiar associações de regra  
   
 -   Copiar índices de texto completo  
   
 -   Copiar XML XSD  
   
 -   Copiar índices XML  
   
 -   Copiar permissões  
   
 -   Copiar índices espaciais  
   
 -   Copiar índices filtrados  
   
 -   Copiar atributo de compactação de dados  
   
 -   Copiar atributo de coluna esparsa  
   
 -   Converter fluxo de arquivos em tipos de dados MAX  
   
 -   Converter hierarchyid em tipos de dados MAX  
   
 -   Converter espacial em tipos de dados MAX  
   
 -   Copiar propriedades estendidas  
   
 -   Copiar permissões  
   
### <a name="limitations-to-be-determined"></a>Limitações a serem determinadas 
 
 -   Copiar agrupamento  
   
 -   Execução em uma transação serializável do SP  
   
 ## <a name="examples"></a>Exemplos  
  Crie uma publicação e uma assinatura por push. Para obter mais informações, consulte:  
   
 -   [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)  
   
 -   [Crie uma assinatura push](../../relational-databases/replication/create-a-push-subscription.md) usando o nome do servidor lógico [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] como o assinante (por exemplo **N'azuresqldbdns.database.windows.net'**) e o nome [!INCLUDE[ssSDS](../../includes/sssds-md.md)] como o banco de dados de destino (por exemplo **AdventureWorks**).  
   
 ## <a name="see-also"></a>Consulte Também  
 - [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 - [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 - [Tipos de replicação](../../relational-databases/replication/types-of-replication.md)   
 - [Monitoramento &#40;replicação&#41;](../../relational-databases/replication/monitor/monitoring-replication.md)   
 - [Inicializar uma assinatura](../../relational-databases/replication/initialize-a-subscription.md)  
