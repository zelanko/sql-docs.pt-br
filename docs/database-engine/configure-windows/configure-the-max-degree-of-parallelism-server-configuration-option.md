---
title: Configurar a opção de configuração de servidor max degree of parallelism | Microsoft Docs
ms.custom: ''
ms.date: 02/12/2020
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- parallel queries [SQL Server]
- processors [SQL Server], parallel queries
- number of processors for parallel queries
- max degree of parallelism option
- MaxDop
ms.assetid: 86b65bf1-a6a1-4670-afc0-cdfad1558032
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 47b9704591acd305a49ff315eb99314f14e87af1
ms.sourcegitcommit: 38c61c7e170b57dddaae5be72239a171afd293b9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2020
ms.locfileid: "77259222"
---
# <a name="configure-the-max-degree-of-parallelism-server-configuration-option"></a>Configurar a opção de configuração de servidor max degree of parallelism
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Este tópico descreve como configurar a opção de configuração de servidor **MAXDOP (grau máximo de paralelismo)** no SQL Server usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Quando uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é executada em um computador com mais de um microprocessador ou CPU, ele detecta o grau de paralelismo, ou seja, o número de processadores utilizados para executar uma única instrução, para cada execução paralela de plano. Você pode usar a opção **max degree of parallelism** para limitar o número de processadores a serem usados na execução de plano paralela. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] considera os planos de execução paralela para consultas, operações DDL (linguagem de definição de dados), inserções paralelas, alteração online de coluna, coleta de estatísticas paralela e população de cursor estático e controlado por conjunto de chaves.

> [!NOTE]
> [!INCLUDE [sssqlv15-md](../../includes/sssqlv15-md.md)] apresenta recomendações automáticas para configurar o MAXDOP durante o processo de instalação. A interface do usuário de instalação permite que você aceite as configurações recomendadas ou as personalize. Para obter mais informações, consulte os seguintes artigos:
>  - [MaxDOP adicionado à instalação do SQL 2019](https://techcommunity.microsoft.com/t5/premier-field-engineering/maxdop-added-to-sql-2019-ctp3-0-setup/ba-p/780071)
>  - [Aprimoramentos da instalação do SQL Server 2019 para MAXDOP e memória máxima](https://www.mssqltips.com/sqlservertip/6211/sql-server-2019-installation-enhancements-for-maxdop-and-max-memory/)
>

##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Se a opção de máscara de afinidade não estiver definida com o padrão, poderá restringir o número de processadores disponíveis para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em sistemas SMP simétricos.  

-   O limite de **MAXDOP (grau máximo de paralelismo)** é definido por [tarefa](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md). Não é um limite por [solicitação](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md) ou por consulta. Isso significa que, durante uma execução de consulta paralela, uma solicitação única pode gerar várias tarefas que são atribuídas a um agendador. Para saber mais, confira o [Guia de arquitetura de threads e tarefas](../../relational-databases/thread-and-task-architecture-guide.md). 
  
###  <a name="Recommendations"></a> Recomendações  
  
-   Esta é uma opção avançada e deve ser alterada somente por um administrador de banco de dados experiente ou por um profissional de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] certificado.  
  
-   Para permitir que o servidor determine o grau máximo de paralelismo, defina essa opção como 0, o valor padrão. A definição do grau máximo de paralelismo como 0 permite que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] use todos os processadores disponíveis, até 64 processadores. Para suprimir a geração de plano paralelo, defina **max degree of parallelism** como 1. Defina o valor como um número de 1 a 32.767 para especificar o número máximo de núcleos de processador que podem ser usados por uma única execução de consulta. Se um valor maior do que o número de processadores disponíveis for especificado, o número real de processadores disponíveis será usado. Se o computador tiver só um processador, o valor **grau máximo de paralelismo** será ignorado.  
  
-   Você pode substituir o valor max degree of parallelism nas consultas ao especificar a dica de consulta MAXDOP na instrução de consulta. Para obter mais informações, veja [Dicas de consulta &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md).  
  
-   As operações de índice que criam ou reconstroem um índice ou descartam um índice clusterizado podem usar muitos recursos. Você pode substituir o valor max degree of parallelism das operações de índice especificando a opção de índice MAXDOP na instrução de índice. O valor MAXDOP é aplicado à instrução no tempo de execução e não é armazenado nos metadados do índice. Para obter mais informações, consulte [Configurar operações de índice paralelo](../../relational-databases/indexes/configure-parallel-index-operations.md).  
  
-   Além das consultas e das operações de índice, essa opção também controla o paralelismo de DBCC CHECKTABLE, DBCC CHECKDB e DBCC CHECKFILEGROUP. É possível desabilitar a execução paralela de planos para essas instruções usando o sinalizador de rastreamento 2528. Para obter mais informações, veja, [Sinalizadores de rastreamento &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).

> [!TIP]
> Para fazer isso no nível da consulta, use o **MAXDOP**, [dica de consulta](../../t-sql/queries/hints-transact-sql-query.md).     
> Para fazer isso no nível do banco de dados, use a [configuração com escopo no banco de dados](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) do **MAXDOP**.      
> Para fazer isso no nível de carga de trabalho, use a [opção de configuração de grupo de carga de trabalho do Resource Governor](../../t-sql/statements/create-workload-group-transact-sql.md) **MAX_DOP**.      

