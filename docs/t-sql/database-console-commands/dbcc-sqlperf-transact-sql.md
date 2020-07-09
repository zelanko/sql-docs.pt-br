---
title: DBCC SQLPERF (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2018
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SQLPERF
- DBCC_SQLPERF_TSQL
- SQLPERF_TSQL
- DBCC SQLPERF
dev_langs:
- TSQL
helpviewer_keywords:
- statistical information [SQL Server], transaction logs
- transaction logs [SQL Server], space usage
- space [SQL Server], transaction logs
- DBCC SQLPERF statement
ms.assetid: ec9225ce-e20f-4b03-8b3a-7bcad8a649df
author: pmasl
ms.author: umajay
ms.openlocfilehash: 4132d5ec459f5fb180ebea94665449cefa7e961a
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85882014"
---
# <a name="dbcc-sqlperf-transact-sql"></a>DBCC SQLPERF (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Fornece estatísticas de uso do espaço do log de transações para todos os bancos de dados. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)],ele também pode ser usado para redefinir as estatísticas de espera e de trava.
  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior), [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] ([versão prévia em algumas regiões](https://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag))
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```
DBCC SQLPERF   
(  
     [ LOGSPACE ]  
     | [ "sys.dm_os_latch_stats" , CLEAR ]  
     | [ "sys.dm_os_wait_stats" , CLEAR ]  
)   
     [WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>Argumentos  
LOGSPACE  
Retorna o tamanho atual do log de transações e a porcentagem de espaço usado pelo log para cada banco de dados. Use essas informações para monitorar a quantidade de espaço usado em um log de transações.

> [!IMPORTANT]
> Para obter mais informações sobre informações de uso de espaço para o log de transações, começando com o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], veja a seção [Comentários](#Remarks) neste tópico.
  
**"sys.dm_os_latch_stats"** , CLEAR  
Zera as estatísticas de trava. Para obter mais informações, confira [sys.dm_os_latch_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md). Essa opção não está disponível no [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
**"sys.dm_os_wait_stats"** , CLEAR  
Zera as estatísticas de espera. Para obter mais informações, confira [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md). Essa opção não está disponível no [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
WITH NO_INFOMSGS  
Suprime todas as mensagens informativas com níveis de severidade de 0 a 10.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 A tabela a seguir descreve as colunas do conjunto de resultados.  
  
|Nome da coluna|Definição|  
|---|---|
|**Database Name**|Nome do banco de dados da estatística de logs exibida.|  
|**Tamanho do log (MB)**|Tamanho atual alocado ao log. Esse valor sempre é menor que a quantidade alocada originalmente para o espaço de log porque o [!INCLUDE[ssDE](../../includes/ssde-md.md)] reserva uma quantidade pequena de espaço em disco para informações de cabeçalho internas.|  
|**Espaço de log usado (%)**|Percentual do arquivo de log em uso no momento para armazenar as informações do log de transações no momento.|  
|**Status**|Status do arquivo de log. Sempre 0.|  
  
## <a name="remarks"></a><a name="Remarks"></a> Comentários  
Começando com o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], é necessário usar a DMV (exibição de gerenciamento dinâmico) [sys.dm_db_log_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md) em vez de `DBCC SQLPERF(LOGSPACE)` para retornar as informações de uso de espaço do log de transações por banco de dados.    
 
O log de transações registra cada transação feita em um banco de dados. Para obter mais informações, confira [O log de transações &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md) e [Guia de arquitetura e gerenciamento de log de transações do SQL Server](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md).
  
## <a name="permissions"></a>Permissões  
No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a execução de `DBCC SQLPERF(LOGSPACE)` requer a permissão `VIEW SERVER STATE` no servidor. Para redefinir as estatísticas de espera e trava, é necessária a permissão `ALTER SERVER STATE` no servidor.
  
No [!INCLUDE[ssSDS](../../includes/sssds-md.md)], as camadas Premium e Comercialmente Críticas requerem a permissão `VIEW DATABASE STATE` no banco de dados. No [!INCLUDE[ssSDS](../../includes/sssds-md.md)], as camadas Standard, Básica e de Uso Geral requerem a conta do administrador [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. Não há suporte para reiniciar as estatísticas de espera e de trava.
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-displaying-log-space-information-for-all-databases"></a>a. Exibindo informações de espaço de log para todos os bancos de dados  
O exemplo a seguir exibe informações de `LOGSPACE` sobre todos os bancos de dados contidos na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
```sql  
DBCC SQLPERF(LOGSPACE);  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
Database Name Log Size (MB) Log Space Used (%) Status        
------------- ------------- ------------------ -----------   
master         3.99219      14.3469            0   
tempdb         1.99219      1.64216            0   
model          1.0          12.7953            0   
msdb           3.99219      17.0132            0   
AdventureWorks 19.554688    17.748701          0  
```  
  
### <a name="b-resetting-wait-statistics"></a>B. Redefinindo estatísticas de espera  
O exemplo a seguir zera as estatísticas de espera da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
```sql  
DBCC SQLPERF("sys.dm_os_wait_stats",CLEAR);  
```  
  
## <a name="see-also"></a>Consulte Também  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)   
[sys.dm_os_latch_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md)    
[sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)     
[sp_spaceused &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)    
[sys.dm_db_log_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md)    
[sys.dm_db_log_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)     
[sys.dm_db_log_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md)     

