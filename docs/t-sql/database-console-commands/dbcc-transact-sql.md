---
title: DBCC (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DBCC
- DBCC_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- transactional consistency
- Database Console Command statements
- status information [SQL Server], DBCC statements
- snapshots [SQL Server database snapshots], DBCC statements
- emergency database state [SQL Server]
- TABLOCK
- internal database snapshots [SQL Server]
- reporting DBCC statement progress
- logical consistency of data [SQL Server]
- DBCC statements
- validation statements [SQL Server]
- miscellaneous statements [SQL Server]
- statements [SQL Server], DBCC statements
- DBCC commands [SQL Server]
- result sets [SQL Server], DBCC statements
- maintenance statements [SQL Server]
- physical consistency of data [SQL Server]
- current DBCC statement status
- progress reporting [DBCC statements]
- informational statements [SQL Server]
ms.assetid: c6da8c04-5b6b-459a-9f76-110c92ca8b29
caps.latest.revision: 50
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8e8750f4b44ec206bb5a26586acd6b567f7dac37
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-transact-sql"></a>DBCC (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

A linguagem de programação [!INCLUDE[tsql](../../includes/tsql-md.md)] fornece instruções DBCC que atuam como comandos de console de banco de dados para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
As instruções de console de comando de banco de dados são agrupadas nas categorias a seguir.
  
|Categoria de comando|Executar|  
|---|---|
|Manutenção|Tarefas de manutenção em um banco de dados, índice ou grupo de arquivos.|  
|Diversos|Tarefas diversas, como habilitar sinalizadores de rastreamento ou remover uma DLL da memória.|  
|Informational|Tarefas que reúnem e exibem vários tipos de informações.|  
|Validação|Operações de validação em um banco de dados, tabela, índice, catálogo, grupo de arquivos ou alocação de páginas de banco de dados.|  
  
Os comandos DBCC assumem os parâmetros de entrada e retornam valores. Todos os parâmetros de comando DBCC aceitam literais Unicode e DBCS.
  
## <a name="dbcc-internal-database-snapshot-usage"></a>Uso de instantâneo de banco de dados interno DBCC  
Os comandos DBCC a seguir operam em um instantâneo de banco de dados interno somente leitura, criado pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Isso evita bloqueio e problemas de simultaneidade quando esses comandos são executados. Para obter mais informações, consulte [Instantâneos de banco de dados &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md).
- DBCC CHECKALLOC
- DBCC CHECKCATALOG
- DBCC CHECKDB
- DBCC CHECKFILEGROUP
- DBCC CHECKTABLE

Quando você executa um desses comandos DBCC, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] cria um instantâneo do banco de dados e o leva para um estado consistente de maneira transacional. O comando DBCC executa as verificações segundo esse instantâneo. Depois que o comando DBCC é concluído, o instantâneo é descartado.
  
Às vezes um instantâneo de banco de dados interno não é necessário ou não pode ser criado. Quando isso ocorre, o comando DBCC é executado no banco de dados real. Se o banco de dados estiver online, o comando DBCC usará o bloqueio de tabela para assegurar a consistência dos objetos que está verificando. Esse comportamento equivale a ter a opção WITH TABLOCK especificada.
  
O instantâneo de banco de dados interno não é criado quando um comando DBCC é executado:
-   Contra **mestre**e a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está sendo executado no modo de usuário único.  
-   Em um banco de dados diferente de **mestre**, mas o banco de dados foi colocado em modo de usuário único usando a instrução ALTER DATABASE.  
-   Em um banco de dados somente leitura.  
-   Em um banco de dados definido como modo de emergência usando a instrução ALTER DATABASE.  
-   Contra **tempdb**. Nesse caso, o instantâneo de banco de dados não pode ser criado em razão de restrições internas.  
-   Usando a opção WITH TABLOCK. Nesse caso, o DBCC honra a solicitação e não cria um instantâneo de banco de dados.  
  
