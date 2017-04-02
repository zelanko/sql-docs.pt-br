---
title: "Configurar a op&#231;&#227;o de configura&#231;&#227;o de servidor max degree of parallelism | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "consultas paralelas [SQL Server]"
  - "processadores [SQL Server], consultas paralelas"
  - "número de processadores para consultas paralelas"
  - "opção max degree of parallelism"
ms.assetid: 86b65bf1-a6a1-4670-afc0-cdfad1558032
caps.latest.revision: 33
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 33
---
# Configurar a op&#231;&#227;o de configura&#231;&#227;o de servidor max degree of parallelism
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Este tópico descreve como configurar a opção de configuração de servidor **max degree of parallelism (MAXDOP)** no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Quando uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é executada em um computador com mais de um microprocessador ou CPU, ele detecta o melhor grau de paralelismo, ou seja, o número de processadores utilizados para executar uma única instrução, para cada execução paralela de plano. Você pode usar a opção **max degree of parallelism** para limitar o número de processadores a serem usados na execução de plano paralela. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] considera os planos de execução paralela para consultas, operações DDL (linguagem de definição de dados), inserção paralela, alteração online de coluna, coleta de estatísticas paralela e população de cursor estático e controlado por conjunto de chaves.
 

  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Se a opção de máscara de afinidade não estiver definida com o padrão, poderá restringir o número de processadores disponíveis para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em sistemas SMP simétricos.  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   Esta é uma opção avançada e deve ser alterada somente por um administrador de banco de dados experiente ou técnico certificado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Para permitir que o servidor determine o grau máximo de paralelismo, defina essa opção como 0, o valor padrão. A definição do grau máximo de paralelismo como 0 permite que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] use todos os processadores disponíveis, até 64 processadores. Para suprimir a geração de plano paralelo, defina **max degree of parallelism** como 1. Defina o valor como um número de 1 a 32.767 para especificar o número máximo de núcleos de processador que podem ser usados por uma única execução de consulta. Se um valor maior do que o número de processadores disponíveis for especificado, o número real de processadores disponíveis será usado. Se o computador tiver só um processador, o valor **grau máximo de paralelismo** será ignorado.  
  
-   Você pode substituir o valor max degree of parallelism nas consultas ao especificar a dica de consulta MAXDOP na instrução de consulta. Para obter mais informações, veja [Dicas de consulta &#40;Transact-SQL&#41;](../Topic/Query%20Hints%20\(Transact-SQL\).md).  
  
-   As operações de índice que criam ou reconstroem um índice ou descartam um índice clusterizado podem usar muitos recursos. Você pode substituir o valor max degree of parallelism das operações de índice especificando a opção de índice MAXDOP na instrução de índice. O valor MAXDOP é aplicado à instrução no tempo de execução e não é armazenado nos metadados do índice. Para obter mais informações, consulte [Configurar operações de índice paralelo](../../relational-databases/indexes/configure-parallel-index-operations.md).  
  
-   Além das consultas e das operações de índice, essa opção também controla o paralelismo de DBCC CHECKTABLE, DBCC CHECKDB e DBCC CHECKFILEGROUP. É possível desabilitar a execução paralela de planos para essas instruções usando o sinalizador de rastreamento 2528. Para obter mais informações, veja, [Sinalizadores de rastreamento &#40;Transact-SQL&#41;](../Topic/Trace%20Flags%20\(Transact-SQL\).md).  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Permissões de execução sem parâmetros ou com apenas o primeiro parâmetro em **sp_configure** são concedidas a todos os usuários por padrão. Para executar **sp_configure** com ambos os parâmetros para alterar uma opção de configuração ou executar a instrução RECONFIGURE, o usuário deve ter a permissão ALTER SETTINGS no nível do servidor. A permissão ALTER SETTINGS é implicitamente mantida pelas funções de servidor fixas **sysadmin** e **serveradmin** .  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### Para configurar a opção max degree of parallelism  
  
1.  No **Pesquisador de Objetos**, clique com o botão direito do mouse em um servidor e selecione **Propriedades**.  
  
2.  Clique no nó **Avançado** .  
  
3.  Na caixa **Grau Máximo de Paralelismo** , selecione o número máximo de processadores a serem usados na execução de plano paralelo.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
#### Para configurar a opção max degree of parallelism  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo mostra como usar o [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) para configurar a opção `max degree of parallelism` como `8`.  
  
```tsql  
USE AdventureWorks2012 ;  
GO   
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE WITH OVERRIDE;  
GO  
EXEC sp_configure 'max degree of parallelism', 8;  
GO  
RECONFIGURE WITH OVERRIDE;  
GO  
```  
  
 Para obter mais informações, consulte [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
##  <a name="FollowUp"></a> Acompanhamento: depois de configurar a opção max degree of parallelism  
 A configuração entra em vigor imediatamente sem reiniciar o servidor.  
  
## Consulte também  
 [Opção affinity mask de configuração de servidor](../../database-engine/configure-windows/affinity-mask-server-configuration-option.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [DBCC CHECKTABLE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)   
 [DBCC CHECKDB &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)   
 [DBCC CHECKFILEGROUP &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkfilegroup-transact-sql.md)   
 [Configurar operações de índice paralelas](../../relational-databases/indexes/configure-parallel-index-operations.md) 
 [Dicas de consulta &#40;Transact-SQL&#41;](../Topic/Query%20Hints%20\(Transact-SQL\).md)    
 [Opções Set Index](../../relational-databases/indexes/set-index-options.md)  
  
  