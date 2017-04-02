---
title: "Replica&#231;&#227;o para Banco de Dados SQL | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "06/29/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Replicação do banco de dados SQL"
  - "replicação, banco de dados SQL"
ms.assetid: e8484da7-495f-4dac-b38e-bcdc4691f9fa
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 15
---
# Replica&#231;&#227;o para Banco de Dados SQL
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a replicação pode ser configurada para [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)].  
  
 **Configurações com suporte:**  
  
-   O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode ser uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em execução no local ou uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em execução em uma máquina virtual do Azure na nuvem. Para saber mais, confira [Visão geral do SQL Server em máquinas virtuais do Azure](https://azure.microsoft.com/documentation/articles/virtual-machines-sql-server-infrastructure-services/).  
  
-   [!INCLUDE[ssSDS](../../includes/sssds-md.md)] deve ser um assinante de envio de um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador.  
  
-   O banco de dados de distribuição e os agentes de replicação não podem ser colocados em [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
-   Somente há suporte para a replicação transacional unidirecional. Não há suporte para a replicação transacional ponto a ponto e replicação de mesclagem.  
  
## Versões  
 O editor e o distribuidor devem estar em pelo menos uma das seguintes versões:  
  
-   [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP1 CU3  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] RTM CU10  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 CU8  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] esperado no SP3  
  
 Tentativa de configurar a replicação usando uma versão mais antiga pode resultar em erro número MSSQL_REPL20084 (o processo não pôde conectar ao assinante.) e MSSQL_REPL40532 (não é possível abrir \< nome> solicitado pelo logon. Falha no logon.).  
  
 O [!INCLUDE[ssSDS](../../includes/sssds-md.md)] assinante deve ter pelo menos V12 e podem estar em qualquer região.  
  
 Para usar todos os recursos de [!INCLUDE[ssSDS](../../includes/sssds-md.md)] deve estar usando as versões mais recentes de [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) e [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx).  
  
## Comentários  
 A replicação pode ser configurada usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou executando [!INCLUDE[tsql](../../includes/tsql-md.md)] instruções no Editor. Você não pode configurar a replicação usando o [!INCLUDE[ssSDS](../../includes/sssds-md.md)] portal.  
  
 Replicação só pode usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logons de autenticação para se conectar ao [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 A tabela replicada deve ter uma chave primária.  
  
 Você deve ter uma assinatura existente e existente [!INCLUDE[ssSDS](../../includes/sssds-md.md)] V12.  
  
 Uma única publicação em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode oferecer suporte a ambos [!INCLUDE[ssSDS](../../includes/sssds-md.md)] e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (local e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em uma máquina virtual do Azure) os assinantes.  
  
 Gerenciamento de replicação, monitoramento e solução de problemas deve ser executada do local [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Apenas enviar assinaturas [!INCLUDE[ssSDS](../../includes/sssds-md.md)] têm suporte.  
  
 Somente `@subscriber_type = 0` tem suporte em **sp_addsubscription** banco de dados SQL.  
  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] não oferece suporte a replicação bidirecional, imediata, atualizável ou ponto a ponto.  
  
## Arquitetura de replicação  
 ![replication-to-sql-database](../../relational-databases/replication/media/replication-to-sql-database.png "replication-to-sql-database")  
  
## Cenários  
  
#### Cenário típico de replicação  
  
1.  Criar uma publicação de replicação transacional em um local [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados.  
  
2.  No local [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usar o **Assistente para nova assinatura** ou [!INCLUDE[tsql](../../includes/tsql-md.md)] instruções para criar um envio para assinatura [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
3.  O conjunto de dados inicial normalmente é um instantâneo criado pelo Snapshot Agent e distribuído e aplicado pelo Distribution Agent. O conjunto de dados inicial também pode ser fornecido por meio de um backup ou outros meios, como [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
#### Cenário de migração de dados  
  
1.  Usar a replicação transacional para replicar dados de um local [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
2.  Redirecionar os aplicativos cliente ou de camada intermediária para atualizar o [!INCLUDE[ssSDS](../../includes/sssds-md.md)] cópia.  
  
3.  Interromper a atualização do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versão da tabela e remover a publicação.  
  
## Limitações  
 Não há suporte para as seguintes opções para [!INCLUDE[ssSDS](../../includes/sssds-md.md)] assinaturas:  
  
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
  
 Limitações a serem determinadas:  
  
-   Copiar agrupamento  
  
-   Execução em uma transação serializável do SP  
  
## Exemplos  
 Crie uma publicação e uma assinatura por push. Para obter mais informações, consulte:  
  
-   [Crie uma publicação](../../relational-databases/replication/publish/create-a-publication.md)  
  
-   [Criar uma assinatura Push](../../relational-databases/replication/create-a-push-subscription.md) usando o [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] nome do servidor lógico como o assinante (por exemplo **N'azuresqldbdns.database.windows.net'**) e o [!INCLUDE[ssSDS](../../includes/sssds-md.md)] nome do banco de dados de destino (por exemplo **AdventureWorks**).  
  
## Consulte também  
 [Crie uma publicação](../../relational-databases/replication/publish/create-a-publication.md)   
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [Tipos de replicação](../../relational-databases/replication/types-of-replication.md)   
 [Monitoramento e 40; Replicação e 41;](../../relational-databases/replication/monitor/monitoring-replication.md)   
 [Inicializar uma assinatura](../../relational-databases/replication/initialize-a-subscription.md)  
  
  