Os comandos DBCC usam bloqueio de tabela em vez de instantâneos de banco de dados internos quando o comando é executado de acordo com:
-   Um grupo de arquivos somente leitura  
-   Um sistema de arquivos FAT  
-   Um volume que não oferece suporte a 'named streams'  
-   Um volume que não oferece suporte a 'alternate streams'  
  
> [!NOTE]  
>  A tentativa de executar DBCC CHECKALLOC, ou parte equivalente de DBCC CHECKDB, usando a opção WITH TABLOCK requer bloqueio X de banco de dados. Esse bloqueio de banco de dados não pode ser definido em **tempdb** ou **mestre** e talvez falhe em todos os outros bancos de dados.  
  
> [!NOTE]  
>  Falha no DBCC CHECKDB quando ele é executado no **mestre** se um instantâneo de banco de dados interno não pode ser criado.  
  
## <a name="progress-reporting-for-dbcc-commands"></a>Relatório de andamento de comandos DBCC  
O **exec_requests** exibição de catálogo contém informações sobre o andamento e a fase atual da execução dos comandos DBCC CHECKDB, CHECKFILEGROUP e CHECKTABLE. O **percent_complete** coluna indica a porcentagem total do comando e o **comando** coluna informa a fase atual da execução do comando.
  
A definição de uma unidade de andamento depende da fase atual de execução do comando DBCC. O andamento é informado ocasionalmente na granularidade de uma página de banco de dados. Em outras fases ele é informado da granularidade de um único banco de dados ou correção de alocação. A tabela a seguir descreve cada fase da execução e a granularidade em que o comando informa sobre o andamento.
  
|Fase de execução|Description|Granularidade do relatório de andamento|  
|---------------------|-----------------|------------------------------------|  
|DBCC TABLE CHECK|A consistência lógica e física dos objetos no banco de dados é verificada nessa fase.|Andamento relatado no nível da página do banco de dados.<br /><br /> O valor de relatório de andamento é atualizado para cada banco de dados de 1000 páginas que são verificados.|  
|DBCC TABLE REPAIR|As correções de banco de dados são executadas nessa fase, se REPAIR_FAST, REPAIR_REBUILD ou REPAIR_ALLOW_DATA_LOSS for especificado e houver erros de objeto que precisem ser corrigidos.|Andamento relatado no nível de correção individual.<br /><br /> O contador é atualizado para todas as correções concluídas.|  
|DBCC ALLOC CHECK|As estruturas de alocação do banco de dados são verificadas durante essa fase.<br /><br /> Observação: O DBCC CHECKALLOC executa as mesmas verificações.|Andamento não é relatado.|  
|DBCC ALLOC REPAIR|As correções de banco de dados são realizadas nessa fase se REPAIR_FAST, REPAIR_REBUILD ou REPAIR_ALLOW_DATA_LOSS for especificado e houver erros de alocação que precisem ser corrigidos.|O andamento não é relatado.|  
|DBCC SYS CHECK|As tabelas do sistema de banco de dados são verificadas nessa fase.|Andamento relatado no nível da página do banco de dados.<br /><br /> O valor do relatório de andamento é atualizado a cada 1.000 páginas do banco de dados verificado.|  
|DBCC SYS REPAIR|As correções de banco de dados são realizadas nessa fase se REPAIR_FAST, REPAIR_REBUILD ou REPAIR_ALLOW_DATA_LOSS for especificado e houver erros de tabelas do sistema que precisem ser corrigidos.|Andamento relatado no nível de correção individual.<br /><br /> O contador é atualizado para todas as correções concluídas.|  
|DBCC SSB CHECK|Os objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agente de Serviços são verificados nessa fase.<br /><br /> Observação: Nesta fase não é executada quando DBCC CHECKTABLE for executado.|O andamento não é relatado.|  
|DBCC CHECKCATALOG|A consistência dos catálogos de banco de dados é verificada nessa fase.<br /><br /> Observação: Nesta fase não é executada quando DBCC CHECKTABLE for executado.|O andamento não é relatado.|  
|DBCC IVIEW CHECK|A consistência lógica de todas as exibições indexadas presentes no banco de dados é verificada nessa fase.|O andamento é relatado no nível da exibição de banco de dados individual que está sendo verificada.|  
  
