---
title: Configurar a opção de configuração de servidor max degree of parallelism | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- parallel queries [SQL Server]
- processors [SQL Server], parallel queries
- number of processors for parallel queries
- max degree of parallelism option
ms.assetid: 86b65bf1-a6a1-4670-afc0-cdfad1558032
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 824dc837142acc4a0898cb04b4a8687bc5be4043
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84935667"
---
# <a name="configure-the-max-degree-of-parallelism-server-configuration-option"></a>Configurar a opção de configuração de servidor max degree of parallelism
  Este tópico descreve como configurar a `max degree of parallelism` opção de configuração de servidor no usando o ou o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] . Quando uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é executada em um computador com mais de um microprocessador ou CPU, ele detecta o melhor grau de paralelismo, ou seja, o número de processadores utilizados para executar uma única instrução, para cada execução paralela de plano. É possível usar a opção `max degree of parallelism` para limitar o número de processadores a serem usados na execução paralela do plano. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] considera os planos de execução paralela para consultas, operações DDL (linguagem de definição de dados) e população de cursor estático e controlado por conjunto de chaves.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Recomendações](#Recommendations)  
  
     [Segurança](#Security)  
  
-   **Para configurar a opção max degree of parallelism usando**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Acompanhamento:**  [depois de configurar a opção max degree of parallelism](#FollowUp)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
  
-   Se a opção de máscara de afinidade não estiver definida com o padrão, poderá restringir o número de processadores disponíveis para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em sistemas SMP simétricos.  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> Recomendações  
  
-   Esta é uma opção avançada e deve ser alterada somente por um administrador de banco de dados experiente ou técnico certificado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Para permitir que o servidor determine o grau máximo de paralelismo, defina essa opção como 0, o valor padrão. A definição do grau máximo de paralelismo como 0 permite que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] use todos os processadores disponíveis, até 64 processadores. Para suprimir a geração de planos paralelos, defina `max degree of parallelism` como 1. Defina o valor como um número de 1 a 32.767 para especificar o número máximo de núcleos de processador que podem ser usados por uma única execução de consulta. Se um valor maior do que o número de processadores disponíveis for especificado, o número real de processadores disponíveis será usado. Se o computador tiver apenas um processador, o valor de `max degree of parallelism` será ignorado.  
  
-   Você pode substituir o valor max degree of parallelism nas consultas ao especificar a dica de consulta MAXDOP na instrução de consulta. Para obter mais informações, veja [Dicas de consulta &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-query).  
  
-   As operações de índice que criam ou reconstroem um índice ou descartam um índice clusterizado podem usar muitos recursos. Você pode substituir o valor max degree of parallelism das operações de índice especificando a opção de índice MAXDOP na instrução de índice. O valor MAXDOP é aplicado à instrução no tempo de execução e não é armazenado nos metadados do índice. Para obter mais informações, consulte [Configurar operações de índice paralelo](../../relational-databases/indexes/configure-parallel-index-operations.md).  
  
-   Além das consultas e das operações de índice, essa opção também controla o paralelismo de DBCC CHECKTABLE, DBCC CHECKDB e DBCC CHECKFILEGROUP. É possível desabilitar a execução paralela de planos para essas instruções usando o sinalizador de rastreamento 2528. Para obter mais informações, veja, [Sinalizadores de rastreamento &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql).  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Permissões de execução sem parâmetros ou com apenas o primeiro parâmetro em **sp_configure** são concedidas a todos os usuários por padrão. Para executar **sp_configure** com ambos os parâmetros para alterar uma opção de configuração ou executar a instrução RECONFIGURE, o usuário deve ter a permissão ALTER SETTINGS no nível do servidor. A permissão ALTER SETTINGS é implicitamente mantida pelas funções de servidor fixas **sysadmin** e **serveradmin** .  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-configure-the-max-degree-of-parallelism-option"></a>Para configurar a opção max degree of parallelism  
  
1.  No **Pesquisador de Objetos**, clique com o botão direito do mouse em um servidor e selecione **Propriedades**.  
  
2.  Clique no nó **Avançado** .  
  
3.  Na caixa **Grau Máximo de Paralelismo** , selecione o número máximo de processadores a serem usados na execução de plano paralelo.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-configure-the-max-degree-of-parallelism-option"></a>Para configurar a opção max degree of parallelism  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo mostra como usar o [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) para configurar a opção `max degree of parallelism` como `8`.  
  
```sql  
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
  
 Para obter mais informações, veja [Opções de configuração do servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md).  
  
##  <a name="follow-up-after-you-configure-the-max-degree-of-parallelism-option"></a><a name="FollowUp"></a> Acompanhamento: depois de configurar a opção grau máximo de paralelismo  
 A configuração entra em vigor imediatamente sem reiniciar o servidor.  
  
## <a name="see-also"></a>Consulte Também  
 [Opção affinity mask de configuração de servidor](affinity-mask-server-configuration-option.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)   
 [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)   
 [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)   
 [DBCC CHECKtable &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checktable-transact-sql)   
 [DBCC CHECKDB &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql)   
 [DBCC CHECKFILEGROUP &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkfilegroup-transact-sql)   
 [Configurar operações de índice paralelo](../../relational-databases/indexes/configure-parallel-index-operations.md)   
 [Dicas de consulta &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-query)   
 [Definir opções de índice](../../relational-databases/indexes/set-index-options.md)  
  
  
