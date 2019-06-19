---
title: Instruções SET (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SET
- SET_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ISO SET statements
- queries [SQL Server], executing
- dates [SQL Server], SET statements
- time [SQL Server], SET statements
- SET statement, about SET statement
- SET statement
- statistical information [SQL Server], SET statements
- locking [SQL Server], SET statements
ms.assetid: f7e107f8-0fcf-408b-b30f-da2323eeb714
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azure-sqldw-latest ||= azuresqldb-current || >= sql-server-2016 || >= sql-server-linux-2017 || = sqlallproducts-allversions
ms.openlocfilehash: bc660aeb0ca4e7b56cae69a8eb294c6681b1765c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65620334"
---
# <a name="set-statements-transact-sql"></a>Instruções SET (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-xxx-md.md)]

A linguagem de programação [!INCLUDE[tsql](../../includes/tsql-md.md)] fornece várias instruções SET que alteram a sessão atual que controla informações específicas. As instruções SET são agrupadas nas categorias mostradas na tabela a seguir.  
  
Para obter informações sobre como configurar variáveis locais usando uma instrução [SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md).  
  
|Categoria|Instruções|  
|--------------|----------------|  
|Instruções de data e hora|[SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md)<br /><br /> [SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md)|  
|Instruções de bloqueio|[SET DEADLOCK_PRIORITY](../../t-sql/statements/set-deadlock-priority-transact-sql.md)<br /><br /> [SET LOCK_TIMEOUT](../../t-sql/statements/set-lock-timeout-transact-sql.md)|  
|Instruções diversas|[SET CONCAT_NULL_YIELDS_NULL](../../t-sql/statements/set-concat-null-yields-null-transact-sql.md)<br /><br /> [SET CURSOR_CLOSE_ON_COMMIT](../../t-sql/statements/set-cursor-close-on-commit-transact-sql.md)<br /><br /> [SET FIPS_FLAGGER](../../t-sql/statements/set-fips-flagger-transact-sql.md)<br /><br /> [SET IDENTITY_INSERT](../../t-sql/statements/set-identity-insert-transact-sql.md)<br /><br /> [SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md)<br /><br /> [SET OFFSETS](../../t-sql/statements/set-offsets-transact-sql.md)<br /><br /> [SET QUOTED_IDENTIFIER](../../t-sql/statements/set-quoted-identifier-transact-sql.md)|  
|Instruções de execução de consulta|[SET ARITHABORT](../../t-sql/statements/set-arithabort-transact-sql.md)<br /><br /> [SET ARITHIGNORE](../../t-sql/statements/set-arithignore-transact-sql.md)<br /><br /> [SET FMTONLY](../../t-sql/statements/set-fmtonly-transact-sql.md)<br /> Observação: [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]<br /><br /> [SET NOCOUNT](../../t-sql/statements/set-nocount-transact-sql.md)<br /><br /> [SET NOEXEC](../../t-sql/statements/set-noexec-transact-sql.md)<br /><br /> [SET NUMERIC_ROUNDABORT](../../t-sql/statements/set-numeric-roundabort-transact-sql.md)<br /><br /> [SET PARSEONLY](../../t-sql/statements/set-parseonly-transact-sql.md)<br /><br /> [SET QUERY_GOVERNOR_COST_LIMIT](../../t-sql/statements/set-query-governor-cost-limit-transact-sql.md)<br /><br /> [SET RESULT SET CACHING](../../t-sql/statements/set-result-set-caching-transact-sql.md?view=azure-sqldw-latest) (versão prévia)<br /> Observação:  esse recurso se aplica somente ao SQL Data Warehouse do Azure.<br /><br /> [SET ROWCOUNT](../../t-sql/statements/set-rowcount-transact-sql.md)<br /><br /> [SET TEXTSIZE](../../t-sql/statements/set-textsize-transact-sql.md)|  
|Instruções de configurações ISO|[SET ANSI_DEFAULTS](../../t-sql/statements/set-ansi-defaults-transact-sql.md)<br /><br /> [SET ANSI_NULL_DFLT_OFF](../../t-sql/statements/set-ansi-null-dflt-off-transact-sql.md)<br /><br /> [SET ANSI_NULL_DFLT_ON](../../t-sql/statements/set-ansi-null-dflt-on-transact-sql.md)<br /><br /> [SET ANSI_NULLS](../../t-sql/statements/set-ansi-nulls-transact-sql.md)<br /><br /> [SET ANSI_PADDING](../../t-sql/statements/set-ansi-padding-transact-sql.md)<br /><br /> [SET ANSI_WARNINGS](../../t-sql/statements/set-ansi-warnings-transact-sql.md)|  
|Instruções estatísticas|[SET FORCEPLAN](../../t-sql/statements/set-forceplan-transact-sql.md)<br /><br /> [SET SHOWPLAN_ALL](../../t-sql/statements/set-showplan-all-transact-sql.md)<br /><br /> [SET SHOWPLAN_TEXT](../../t-sql/statements/set-showplan-text-transact-sql.md)<br /><br /> [SET SHOWPLAN_XML](../../t-sql/statements/set-showplan-xml-transact-sql.md)<br /><br /> [SET STATISTICS IO](../../t-sql/statements/set-statistics-io-transact-sql.md)<br /><br /> [SET STATISTICS XML](../../t-sql/statements/set-statistics-xml-transact-sql.md)<br /><br /> [SET STATISTICS PROFILE](../../t-sql/statements/set-statistics-profile-transact-sql.md)<br /><br /> [SET STATISTICS TIME](../../t-sql/statements/set-statistics-time-transact-sql.md)|  
|Instruções de transações|[SET IMPLICIT_TRANSACTIONS](../../t-sql/statements/set-implicit-transactions-transact-sql.md)<br /><br /> [SET REMOTE_PROC_TRANSACTIONS](../../t-sql/statements/set-remote-proc-transactions-transact-sql.md)<br /><br /> [SET TRANSACTION ISOLATION LEVEL](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)<br /><br /> [SET XACT_ABORT](../../t-sql/statements/set-xact-abort-transact-sql.md)| 
  
## <a name="considerations-when-you-use-the-set-statements"></a>Considerações sobre quando usar instruções SET  
  
- Todas as instruções SET executadas no tempo de execução, exceto essas instruções, que são executadas no momento da análise:

  - SET FIPS_FLAGGER
  - SET OFFSETS
  - SET PARSEONLY
  - e SET QUOTED_IDENTIFIER  
  
- Se uma instrução SET for executada em um procedimento armazenado ou gatilho, o valor da opção SET será restaurado depois que o procedimento armazenado ou o gatilho retornar o controle. Além disso, se uma instrução SET for especificada em uma cadeia de caracteres SQL dinâmica que seja executada usando **sp_executesql** ou EXECUTE, o valor da opção SET será restaurado depois que o controle for retornado do lote especificado na cadeia de caracteres SQL dinâmica.  
  
- Os procedimentos armazenados são executados com as configurações SET especificadas no momento da execução, com exceção de SET ANSI_NULLS e SET QUOTED_IDENTIFIER. Os procedimentos armazenados que especificam que SET ANSI_NULLS ou SET QUOTED_IDENTIFIER usam a configuração especificada no momento da criação do procedimento armazenado. Se usada em um procedimento armazenado, qualquer configuração SET será ignorada.  
  
- A configuração **user options** de **sp_configure** permite configurações em todo o servidor e funciona em vários bancos de dados. Essa configuração também se comporta como uma instrução SET explícita, a não ser que ocorra no momento de logon.  
  
- As configurações de banco de dados definidas usando ALTER DATABASE só são válidas em nível do banco de dados e entram em vigor apenas quando definidas explicitamente. As configurações de banco de dados substituem as configurações de opção de instância que são definidas usando **sp_configure**.  
  
- Se uma instrução SET usa ON e OFF, você pode especificar qualquer um para várias opções SET.
  
    > [!NOTE]  
    >  Isso não se aplica às estatísticas relacionadas às opções SET.
  
     Por exemplo, `SET QUOTED_IDENTIFIER, ANSI_NULLS ON` define QUOTED_IDENTIFIER e ANSI_NULLS como ON.  
  
- As configurações da instrução SET substituem as configurações de opção de banco de dados idênticas que são definidas usando ALTER DATABASE. Por exemplo, o valor especificado em uma instrução SET ANSI_NULLS substituirá a configuração de banco de dados por ANSI_NULLs. Além disso, algumas configurações de conexão são definidas automaticamente como ON quando um usuário se conecta a um banco de dados com base nos valores especificados pelo uso anterior da configuração de **sp_configure user options** ou dos valores que se aplicam a todas as conexões ODBC e OLE/DB.  
  
- As instruções ALTER, CREATE e DROP DATABASE não aceitam a configuração SET LOCK_TIMEOUT.  
  
- Quando uma instrução SET global ou de atalho define várias configurações, emitindo o atalho, a instrução SET redefine as configurações anteriores por todas as opções afetadas pela instrução SET de atalho. Se uma opção SET que é afetada por uma instrução SET de atalho for definida depois que a instrução SET de atalho for emitida, a instrução SET individual substituirá as configurações de atalho comparáveis. Um exemplo de uma instrução SET de atalho seria SET ANSI_DEFAULTS.  
  
- Quando lotes são usados, o contexto de banco de dados é determinado pelo lote estabelecido usando a instrução USE. Consultas não planejadas e todas as outras instruções que são executadas fora do procedimento armazenado e que estão em lotes herdam as configurações de opção do banco de dados e a conexão estabelecida pela instrução USE.  
  
- Solicitações MARS (Vários Conjuntos de Resultados Ativos) compartilham um estado global que contém as configurações de opção SET da sessão mais recente. Quando uma solicitação é executada, ela pode modificar as opções SET. As alterações são específicas do contexto de solicitação no qual elas foram definidas e não afetam outras solicitações MARS simultâneas. Entretanto, depois que a execução da solicitação é concluída, as novas opções SET são copiadas para o estado de sessão global. As novas solicitações executadas na mesma sessão depois dessa alteração usarão essas novas configurações de opção SET.  
  
- Quando um procedimento armazenado é executado, seja de um lote ou de outro procedimento armazenado, ele é executado nos valores de opção definidos no banco de dados que contém o procedimento armazenado. Por exemplo, quando o procedimento armazenado **db1.dbo.sp1** chama o procedimento armazenado **db2.dbo.sp2**, o procedimento armazenado **sp1** é executado na configuração de nível de compatibilidade atual do banco de dados **db1** e o procedimento armazenado **sp2** é executado na configuração de nível de compatibilidade atual do banco de dados **db2**.  
  
- Quando uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] se refere a objetos que residem em vários bancos de dados, o contexto de banco de dados atual e o contexto de conexão atual se aplicam a essa instrução. Nesse caso, se a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] estiver em um lote, o contexto de conexão atual será o banco de dados definido pela instrução USE; se a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] estiver em um procedimento armazenado, o contexto de conexão será o banco de dados que contém o procedimento armazenado.  
  