###  <a name="Guidelines"></a> Diretrizes  
A partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], durante a inicialização do serviço, se o [!INCLUDE[ssde_md](../../includes/ssde_md.md)] detectar mais de oito núcleos por nó NUMA ou soquete na inicialização, os nós soft-NUMA serão criados automaticamente por padrão. O [!INCLUDE[ssde_md](../../includes/ssde_md.md)] coloca os processadores lógicos do mesmo núcleo físico em nós soft-NUMA diferentes. As recomendações na tabela a seguir visam manter todos os threads de trabalho de uma consulta paralela dentro do mesmo nó soft-NUMA. Isso melhorará o desempenho das consultas e a distribuição de threads de trabalho em todos os nós NUMA para a carga de trabalho. Para obter mais informações, veja [Soft-NUMA](../../database-engine/configure-windows/soft-numa-sql-server.md).

A partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], use as seguintes diretrizes ao configurar o valor de configuração de servidor **grau máximo de paralelismo**:

||||
|----------------|-----------------|-----------------|
|Servidor com um único nó NUMA|Menor ou igual a 8 processadores lógicos|Manter MAXDOP com o mesmo número ou abaixo do número de processadores lógicos|
|Servidor com um único nó NUMA|Mais de 8 processadores lógicos|Manter MAXDOP em 8|
|Servidor com vários nós NUMA|Menor ou igual a 16 processadores lógicos por nó NUMA|Manter MAXDOP com o mesmo número ou abaixo do número de processadores lógicos por nó NUMA|
|Servidor com vários nós NUMA|Mais de 16 processadores lógicos por nó NUMA|Manter MAXDOP em metade do número de processadores lógicos por nó NUMA com um valor MAX de 16|
  
> [!NOTE]
> O nó NUMA na tabela acima refere-se a nós soft-NUMA criados automaticamente pelo [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e versões superiores ou nós NUMA baseados em hardware caso soft-NUMA tenha sido desabilitado.   
>  Use essas mesmas diretrizes ao definir a opção grau máximo de paralelismo para os grupos de carga de trabalho Resource Governor. Para obter mais informações, veja [CREATE WORKLOAD GROUP (Transact-SQL)](../../t-sql/statements/create-workload-group-transact-sql.md).
  
Em [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] a [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], use as seguintes diretrizes ao configurar o valor de configuração de servidor **grau máximo de paralelismo**:

||||
|----------------|-----------------|-----------------|
|Servidor com um único nó NUMA|Menor ou igual a 8 processadores lógicos|Manter MAXDOP com o mesmo número ou abaixo do número de processadores lógicos|
|Servidor com um único nó NUMA|Mais de 8 processadores lógicos|Manter MAXDOP em 8|
|Servidor com vários nós NUMA|Menor ou igual a 8 processadores lógicos por nó NUMA|Manter MAXDOP com o mesmo número ou abaixo do número de processadores lógicos por nó NUMA|
|Servidor com vários nós NUMA|Mais de 8 processadores lógicos por nó NUMA|Manter MAXDOP em 8|
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Permissões de execução sem parâmetros ou com apenas o primeiro parâmetro em **sp_configure** são concedidas a todos os usuários por padrão. Para executar **sp_configure** com ambos os parâmetros para alterar uma opção de configuração ou executar a instrução RECONFIGURE, o usuário deve ter a permissão ALTER SETTINGS no nível do servidor. A permissão ALTER SETTINGS é implicitamente mantida pelas funções de servidor fixas **sysadmin** e **serveradmin** .  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-configure-the-max-degree-of-parallelism-option"></a>Para configurar a opção max degree of parallelism  
  
1.  No **Pesquisador de Objetos**, clique com o botão direito do mouse em um servidor e selecione **Propriedades**.  
  
2.  Clique no nó **Avançado** .  
  
3.  Na caixa **Grau Máximo de Paralelismo** , selecione o número máximo de processadores a serem usados na execução de plano paralelo.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-configure-the-max-degree-of-parallelism-option"></a>Para configurar a opção max degree of parallelism  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo mostra como usar o [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) para configurar a opção `max degree of parallelism` como `8`.  
  
```sql  
USE AdventureWorks2012 ;  
GO   
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE WITH OVERRIDE;  
GO  
EXEC sp_configure 'max degree of parallelism', 16;  
GO  
RECONFIGURE WITH OVERRIDE;  
GO  
```  
  
 Para obter mais informações, veja [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
##  <a name="FollowUp"></a> Acompanhamento: depois de configurar a opção grau máximo de paralelismo  
 A configuração entra em vigor imediatamente sem reiniciar o servidor.  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)      
 [Recomendações e diretrizes para a opção de configuração "grau máximo de paralelismo" do SQL Server](https://support.microsoft.com/help/2806535)     
 [Opção affinity mask de configuração de servidor](../../database-engine/configure-windows/affinity-mask-server-configuration-option.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [Guia de arquitetura de processamento de consultas](../../relational-databases/query-processing-architecture-guide.md#DOP)       
 [Guia de arquitetura de threads e tarefas](../../relational-databases/thread-and-task-architecture-guide.md)    
 [Configurar operações de índice paralelo](../../relational-databases/indexes/configure-parallel-index-operations.md)    
 [Dicas de consulta &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md)     
 [Definir opções de índice](../../relational-databases/indexes/set-index-options.md)     