## <a name="informational-statements"></a>Instruções informativas  
  
|||  
|-|-|  
|[DBCC INPUTBUFFER](../../t-sql/database-console-commands/dbcc-inputbuffer-transact-sql.md)|[DBCC SHOWCONTIG](../../t-sql/database-console-commands/dbcc-showcontig-transact-sql.md)|  
|[DBCC OPENTRAN](../../t-sql/database-console-commands/dbcc-opentran-transact-sql.md)|[DBCC SQLPERF](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md)|  
|[DBCC OUTPUTBUFFER](../../t-sql/database-console-commands/dbcc-outputbuffer-transact-sql.md)|[DBCC TRACESTATUS](../../t-sql/database-console-commands/dbcc-tracestatus-transact-sql.md)|  
|[DBCC PROCCACHE](../../t-sql/database-console-commands/dbcc-proccache-transact-sql.md)|[DBCC USEROPTIONS](../../t-sql/database-console-commands/dbcc-useroptions-transact-sql.md)|  
|[DBCC SHOW_STATISTICS](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)||  
  
## <a name="validation-statements"></a>Instruções de validação  
  
|||  
|-|-|  
|[DBCC CHECKALLOC](../../t-sql/database-console-commands/dbcc-checkalloc-transact-sql.md)|[DBCC CHECKFILEGROUP](../../t-sql/database-console-commands/dbcc-checkfilegroup-transact-sql.md)|  
|[DBCC CHECKCATALOG](../../t-sql/database-console-commands/dbcc-checkcatalog-transact-sql.md)|[DBCC CHECKIDENT](../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md)|  
|[DBCC CHECKCONSTRAINTS](../../t-sql/database-console-commands/dbcc-checkconstraints-transact-sql.md)|[DBCC CHECKTABLE](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)|  
|[DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)||  
  
## <a name="maintenance-statements"></a>Instruções de manutenção  
  
|||  
|-|-|  
|[DBCC CLEANTABLE](../../t-sql/database-console-commands/dbcc-cleantable-transact-sql.md)|[DBCC INDEXDEFRAG](../../t-sql/database-console-commands/dbcc-indexdefrag-transact-sql.md)|  
|[DBCC DBREINDEX](../../t-sql/database-console-commands/dbcc-dbreindex-transact-sql.md)|[DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md)|  
|[DBCC DROPCLEANBUFFERS](../../t-sql/database-console-commands/dbcc-dropcleanbuffers-transact-sql.md)|[DBCC SHRINKFILE](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md)|  
|[DBCC FREEPROCCACHE](../../t-sql/database-console-commands/dbcc-freeproccache-transact-sql.md)|[DBCC UPDATEUSAGE](../../t-sql/database-console-commands/dbcc-updateusage-transact-sql.md)|  
  
## <a name="miscellaneous-statements"></a>Instruções diversas  
  
|||  
|-|-|  
|[Nomedadll DBCC (FREE)](../../t-sql/database-console-commands/dbcc-dllname-free-transact-sql.md)|[AJUDA DO DBCC](../../t-sql/database-console-commands/dbcc-help-transact-sql.md)|  
|[DBCC FLUSHAUTHCACHE](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md)|[DBCC TRACEOFF](../../t-sql/database-console-commands/dbcc-traceoff-transact-sql.md)|  
|[DBCC FREESESSIONCACHE](../../t-sql/database-console-commands/dbcc-freesessioncache-transact-sql.md)|[DBCC TRACEON](../../t-sql/database-console-commands/dbcc-traceon-transact-sql.md)|  
|[DBCC FREESYSTEMCACHE](../../t-sql/database-console-commands/dbcc-freesystemcache-transact-sql.md)|[DBCC CLONEDATABASE](https://support.microsoft.com/en-us/kb/3177838) <br /><br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Service Pack 2.|  
  
  