- Ao criar e manipular índices em colunas computadas ou exibições indexadas, você deve definir essas opções SET como ON: ARITHABORT, CONCAT_NULL_YIELDS_NULL, QUOTED_IDENTIFIER, ANSI_NULLS, ANSI_PADDING e ANSI_WARNINGS. Defina a opção NUMERIC_ROUNDABORT como OFF.  
  
  Se não definir uma dessas opções com os valores solicitados, haverá falha nas ações INSERT, UPDATE, DELETE, DBCC CHECKDB e DBCC CHECKTABLE em exibições ou tabelas indexadas com índices em colunas computadas. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gerará um erro que lista todas as opções definidas incorretamente. Além disso, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] processará as instruções SELECT nessas tabelas ou exibições indexadas como se os índices nas colunas computadas ou nas exibições não existissem. 

- Quando SET RESULT_SET_CACHING for ON, o recurso de armazenamento em cache de resultados estará ativado para a sessão atual do cliente.   O Result_set_caching não pode ser ATIVADO para uma sessão se estiver DESATIVADO no nível do banco de dados.    Quando SET RESULT_SET_CACHING for OFF, o recurso de armazenamento em cache de resultados estará desativado para a sessão atual do cliente. A alteração dessa configuração requer associação na função pública.
Aplica-se a: SQL Data Warehouse do Azure Gen2